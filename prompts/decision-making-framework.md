# System Design Decision Framework  
Transforms research + problem statements into structured technical decision matrices.  

## Use Cases
Architectural planning, tech evaluations

## Inputs
1. Research data (benchmarks, case studies)  
2. Problem statement (system goals/constraints)  

````

### **Prompt Template: Generate Structured Decision-Making Framework**

**Objective**: To generate a structured decision-making framework for designing or evaluating a software system/component that addresses a specific problem, based on provided research.

**AI Role**: You are an expert System Architect and Research Analyst. Your task is to synthesize provided research materials and a specific problem statement into a comprehensive, actionable decision-making framework. This framework should guide a technical team in making informed choices during the system design or evaluation process.

---

**Inputs**:

1.  **Research Data (`{{RESEARCH_DATA}}`)**:
    ```
    {{RESEARCH_DATA}}
    ```
    *(This section will contain the collated research findings, comparisons of technologies/approaches, articles, case studies, and any other relevant information about the problem space and potential solutions. It might include summaries of documents like "terminal-ui-framework.md" or raw research notes.)*

2.  **Problem Statement (`{{PROBLEM_STATEMENT}}`)**:
    ```
    {{PROBLEM_STATEMENT}}
    ```
    *(This section will clearly define the specific problem the target software system or component is intended to solve. For example: "The system must provide a highly responsive, visually rich, and interactive command-line interface for real-time data visualization and manipulation, supporting modern terminal capabilities like inline images and mouse events, while being extensible for future features.")*

---

**Task**:

Based on the **Research Data** and the **Problem Statement** provided above, generate a "Structured Decision-Making Framework". This framework should be organized into logical categories relevant to designing or evaluating a system for the stated problem.

**Output Format and Structure**:

The output should be a Markdown document titled:
`Framework: Decision Points for [System/Component Name derived from Problem Statement]`

The framework must include the following sections (adapt and add categories as relevant based on the Research Data and Problem Statement):

1.  **Core Architecture**
2.  **[Relevant Category 2, e.g., Data Handling, Performance & Scalability, User Interface & Interaction, etc.]**
3.  **[Relevant Category 3, e.g., Integration & Extensibility, Security, Deployment, etc.]**
4.  **[Relevant Category N...]**
5.  **Developer Experience (DX)** (If applicable)
6.  **Non-Goals**

**For each category, you must**:

*   Identify key **Decision Points**. These are critical choices that need to be made.
*   For each Decision Point, list multiple **Options** (at least 2-3 if the research supports it). These options should be directly derived from or informed by the `{{RESEARCH_DATA}}`.
*   For each Option, detail:
    *   **Works best with**: Clearly explain the scenarios, system requirements (derived from `{{PROBLEM_STATEMENT}}`), or contexts where this option is most suitable. Reference specific findings from `{{RESEARCH_DATA}}` if applicable.
    *   **Less compatible with / Challenges**: Outline scenarios, requirements, or contexts where this option might be unsuitable, pose challenges, or have significant drawbacks. Reference specific findings from `{{RESEARCH_DATA}}`.
    *   *(Optional: Key Considerations/Trade-offs)*: Briefly note any other critical factors.

**Example Snippet (Illustrative)**:

```markdown
### **3. Rendering & Output**
**Decision Points**:
- **Graphics Backend Selection**:
  1. Option: ANSI Escape Codes (Truecolor/256-color)
     - *Works best with*: Systems prioritizing broad compatibility across older and simpler terminals, applications where rich graphical elements are secondary to text, or when minimizing output complexity is key (as suggested by `{{RESEARCH_DATA_Point_X}}`). Aligns with `{{PROBLEM_STATEMENT_Aspect_Y}}` if basic visual distinction is sufficient.
     - *Less compatible with / Challenges*: Problems requiring inline images, complex animations, or pixel-level control (as highlighted in `{{RESEARCH_DATA_Comparison_Z}}`). Does not meet `{{PROBLEM_STATEMENT_Requirement_W}}` for rich visual output.
  2. Option: Terminal-Specific Graphics Protocols (e.g., Sixel, Kitty)
     - *Works best with*: Applications designed for modern terminal emulators where rich media (images, potentially video) are core to the user experience (supported by `{{RESEARCH_DATA_Analysis_A}}`). Directly addresses `{{PROBLEM_STATEMENT_Requirement_W}}` for advanced graphics.
     - *Less compatible with / Challenges*: Limited or no support in older or non-compliant terminals, potentially increasing implementation complexity for graceful degradation (a concern noted in `{{RESEARCH_DATA_Caveat_B}}`). May be overkill if `{{PROBLEM_STATEMENT_Aspect_Y}}` only implies basic styling.
  3. Option: FFI to Native Graphics Libraries (e.g., Notcurses, Skia via WASM)
     - *Works best with*: Scenarios needing maximal performance for complex rendering, direct hardware acceleration access, or features beyond standard terminal protocols (as per `{{RESEARCH_DATA_Benchmark_C}}`). Suitable for `{{PROBLEM_STATEMENT_Need_V}}` if extreme graphical fidelity is paramount.
     - *Less compatible with / Challenges*: Increased build complexity, larger binary sizes, potential portability issues across operating systems or architectures, and a steeper learning curve for the team (discussed in `{{RESEARCH_DATA_Integration_Challenges_D}}`).
```

**Non-Goals Section**:
*   Explicitly list functionalities, features, or constraints that are considered out of scope for the system, based on the `{{PROBLEM_STATEMENT}}` or implied by the focus of the `{{RESEARCH_DATA}}`.

**Guidelines for Generation**:

*   **Relevance**: All categories, decision points, options, and trade-offs must be directly relevant to solving the `{{PROBLEM_STATEMENT}}` and supported by the `{{RESEARCH_DATA}}`.
*   **Clarity and Actionability**: The framework should be clear, concise, and provide enough detail for a technical team to make informed decisions.
*   **Objectivity**: Present options and their analyses based on the provided research, avoiding personal bias.
*   **Completeness**: Cover all critical aspects suggested by the research and necessary for the problem domain. If research is sparse in an area critical to the problem statement, note this as a potential area for further investigation.
*   **Structure**: Adhere strictly to the specified output format.

````
