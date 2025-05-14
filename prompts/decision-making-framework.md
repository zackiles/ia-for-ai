# System Design Decision Framework  
Transforms research + problem statements into structured technical decision matrices.  

## Use Cases
Architectural planning, tech evaluations

## Inputs
1. Research data (benchmarks, case studies)  
2. Problem statement (system goals/constraints)  

````markdown

# **Prompt Template: Generate Structured Decision-Making Framework**

**Objective**: To generate a structured decision-making framework for designing or evaluating a software system/component that addresses a specific problem, based on provided research.

**AI Role**: You are an expert System Architect and Research Analyst. Your task is to synthesize provided research materials and a specific problem statement into a comprehensive, actionable decision-making framework. This framework should guide a technical team in making informed choices during the system design or evaluation process.

---

**Inputs**:

1.  **Research Data (`{{RESEARCH_DATA}}`)**:
    ```
    {{RESEARCH_DATA}}
    ```
    *(This section will contain the collated research findings, comparisons of technologies/approaches, articles, case studies, and any other relevant information about the problem space and potential solutions. It might include summaries of multiple documents, studies, research papers,  or raw research notes from the user.)*

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
## **3. Rendering & Output**
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
*   **Structure**: Adhere strictly to the specified output format. Optimize content to interpreted and acted on by an advanced AI agent or LLM.

````

## Example Output

```markdown
### **RFC: Next-Generation Terminal UI Framework**

#### **1. Core Architecture**
- **Decision Points**:
  - **State Management Model**:  
    1. Elm Architecture (TEA)  
       - Works best with: Declarative API, diffing optimization  
       - Less compatible with: Immediate Mode  
    2. Reactive Signals (SolidJS)  
       - Works best with: Fine-grained updates, hybrid API  
       - Less compatible with: Full immediate mode  
    3. Entity-Component-System (ECS)  
       - Works best with: Immediate Mode or Hybrid API  
       - Less compatible with: Pure declarative  

  - **API Paradigm**:  
    1. Declarative (JSX/DSL)  
       - Works best with: TEA or Reactive Signals  
       - Less compatible with: Pure ECS  
    2. Immediate Mode (ImGui-style)  
       - Works best with: ECS  
       - Less compatible with: TEA  
    3. Hybrid (Declarative + Imperative escape hatches)  
       - Compatible with: Any state management approach  

#### **2. Layout System**
- **Decision Points**:
  - **Layout Engine**:  
    1. Constraint Solver (Cassowary)  
       - Works best with: Complex layouts, declarative specification  
       - Less compatible with: Pure immediate mode  
    2. Custom DSL (CSS-like)  
       - Works best with: Declarative API  
       - Less compatible with: Pure immediate mode  
    3. Hybrid (Flexbox + Grid via WASM)  
       - Compatible with: Most API approaches  

  - **Text Handling**:  
    1. Monospace-only  
       - Works best with: Simple ANSI rendering  
       - Less compatible with: Advanced text styling  
    2. Unicode-aware (wrapping/alignment)  
       - Works best with: FFI or advanced rendering backend  
       - Less compatible with: Simple ANSI-only  
    3. GPU-accelerated (via Sixel/Kitty)  
       - Works best with: Advanced rendering backend (Notcurses)  
       - Less compatible with: Simple ANSI-only, headless mode  

#### **3. Input Handling**
- **Decision Points**:
  - **Keyboard/Mouse Parser**:  
    1. Pure TS (ANSI sequences)  
       - Works best with: Cross-platform focus  
       - Less compatible with: Advanced terminal features  
    2. FFI (libtermkey/Notcurses)  
       - Works best with: Other FFI components  
       - Less compatible with: Pure WASM approach  
    3. Hybrid (TS + FFI fallback)  
       - Compatible with: Most architectural choices  

  - **Focus Management**:  
    1. Manual (developer-controlled)  
       - Works best with: Immediate Mode or Hybrid API  
       - Less compatible with: Automatic focus systems  
    2. Automatic (DOM-like)  
       - Works best with: Declarative API  
       - Less compatible with: Pure immediate mode  
    3. Hybrid (z-index + tab order)  
       - Compatible with: Most API approaches  

#### **4. Rendering & Output**
- **Decision Points**:
  - **Graphics Backend**:  
    1. ANSI (Truecolor/256-color)  
       - Works best with: Simple text-focused UI  
       - Less compatible with: Advanced graphics  
    2. FFI (Notcurses/FTXUI)  
       - Works best with: Advanced graphics, other FFI components  
       - Less compatible with: Pure WASM approach  
    3. WASM (Taffy for layout + custom renderer)  
       - Works best with: Other WASM components  
       - Less compatible with: Heavy FFI usage  

  - **Optimization**:  
    1. Double-buffering  
       - Works best with: Any rendering approach  
       - Less compatible with: Minimal memory usage  
    2. Diffing (React-style)  
       - Works best with: Declarative API  
       - Less compatible with: Pure immediate mode  
    3. Terminal-specific (Kitty/Sixel)  
       - Works best with: Advanced graphics backend  
       - Less compatible with: Universal terminal support  

#### **5. Animation System**
- **Decision Points**:
  - **Animation Primitives & Control**:
    1. Frame-based (Timer/requestAnimationFrame-like loop)
       - Works best with: Immediate mode or hybrid where imperative updates are easy.
       - Less compatible with: Purely declarative state-driven updates without side effects.
    2. Event-driven / State-driven Transitions
       - Works best with: Declarative APIs (TEA, Reactive Signals) where state changes trigger animations.
       - Less compatible with: Fine-grained imperative control needed for complex physics.
    3. Protocol-specific Commands (e.g., Kitty animation protocol)
       - Works best with: Terminals supporting advanced graphics protocols.
       - Less compatible with: Universal terminal support, simpler backends.
  - **Easing & Interpolation**:
    1. Built-in Easing Functions (linear, ease-in-out, etc.)
    2. Physics-based (springs, dampers)
    3. Custom Interpolators via API

#### **6. Interactivity & Extensibility**
- **Decision Points**:
  - **Embedded Subprocesses**:  
    1. Deno.Pty  
       - Works best with: Deno-specific features  
       - Less compatible with: WASI  
    2. Custom PTY layer  
       - Works best with: Cross-platform needs  
       - Less compatible with: Simplicity  
    3. None (CLI-only)  
       - Works best with: Simple commands  
       - Less compatible with: Interactive applications  

  - **Remote UI Protocol**:  
    1. JSON-RPC  
       - Works best with: Web interoperability  
       - Less compatible with: Binary optimization  
    2. CRDT (Yjs/Automerge)  
       - Works best with: Collaborative features  
       - Less compatible with: Simple unidirectional flow  
    3. Custom binary (MessagePack)  
       - Works best with: Performance requirements  
       - Less compatible with: Web browser integration  

#### **7. Middleware & Plugin Architecture**
- **Decision Points**:
  - **Extensibility Mechanism**:
    1. Hook-based System (Lifecycle hooks for components/app)
       - Works best with: Both declarative and imperative APIs, allows tapping into various stages.
    2. Pipeline/Stream Processing (for events, state updates)
       - Works best with: Event-driven architectures (TEA, Redux-like).
    3. Component Registry & Mixins
       - Works best with: Declarative, component-based APIs.
  - **Plugin API Surface**:
    1. Access to Core Internals (State, Renderer, Input)
       - More powerful, but harder to maintain API stability.
    2. Restricted API (Specific extension points)
       - Easier to maintain, less powerful.
    3. Message-Passing Interface
       - Decoupled, good for sandboxing.

#### **8. Internationalization & Localization (i18n & l10n)**
- **Decision Points**:
  - **Translation Management**:
    1. Built-in Key-Value System (e.g., JSON/YAML resource files)
       - Works best with: Most application types needing static string translation.
    2. Integration with Standard Libraries (e.g., Intl API via JS runtime)
       - Works best with: Complex formatting needs (dates, numbers, plurals).
    3. No Built-in Support (Developer brings their own solution)
       - Simpler framework core, more work for app developer.
  - **Text Direction & Layout**:
    1. Basic Left-to-Right (LTR) only
    2. Bidirectional Text Support (RTL, e.g., for Arabic, Hebrew)
       - Requires layout engine and text rendering to be BiDi-aware.
    3. Locale-aware Component Variants (e.g., different date pickers)

#### **9. Security Model**
- **Decision Points**:
  - **Subprocess Sandboxing**:
    1. OS-level Sandboxing (if available and controllable)
    2. Permission-based API Access for Subprocesses
       - Requires framework to mediate PTY I/O for filtering.
    3. No Explicit Sandboxing (Relies on OS permissions)
       - Simpler, but higher risk if running untrusted code.
  - **Resource Access Control (Files, Network)**:
    1. Framework-level Permission Prompts/API
       - Works best with: Interactive applications needing user consent.
    2. Static Configuration/Manifest
    3. Rely on Deno/Runtime Permissions
       - Puts onus on how the main app is run.
  - **Input Sanitization & Output Encoding**:
    1. Automatic Sanitization for Known Vulnerabilities (e.g., escape sequence injection)
    2. Developer-controlled Sanitization APIs
    3. None (Developer responsibility)

#### **10. Cross-Platform & Performance**
- **Decision Points**:
  - **Terminal Abstraction**:  
    1. ANSI-only (Xterm baseline)  
       - Works best with: Modern terminals  
       - Less compatible with: Legacy support  
    2. Terminfo/FFI (ncurses)  
       - Works best with: Wide terminal compatibility  
       - Less compatible with: WASI  
    3. WASI (headless testing)  
       - Works best with: Testing focus  
       - Less compatible with: Terminal-specific features  

  - **Heavy Compute**:  
    1. WASM (Rust/C++)  
       - Works best with: Browser compatibility  
       - Less compatible with: FFI-heavy approach  
    2. Native FFI  
       - Works best with: Performance-critical code  
       - Less compatible with: Browser/WASI  
    3. Pure TS (fallback)  
       - Works best with: Simplicity, portability  
       - Less compatible with: Performance-critical code  

#### **11. Developer Experience**
- **Decision Points**:
  - **Debugging Tools**:  
    1. Time-travel (Redux DevTools)  
       - Works best with: TEA or unidirectional flow  
       - Less compatible with: ECS without middleware  
    2. UI Tree Inspector  
       - Works best with: Declarative or hybrid API  
       - Less compatible with: Pure immediate mode  
    3. Terminal Capability Sniffer  
       - Works best with: Terminal abstraction layer  
       - Less compatible with: ANSI-only approach  

  - **Tooling**:  
    1. CLI Scaffolding  
       - Works best with: Any architecture  
    2. Hot Reload  
       - Works best with: Declarative or hybrid API  
       - Less compatible with: Stateful immediate mode  
    3. VS Code Extension  
       - Works best with: Any architecture  

#### **12. Non-Goals**
- Legacy terminal support (pre-VT100).  
- Full GUI emulation (WebView/Electron). 

```
