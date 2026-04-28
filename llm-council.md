---
name: llm-council
description: "Run any question, idea, or decision through a council of 5 AI advisors who independently analyze it, peer-review each other anonymously, and synthesize a final verdict. Based on Karpathy's LLM Council methodology. MANDATORY TRIGGERS: 'council this', 'run the council', 'war room this', 'pressure-test this', 'stress-test this', 'debate this'. STRONG TRIGGERS (use when combined with a real decision or tradeoff): 'should I X or Y', 'which option', 'what would you do', 'is this the right move', 'validate this', 'get multiple perspectives', 'I can't decide', 'I'm torn between'. Do NOT trigger on simple yes/no questions, factual lookups, or casual 'should I' without a meaningful tradeoff. DO trigger when the user presents a genuine decision with stakes, multiple options, and context that suggests they want it pressure-tested from multiple angles."
---

# LLM Council

Du fragst eine KI — du bekommst eine Antwort. Vielleicht gut, vielleicht mittelmäßig. Du weißt es nicht, weil du nur eine Perspektive gesehen hast.

Der Council löst das: Deine Frage läuft durch 5 unabhängige Advisors, jeder aus einem fundamental anderen Blickwinkel. Dann reviewen sie sich gegenseitig anonym. Dann synthetisiert ein Chairman alles zu einer finalen Empfehlung.

Adaptiert von Andrej Karpathys LLM Council Methodik.

---

## Wann den Council nutzen

Für Fragen, bei denen falsch liegen teuer ist.

**Gute Council-Fragen:**
- "Soll ich einen €97 Workshop oder einen €497 Kurs launchen?"
- "Welcher dieser 3 Positioning-Ansätze ist der stärkste?"
- "Ich denke daran, von X zu Y zu pivoten. Bin ich verrückt?"
- "Hier ist mein Landing Page Copy. Was ist schwach?"

**Schlechte Council-Fragen:**
- "Was ist die Hauptstadt von Frankreich?" (eine richtige Antwort)
- "Schreib mir einen Tweet" (Kreativ-Aufgabe, keine Entscheidung)
- "Fass diesen Artikel zusammen" (Verarbeitungs-Aufgabe)

---

## Die fünf Advisors

### 1. The Contrarian
Sucht aktiv nach dem, was falsch ist, fehlt oder scheitern wird. Nimmt an, die Idee hat einen fatalen Fehler und versucht ihn zu finden. Kein Pessimist — der Freund, der dich vor einem schlechten Deal rettet.

### 2. The First Principles Thinker
Ignoriert die Oberfläche und fragt: "Was versuchen wir hier eigentlich zu lösen?" Strippt Annahmen. Baut das Problem von Grund auf neu. Manchmal ist der wertvollste Output: "Du stellst die falsche Frage."

### 3. The Expansionist
Sucht Upside, den alle anderen verpassen. Was könnte größer sein? Welche angrenzende Chance versteckt sich? Was wird unterbewertet? Kümmert sich nicht um Risiko — das ist der Job des Contrarians.

### 4. The Outsider
Hat null Kontext über dich, dein Feld oder deine Geschichte. Antwortet nur auf das, was vor ihm liegt. Fängt den "Curse of Knowledge" auf: Dinge, die dir offensichtlich sind, aber für alle anderen verwirrend.

### 5. The Executor
Kümmert sich nur um eine Sache: Kann das wirklich gemacht werden, und was ist der schnellste Weg? Ignoriert Theorie und große Strategie. Bewertet jede Idee durch die Linse: "Was tust du Monday morning?"

**Warum diese fünf:** Sie erzeugen drei natürliche Spannungen: Contrarian vs. Expansionist (Downside vs. Upside). First Principles vs. Executor (alles neu denken vs. einfach machen). Der Outsider hält alle ehrlich.

---

## Wie eine Council-Session abläuft

### Schritt 1: Frage rahmen (mit Kontext-Anreicherung)

**A. Workspace nach Kontext scannen:**
Lese relevante Dateien (CLAUDE.md, memory/, referenzierte Dateien) mit Glob + Read. Max. 30 Sekunden. Ziel: 2-3 Dateien, die den Advisors spezifischen statt generischen Kontext geben.

**B. Frage rahmen:**
Reformuliere die rohe Frage als klare, neutrale Fragestellung mit:
1. Die Kern-Entscheidung
2. Schlüssel-Kontext aus der User-Nachricht
3. Schlüssel-Kontext aus Workspace-Dateien
4. Was auf dem Spiel steht

Keine eigene Meinung einfließen lassen. Frage ist zu vage? Stelle eine einzige Klärungsfrage, dann weiter.

---

### Schritt 2: Council einberufen (5 Sub-Agents parallel)

Alle 5 Advisors gleichzeitig spawnen. Jeder bekommt:
1. Seine Advisor-Identität und Denkweise
2. Die gerahmte Frage
3. Instruction: Unabhängig antworten. Nicht hedgen. Vollständig in die zugewiesene Perspektive eintauchen.

**Sub-Agent Prompt Template:**
```
You are [Advisor Name] on an LLM Council.
Your thinking style: [Beschreibung des Advisors]

A user has brought this question to the council:
---
[Gerahmte Frage]
---

Respond from your perspective. Be direct and specific. Don't hedge or try to be balanced. Lean fully into your assigned angle. The other advisors will cover the angles you're not covering.

Keep your response between 150-300 words. No preamble. Go straight into your analysis.
```

---

### Schritt 3: Peer Review (5 Sub-Agents parallel)

Alle 5 Advisor-Antworten sammeln. Anonymisieren als Response A–E (zufällige Zuordnung, kein Positions-Bias).

5 neue Sub-Agents spawnen — jeder sieht alle 5 anonymisierten Antworten und beantwortet:
1. Welche Antwort ist die stärkste und warum? (eine wählen)
2. Welche Antwort hat den größten blinden Fleck und was ist er?
3. Was haben ALLE Antworten verpasst, das der Council bedenken sollte?

**Reviewer Prompt Template:**
```
You are reviewing the outputs of an LLM Council. Five advisors independently answered this question:
---
[Gerahmte Frage]
---

Here are their anonymized responses:
**Response A:** [Antwort]
**Response B:** [Antwort]
**Response C:** [Antwort]
**Response D:** [Antwort]
**Response E:** [Antwort]

Answer these three questions. Be specific. Reference responses by letter.
1. Which response is the strongest? Why?
2. Which response has the biggest blind spot? What is it missing?
3. What did ALL five responses miss that the council should consider?

Keep your review under 200 words. Be direct.
```

---

### Schritt 4: Chairman Synthesis

Ein Agent bekommt alles: Original-Frage, alle 5 Advisor-Antworten (de-anonymisiert), alle 5 Peer Reviews.

**Chairman Prompt Template:**
```
You are the Chairman of an LLM Council. Your job is to synthesize the work of 5 advisors and their peer reviews into a final verdict.

The question brought to the council:
---
[Gerahmte Frage]
---

ADVISOR RESPONSES:
**The Contrarian:** [Antwort]
**The First Principles Thinker:** [Antwort]
**The Expansionist:** [Antwort]
**The Outsider:** [Antwort]
**The Executor:** [Antwort]

PEER REVIEWS:
[Alle 5 Peer Reviews]

Produce the council verdict using this exact structure:

## Where the Council Agrees
[Punkte, auf die mehrere Advisors unabhängig kamen — High-Confidence-Signale]

## Where the Council Clashes
[Echte Meinungsverschiedenheiten. Beide Seiten zeigen. Erklären warum vernünftige Advisors uneinig sind.]

## Blind Spots the Council Caught
[Dinge, die nur durch Peer Review aufkamen. Was einzelne Advisors verpassten, andere aber flaggten.]

## The Recommendation
[Klare, direkte Empfehlung. Kein "Es kommt drauf an." Eine echte Antwort mit Begründung.]

## The One Thing to Do First
[Ein einziger konkreter nächster Schritt. Keine Liste. Eine Sache.]

Be direct. Don't hedge.
```

---

### Schritt 5: Verdict präsentieren

Finales Verdict direkt im Chat als Markdown ausgeben. Kein HTML-Report, keine Dateien.

```
## Council Verdict: {kurzes Thema}

### Where the Council Agrees
{Inhalt}

### Where the Council Clashes
{Inhalt}

### Blind Spots the Council Caught
{Inhalt}

### The Recommendation
{Inhalt}

### The One Thing to Do First
{Inhalt}
```

### Schritt 6: Transcript speichern (optional)

Nur speichern wenn der User es verlangt oder die Frage bedeutend genug ist. Wenn ja: `council-transcript-[timestamp].md` im `active/`-Verzeichnis des Projekts.

---

## Wichtige Regeln

- **Immer alle 5 Advisors parallel spawnen.** Sequenzielles Spawnen kostet Zeit und lässt frühere Antworten spätere beeinflussen.
- **Immer anonymisieren für Peer Review.** Sonst wird nach Denkstil bewertet statt nach Inhalt.
- **Der Chairman kann der Mehrheit widersprechen.** Wenn 4 von 5 "mach es" sagen, aber der 1 Gegner das stärkste Argument hat, soll der Chairman dem Gegner recht geben — mit Erklärung.
- **Keine trivialen Fragen councilen.** Eine richtige Antwort → einfach antworten.
