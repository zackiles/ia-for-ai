# 🧠 WHAM (Weights Handlers Actions and Messages)

WHAM, or a WHAM agent in an agentic system is one that effectively acts as a "Transformer-Decoded Planner + Function Router + Input Resolver in a Recurrent Decision Cycle". In essence, it's the critical orchestration layer in an agentic system.

## Overview

In tool-using LLM systems like OpenAI’s (reported to have an exact system called WHAM), decision-making is modular, interpretable, and stateful. Rather than emitting a final answer in one shot, the agent **iteratively plans, routes, and executes actions**, using its memory and world state to adapt its behavior step-by-step.

This execution loop fuses three primary components:

- 🧭 **Transformer-Decoded Planner** — decides what to do next  
- 🔀 **Function Router** — maps that decision to available tools  
- 🧩 **Input Resolver** — supplies arguments to those tools from memory/context  

Each execution feeds back into the agent’s internal state, forming a **recurrent decision loop**. This allows for sophisticated, context-aware behavior in multi-step reasoning tasks, tool use, simulations, and assistant workflows.

---

## 🔄 Diagram: Recurrent Decision Loop

```mermaid
flowchart TD
  Context[Task + History + Memory] --> Decode[Transformer Planner]
  Decode --> Intent[Intent/Tool Plan]
  Intent --> Router[Function Router]
  Router --> Call[Tool Call Template]
  Call --> Resolver[Input Resolver]
  Resolver --> Execution[Execute Tool]
  Execution --> Observe[Result]
  Observe -->|Append to Context| Context
````

---

## 🧭 1. Transformer-Decoded Planner

### 🔍 What is a Transformer?

A **transformer** is a neural network architecture made of stacked **self-attention layers** that allow a model to read all input tokens at once and compute contextual relationships between them.
There are three major types:

| Type            | Used For                   | Example     |
| --------------- | -------------------------- | ----------- |
| Encoder-only    | Text understanding         | BERT        |
| Decoder-only    | Text generation            | GPT         |
| Encoder-decoder | Translation, summarization | T5, FLAN-T5 |

OpenAI models like GPT-4 use **decoder-only transformers**, which **generate text token-by-token** — this means it produces one piece of text (token) at a time, feeding it back into itself to determine the next. This is different from masked models (like BERT), which predict all missing pieces at once.

### 🧮 Role in Agent Systems

The planner receives structured context:

* Prompt/instructions
* History of actions/results
* Tool availability
* Working memory

It then **decodes** the next action to take, typically in JSON format, by emitting tokens stepwise until a valid structured object is completed.

### 🧠 How It Reasons

The planner uses:

* **Scratchpads**: a visible “thought space” where it writes intermediate logic, hypotheses, or deductions before producing output.
* **Few-shot examples**: samples of previous task→action pairs included in the prompt to condition the model into matching a specific format or behavior. For instance:

  ```
  Q: “Analyze sales.csv and chart top products”
  A: {"tool":"code_interpreter", "args":{"code":"..."}}
  ```

Together, this makes the planner capable of:

* Reflective decision-making
* Tool selection
* Sequencing actions
* Error recovery

---

## 🔀 2. Function Router

Once the planner emits a structured intent like:

```json
{
  "tool_name": "browser_agent",
  "action": "call_tool",
  "reasoning": "We need to fetch the HTML to parse product details."
}
```

…the **Function Router** maps this to a real, callable tool in the runtime environment.

### 🧩 Behavior

* Looks up the `tool_name` in a tool registry.
* Validates if the tool is available.
* Retrieves the tool schema (input/output shape).
* Prepares the next step for argument resolution.

### 🧪 Example

```ts
router.getTool("browser_agent").schema = {
  name: "browser_agent",
  parameters: { url: "string", clickSelector: "string" }
}
```

The tool might be:

* An internal function (e.g., `code_interpreter`)
* A plugin (e.g., `retrieval_agent`, `browser`)
* A remote API service

---

## 🧩 3. Input Resolver

The planner may generate a partially complete action. The **Input Resolver** binds all variables and fills in arguments using the agent’s active memory, prior outputs, user-uploaded files, or environment.

### 🔄 Sources of Truth

* `{{file_name}}` → from uploaded file metadata
* `{{result_from_tool_x}}` → previous tool output
* `{{user.email}}` → structured identity or memory

### 🔧 Example

```json
{
  "tool": "email_agent",
  "args": {
    "to": "{{last_user_email}}",
    "subject": "Here is your data",
    "body": "{{summary_from_code_interpreter}}"
  }
}
```

Input resolution may involve:

* Direct substitution
* Prompt-based filling (ask LLM to guess/complete)
* Validation of types and formats

---

## 🔁 Recurrent Decision Cycle

Each loop produces:

1. **Observation**: tool result, error, message
2. **Append to Context**: saved to memory
3. **Next Decode**: planner chooses next action

This creates:

* Stateful agents
* Plan-and-act capabilities
* Dynamic branching, retries, refinement

---

## 🛠️ Implementation Skeleton (Pseudocode)

```ts
class AgentEngine {
  planner: TransformerPlanner
  router: FunctionRouter
  resolver: InputResolver
  memory: AgentContext

  async act() {
    const intent = await this.planner.plan(this.memory)
    const fn = this.router.getTool(intent.tool_name)
    const args = await this.resolver.resolve(fn.schema, this.memory)
    const result = await fn.invoke(args)
    this.memory.append({ intent, args, result })
  }
}
```

This system can repeat the loop until task success, timeout, or manual interruption.

---

## ✅ Benefits of This Architecture

| Feature          | Value                                                                   |
| ---------------- | ----------------------------------------------------------------------- |
| **Modular**      | Planner, router, resolver can be swapped/upgraded independently         |
| **Explainable**  | Every action is traceable and structured                                |
| **Composable**   | Supports nesting, chaining, retries, and stateful workflows             |
| **LLM-Friendly** | Keeps LLM prompts structured, observable, and interruptible             |
| **Tool-Aware**   | Separates reasoning from execution, making safety and validation easier |

---

## 🧱 Core Architectural Components of WHAM


| Component                              | Function                                                                                        |
| -------------------------------------- | ----------------------------------------------------------------------------------------------- |
| **Rollout Function** (`rollout_fn.py`) | Executes task episodes or simulations; likely performs environment-agent rollout cycles         |
| **Task Spec Parser**                   | Interprets structured instructions or environment definitions                                   |
| **Tool Interface Layer**               | Manages API/tool usage (e.g., invokes code interpreter, browser, etc.)                          |
| **Observation Synthesizer**            | Aggregates input context (e.g., text, state, tool responses) into a unified input for the model |
| **Action Policy**                      | LLM-backed decision engine; outputs tool calls, commands, or messages                           |
| **Memory or State Tracker**            | Tracks current episode/task state, logs intermediate outputs                                    |
| **Execution Monitor**                  | Handles success/failure detection, retries, and loop control                                    |
| **Logging / Telemetry**                | Sends trace data to internal systems like Datadog or Temporal                                   |
| **Temporal Workflow Integration**      | Hooks into OpenAI’s `oai_temporal` system for managing long-running tasks                       |
| **Error Interceptor**                  | Captures stack traces, validation issues, and task execution errors                             |



---

## Final Notes

This architectural pattern is at the heart of modern LLM-based systems like ChatGPT’s code interpreter mode, `wham_agent_v2`, agent simulators, and Auto-GPT-like planning agents. By wrapping LLMs in structured, recurrent, tool-driven loops, these agents go beyond static answers to become **dynamic, reliable, and extensible task solvers**.
