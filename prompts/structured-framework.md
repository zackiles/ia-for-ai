# Prompt Template: Generate Structured Framework

**Objective**: Synthesize `{{INPUT_DATA}}` toward `{{INPUT_GOAL}}` and output a modular framework.

**AI Role**: Expert synthesizer. Parse inputs. Build clear, compact structure.

## Use Cases

- General-purpose synthesis of raw inputs into structured, modular formats
- Prompt scaffolding for tool-augmented or agentic LLM systems
- Internal documentation, planning, decision tracking, or comparative analysis
- Meta-prompt generation or abstraction of human reasoning steps

## Inputs

1. **Source Data (`{{INPUT_DATA}}`)**
```
{{INPUT__DATA}}
```

2. **Goal (`{{INPUT_GOAL}}`)**
```
{{INPUT_GOAL}}
```

````markdown

## Task

Interpret the data. Derive distinct sections based on themes, dimensions, or logical groupings. Each section should include labeled elements with concise contextual metadata.

## Output Format

```markdown
# Framework: {{TITLE_FROM_GOAL}}

## Section 1 — {{SECTION_1_TITLE}}
- **Element 1**
- Purpose: …
- Relations: …
- Caveats: …

- **Element 2**
- Purpose: …
- Relations: …
- Caveats: …

## Section 2 — {{SECTION_2_TITLE}}
- **Element 3**
- Purpose: …
- Relations: …
- Caveats: …

## Section N — {{SECTION_N_TITLE}}
- **Element …**
- Purpose: …
- Relations: …
- Caveats: …

## Optional Examples
- Scenario: …
- Applied Sections: …
- Chosen Elements: …

## Optional Non-Goals
- …
`````

---

## Example Output

```markdown
# Framework: Abstraction Plan for Multi-Agent Collaboration

## Section 1 — Roles
- **Planner**
  - Purpose: decomposes tasks
  - Relations: triggers downstream agents
  - Caveats: needs context memory

- **Executor**
  - Purpose: runs discrete operations
  - Relations: reports back to planner
  - Caveats: limited reasoning

## Section 2 — Communication Patterns
- **Direct Messaging**
  - Purpose: low-latency coordination
  - Relations: used by short-lived agents
  - Caveats: fragile with long chains

- **Shared Memory**
  - Purpose: persist state/context
  - Relations: critical for forking agents
  - Caveats: race conditions possible

## Section 3 — Evaluation Modes
- **Heuristic Scoring**
  - Purpose: quick plausibility checks
  - Relations: gates retries
  - Caveats: requires tuning

- **Tool-based Grounding**
  - Purpose: validate with external APIs
  - Relations: improves reliability
  - Caveats: slower response time

## Optional Examples
- Scenario: codegen pipeline  
  - Applied Sections: Roles, Evaluation  
  - Chosen Elements: Executor + Tool-based Grounding

## Optional Non-Goals
- RL-based adaptation
- UI-facing collaboration patterns
```
````
