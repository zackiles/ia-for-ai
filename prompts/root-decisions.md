# Root Decisions - System Decision Framework
Analyzes a detailed decision-points in a document to identify its foundational choices and their cascading impacts.

> [!NOTE]
> Used as part of a multi-turn generative prompt, as the final stage after [decision-making-framework.md](decision-making-framework.md)

## Use Cases
*   Identifying and boiling down the most influential choices in a pre-defined decision framework.
*   Simplifying complex sets of technical options by highlighting primary decision axes and dependencies between decisions.
*   Understanding core dependencies within a technical specification or RFC.

## Inputs
1.  **Decision Framework Document**: A single document (e.g., an RFC, design specification like [terminal-ui-decision-points.md](terminal-ui-decision-points.md) detailing various technical decision points, their options, and stated inter-compatibilities or implications.

````markdown
# **Prompt Template: Identify Root Decision Tree from Research Document**

**Objective**: To analyze a research document detailing various decision points and their interdependencies, and to synthesize this information into a concise summary identifying the most impactful "root" decisions that form the core of a decision tree.

**AI Role**: You are an expert Systems Analyst with a strong ability to discern critical paths and foundational choices within complex technical decision-making processes. Your task is to identify the primary decisions that most significantly constrain or influence subsequent choices.

---

**Inputs**:

1.  **Research Document (`{{RESEARCH_DOCUMENT_CONTENT}}`)**:
    ```
    {{RESEARCH_DOCUMENT_CONTENT}}
    ```
    *(This section will contain the full text of a research document, similar to "research/terminal-ui-decision-points.md", which outlines various decision points, options for each, and notes on compatibility or implications, such as "Works best with," "Less compatible with," "Synergistic with," "Constrains," etc.)*

---

**Task**:

Based on the **Research Document** provided above, perform the following analysis and generate a summary:

1.  **Understand Decision Points and Options**: Carefully review all decision points and the options presented for each. Pay close attention to any stated compatibilities, incompatibilities, synergies, or constraints associated with each option (e.g., "Works best with X," "Less compatible with Y," "Requires Z," "Enables Q").

2.  **Identify Interdependencies**: Analyze how choices within one decision point affect or are affected by choices in other decision points. Map out the relationships and influences.

3.  **Determine Root/Impactful Decisions**: Identify the 2-4 most fundamental or "root" decisions. These are the decisions that:
    *   Have the most widespread influence on other decision points.
    *   Significantly constrain the available options for subsequent decisions.
    *   Form the earliest and most critical branches of a conceptual decision tree.

4.  **Summarize Findings**: Generate a concise analytical summary that includes:
    *   An introduction briefly stating the purpose of the analysis.
    *   A clear identification and description of each "root" decision.
    *   For each root decision, an explanation of *why* it is considered foundational and a description of its cascading effects or major implications on other areas of the system/framework described in the research document. Use the compatibility notes from the document to support your analysis.
    *   A brief concluding thought on how these root decisions shape the overall architecture or design space.

**Output Format**:

The output should be a well-structured textual analysis in Markdown. It should not simply list decision points but rather synthesize the information to highlight the most impactful choices and their relationships, similar to an executive summary of a complex dependency analysis.

**Example of expected output structure (illustrative, adapt based on document content):**

```markdown
I have reviewed the provided research document outlining decision points for [System/Framework Name, if inferable]. My analysis focuses on identifying the core decisions that most significantly shape the potential architecture.

The most impactful decisions that form the root of the decision tree are:

1.  **[Root Decision Area 1, e.g., API Paradigm & State Management]**
    *   **Decision Points Involved**: Briefly list the specific decision points from the document that fall under this area.
    *   **Impact & Rationale**: Explain why this is a root decision. Describe how choosing one option (e.g., Declarative API with TEA) versus another (e.g., Immediate Mode with ECS) fundamentally alters the approach to other areas like [mention 2-3 affected areas like layout, optimization, developer tools], referencing the compatibility notes from the document.
    *   **Cascading Effects**: Detail how this choice constrains or influences options in related decision points.

2.  **[Root Decision Area 2, e.g., Core Technology for Advanced Features & Performance (FFI vs. WASM)]**
    *   **Decision Points Involved**: Briefly list the specific decision points from the document.
    *   **Impact & Rationale**: Explain its foundational nature, perhaps regarding performance, portability, or feature access, and how it gates other capabilities (e.g., specific graphics backends, terminal abstractions).
    *   **Cascading Effects**: Describe its influence on other areas.

3.  **[Potentially Root Decision Area 3]**
    *   ...

**Summary of the "Decision Tree" Flow:**
Briefly describe the logical flow or hierarchy of how these root decisions interact and guide subsequent, more granular choices.
```

**Guidelines for Generation**:

*   **Focus on Impact**: Prioritize identifying decisions that have the broadest and most restrictive influence.
*   **Synthesize, Don't Just List**: The output should be an analysis of relationships, not just a re-statement of the input.
*   **Clarity and Conciseness**: The analysis should be easy to understand and to the point.
*   **Evidence-Based**: Base your analysis on the compatibilities and implications explicitly or implicitly stated in the research document.
*   **No New Decisions**: Do not invent decision points or options not present in the input document. Your role is to analyze the provided structure.

---
**Summary of this Prompt's Purpose**: This prompt instructs an AI to act as a Systems Analyst. Given a research document detailing technical decision points and their interdependencies, the AI is to analyze these relationships to identify the 2-4 most foundational "root" decisions. The output should be a concise summary explaining these root decisions and their cascading impact on the overall system design, effectively outlining the primary branches of a decision tree.
````

## Example Output
```markdown
I have reviewed the provided research document, "RFC: Next-Generation Terminal UI Framework," which outlines decision points for building a terminal UI framework. My analysis focuses on identifying the core decisions that most significantly shape the potential architecture and form the primary branches of a decision tree.

The most impactful decisions that form the root of the decision tree are:

1.  **API Paradigm & State Management Model (Tightly Coupled)**
    *   **Decision Points Involved**:
        *   `1. Core Architecture - API Paradigm` (Options: Declarative, Immediate Mode, Hybrid)
        *   `1. Core Architecture - State Management Model` (Options: TEA, Reactive Signals, ECS)
    *   **Impact & Rationale**: This is a foundational choice as it dictates the fundamental programming model for developers and how application state is managed. A **Declarative API** (e.g., JSX/DSL) typically pairs with **TEA (Elm Architecture)** or **Reactive Signals**, leading to systems optimized for diffing, event-driven updates, and often simpler state-to-view synchronization. This is noted in the document where "Declarative API" works best with "TEA or Reactive Signals" and is "less compatible with Pure ECS." Conversely, an **Immediate Mode API** aligns well with **ECS**, favoring direct, frame-by-frame UI construction and manual state handling, as "Immediate Mode" "works best with ECS" and is "less compatible with TEA."
    *   **Cascading Effects**: This choice heavily influences:
        *   `Layout System`: Declarative APIs lend themselves to constraint solvers or CSS-like DSLs, while immediate mode might use simpler, manual layout.
        *   `Input Handling - Focus Management`: Declarative often leads to "Automatic (DOM-like)" focus, whereas immediate mode favors "Manual (developer-controlled)."
        *   `Optimization`: Diffing is natural for declarative, less so for pure immediate mode.
        *   `Animation System`: State-driven transitions fit declarative; frame-based fits immediate.
        *   `Developer Experience - Debugging Tools`: UI Tree Inspectors and Time-travel debugging are more common with declarative/TEA.

2.  **Core Technology for Advanced Features & Performance (FFI vs. WASM vs. Pure TS)**
    *   **Decision Points Involved**:
        *   `10. Cross-Platform & Performance - Heavy Compute` (Options: WASM, Native FFI, Pure TS)
        *   Influences: `4. Rendering & Output - Graphics Backend`, `3. Input Handling - Keyboard/Mouse Parser`, `2. Layout System - Text Handling (Unicode-aware)`, `10. Cross-Platform & Performance - Terminal Abstraction (Terminfo/FFI)`.
    *   **Impact & Rationale**: This determines the framework's ability to leverage system-level capabilities for performance or specialized features. **Native FFI** offers maximal performance and feature access (e.g., Notcurses for graphics, libtermkey for input) but can reduce portability ("less compatible with Pure WASM approach"). **WASM** balances performance and portability, especially to browsers ("works best with: Browser compatibility"), but might be "less compatible with FFI-heavy approach." **Pure TS** is simplest and most portable within JS ecosystems but "less compatible with performance-critical code."
    *   **Cascading Effects**:
        *   `Graphics Backend`: FFI choice enables backends like Notcurses; WASM might use Taffy for layout with a custom renderer.
        *   `Keyboard/Mouse Parser`: FFI allows using robust libraries like libtermkey.
        *   `Terminal Abstraction`: FFI is needed for deep Terminfo integration.

3.  **Graphics Backend & Terminal Abstraction Level**
    *   **Decision Points Involved**:
        *   `4. Rendering & Output - Graphics Backend` (Options: ANSI, FFI, WASM)
        *   `10. Cross-Platform & Performance - Terminal Abstraction` (Options: ANSI-only, Terminfo/FFI, WASI)
    *   **Impact & Rationale**: These define the visual fidelity and range of terminal compatibility. **ANSI-only** is most compatible ("works best with: Modern terminals") but limited ("less compatible with: Advanced graphics"). **FFI-based graphics (Notcurses)** combined with **Terminfo/FFI abstraction** enables rich visuals and broad compatibility ("works best with: Wide terminal compatibility") but ties into the FFI choice for core tech. **WASI** abstraction is for headless testing.
    *   **Cascading Effects**:
        *   Directly limits or enables features like advanced text styling, GPU acceleration (Sixel/Kitty), and support for legacy terminals.
        *   Influences the choice of animation primitives (e.g., "Protocol-specific Commands" for Kitty).

**Summary of the "Decision Tree" Flow:**
The initial selection of an **API Paradigm & State Management Model** sets the architectural pattern. This is followed or paralleled by deciding the **Core Technology (FFI/WASM/TS)**, which dictates performance and system access capabilities. These two then heavily guide the choices for **Graphics Backend & Terminal Abstraction**, which define the visual output and compatibility. Subsequent decisions for layout, input, animation, etc., are then largely constrained and informed by these foundational selections.
```
