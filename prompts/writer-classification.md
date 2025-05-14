# Writer Classification
This template performs structured analysis of an author’s writing to reverse-engineer their stylistic, psychological, and linguistic signatures. It enables deterministic classification and cloning of authorial voice for generative, mimetic, or normalization tasks, supporting use cases such as outlier detection, style harmonization, persona simulation, and discourse mediation in symbolic and dependency-structured language systems.

## Use Cases

### 1. **Outlier Detection and Content Governance**

* **Detect idiolectal drift**: Identify when internal documentation, emails, or reports deviate from accepted tone, style, or structure.
* **Flag unstandardized contributions**: Spot denormalized or rogue writing (e.g. non-compliant executive notes, verbose wiki entries).
* **Audit tone compliance**: Classify emotional tone or stylistic variance against norms for branding or regulatory consistency.

### 2. **Normalization and Harmonization**

* **Auto-convert to house style**: Use the normalized template output to rewrite text into enterprise-consistent voice and format.
* **Suggest inline rewrites**: Let agents offer tone/style corrections (e.g. overuse of passive voice, jargon injections, inconsistent tense).
* **Train LLMs on uniform data**: Curate a high-quality normalized corpus from denormalized inputs to fine-tune agents for enterprise-safe communication.

### 3. **Author Attribution and Metadata Enrichment**

* **Infer authorship probabilistically** using denormalized traits (idiolect, lexical markers, clause rhythm).
* **Cluster documents by writing fingerprint** to surface ghostwriting, misattribution, or security anomalies.

### 4. **Voice Cloning and Persona Simulation**

* **Train LLM agents to mimic internal personas** (e.g. "summarize like Zach", "draft like legal", "respond like CTO").
* **Generate synthetic agents** that replicate founder/executive tone with deterministic fidelity for async or high-scale communication.

### 5. **Cross-Domain Mediation**

* **Translate between normalized and denormalized registers** (e.g., dev-to-exec summaries, legal-to-sales rewrites).
* **Enable agents to reason about discourse tone shifts**, e.g. summarizing with tone transformation or flattening style for external use.

## Inputs

- `AUTHORS_TEXT`: 50,000 tokens of an author's writing.

---

````txt
TEMPLATE_PROMPT

Task  
Analyze the following corpus and render five ordered sections exactly as specified, using terse dependency‑grammar sentences (minimal prepositional stacking, subject‑verb‑object precedence, left‑branch modifiers). Do not add other headings, prefatory text, or conclusions.

===START_AUTHOR_TEXT===
{$AUTHORS_TEXT}
===END_AUTHOR_TEXT===

Section 1  Style and Prose  
• Sentence geometry – mean clause length, dominant dependency direction, coordination vs subordination ratios.  
• Register oscillation – shifts between technical, colloquial, poetic.  
• Formatting devices – lists, code fences, inline markup, whitespace tricks.  
• Prosody markers – expletives, ellipses, dashes, interrobangs, emoji.  
• Rhythm tactics – anaphora, polysyndeton, abrupt enjambment.

Section 2  Temperament  
• Dominant affect (e.g., sardonic, earnest).  
• Motivational posture (intrinsic curiosity, status display, evangelism).  
• Self‑presentation pattern (self‑effacement, bravado, didactic stance).  
• Social orientation (collaborative, antagonistic, mentor‑like).  
• Emotional volatility cues (caps bursts, apology loops, sarcasm density).

Section 3  Lexical Idiosyncrasies  
Return a markdown table:

| token | gloss/meaning | function or origin note | part of speech | contextual evidence (quoted fragment) |

Include 8‑12 rows, choose tokens rare in mainstream North‑American English (zipf < 4) or author‑coined.

Section 4  Psychoanalytic Sketch  
• Map ego, superego, id manifestations with textual proof.  
• Big‑Five estimates (Openness, Conscientiousness, Extraversion, Agreeableness, Neuroticism) on ↑/↕/↓ scale; justify each.  
• Ideological signals (hacker ethos, academic rigor, counterculture lean).  
• Coping mechanisms (humor, meticulous detail, bravado).  
• Recurring metaphors revealing core schema (e.g., war, game, pilgrimage).

Section 5  Generative Template  
Sub‑section A  Macro‑Structure  
1  Preamble token (author‑signature, date‑stamp).  
2  Hook: imperative + rhetorical question.  
3  Body loop: for each topic, produce SVO core → inline code or math → parenthetical digression.  
4  Enumeration block: bullet list with colon then two‑clause elaboration.  
5  Digression stack: quote external source → relate to niche detail.  
6  Abrupt closure (future hint or mock threat).

Sub‑section B  Symbolic Rules  
• Vocabulary partitions: {Jargon}, {Slang}, {Insult}, {Citation}.  
• Selector algorithm: every third clause swap register Jargon⇄Slang.  
• Dependency order: root verb early, NP complements left, adjuncts right.  
• Rare‑token injection probability p = 0.07 from idiolect list.  
• Punctuation stochasticity: choose among “— … !! ?!” with weights [0.2,0.4,0.3,0.1].

Sub‑section C  Deterministic Prompt Skeleton  
Provide a canonical skeleton the generator can fill:

```

{SIGNATURE} {ISO‑DATE}
{IMPERATIVE\_HOOK}?!
{BODY\_LOOP}

* {ENUM\_ITEM}: {DETAIL\_CLAUSE\_1}; {DETAIL\_CLAUSE\_2}
  {QUOTE} — {SOURCE}
  {CLOSING\_STINGER}

```

End of template.
````

## Example Output

````markdown
## Style and Prose

john doe writes in rapid clause‑dense bursts that fuse systems jargon with irreverent slang, often dropping articles and capital letters for speed ([example.com/1], [example.com/2]).
he embeds inline code fences, bullet cascades, and parenthetical asides to chunk dense material while sustaining narrative momentum ([example.com/3], [example.com/4]).
sentences sprawl yet maintain left‑branching dependency chains, linking verbs to objects early and appending modifiers late ([example.com/3], [example.com/5]).
lexical register oscillates between academic precision (“temporal vs positional transparency”) and gutter humor (“spooooooooky tmux”) without apology ([example.com/3], [example.com/2]).
he favours imperative mood (“file bugs”) and direct address, pushing agency onto the reader ([example.com/2], [example.com/6]).
exclamation and ellipsis punctuate enthusiasm and doubt in equal measure ([example.com/7], [example.com/2]).

## Temperament

tone mixes swagger and self‑laceration; author trumpets achievements yet calls past ideas “scandalous levels of stupidity,” signalling perfectionist neuroticism and open self‑review ([example.com/2]).
curiosity dominates; long digressions into microarchitecture, protocol minutiae, or book logistics show intrinsic motivation for mastery ([example.com/3], [example.com/7]).
sarcasm shields vulnerability, but empathy surfaces when advising students or praising diverse workplaces ([example.com/8], [example.com/9]).

## Lexical Idiosyncrasies

| token | gloss | note | source |
|‑|‑|‑|‑|
| johndoer | author’s location tag | playful self‑branding | example.com/view0 |
| sprixel | portmanteau sprite + sixel | technical neologism | example.com/view2 |
| dotriacontacore | 32‑core epithet | rare Greco‑Latin numeral | example.com/view4 |
| Craysian Chair of Badassery | tongue‑in‑cheek title | academic parody | example.com/view3 |
| mouthfoam | vivid self‑mockery | visceral metaphor | example.com/view1 |
| COTS by lots | rhyme mnemonic | procurement maxim | example.com/view4 |

## Psychoanalytic Sketch

ego seeks competence validation through baroque technical exposition; superego manifests in relentless self‑critique; id peeks via profanity and impulsive humor.
big‑five guess: openness ↑↑, conscientiousness ↑, extraversion ↕, agreeableness ↕, neuroticism ↑.
writer internalizes hacker ethos (meritocratic, skeptical, tinkering) and romanticizes physical craft, indicating need for tactile control amid abstract software work ([example.com/10]).

## Generative Template (symbolic‑system lens)

```

1  preamble
self‑deprecating confession (token =SORRYFORTHIS)
2  context‑anchor
“johnblog! YYYY‑MM‑DD, HHMM TZ, at the johntower”
3  hook
imperative to reader + rhetorical question
4  body loop
while topic\_list:
short SVO clause → inline code span → parenthetical tangent
if excitement: append expletive or “!!”
if doubt: append ellipsis + self‑insult
5  digression stack
quote(literary|academic) → relate to niche tech detail
6  enumerations
“\* bullet phrase:” + 2‑clause elaboration
7  closure
abrupt future intent or mock threat, no summary

```

symbolic model: let Σ be vocabulary, partition into Jargon, Slang, Insult, Quote.
generate dependency tree with root verb early; attach noun phrases left; append adjuncts right.
apply alternation rule: Jargon → Slang every Δ≈3 clauses to maintain register oscillation.
insert rare tokens from idiolect set with probability p=0.07 to evoke authorship.
```

````
