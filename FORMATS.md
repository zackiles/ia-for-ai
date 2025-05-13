# Formats for Structured Exchange of Graphs
This document compares three structured data formats to express graphs—S-expr, JSONL, and NDJSON—focusing on their use in information architecture, agentic systems, and LLM workflows. Use it to choose the right format for symbolic reasoning, data streaming, or large-scale structured integration based on your system’s needs.

## S-expr

S-expressions (symbolic expressions) represent data as nested lists.
You use them primarily for symbolic data, recursive structures, and deterministic logic.

### Syntax and structure

S-expressions use parentheses for hierarchy and whitespace for token separation.

Example:

```lisp
(action move (from blockA) (to blockB))
```

### Primary use cases

| Use case                        | Suitability | Reason                            |
| ------------------------------- | ----------- | --------------------------------- |
| Deterministic planning          | High        | Simple syntax, clear actions      |
| Symbolic grammar representation | High        | Recursive structure easy to parse |
| Formal rule-based systems       | High        | Ideal for rule definitions        |

### Strengths and limitations

| Strengths                            | Limitations                  |
| ------------------------------------ | ---------------------------- |
| Easy to parse recursively            | Limited enterprise adoption  |
| Compact symbolic notation            | Poor streaming support       |
| Clear representation of nested logic | Requires specialized parsers |

### Enterprise adoption

Few enterprises adopt S-expressions directly.
Use typically occurs in Lisp systems, symbolic planners, or niche tooling.

### Agentic systems

Rarely found in modern agentic systems.
Consider using them only if your system explicitly requires symbolic planning or logic reasoning.

### RAG integrations

Rarely integrated directly into retrieval-augmented generation (RAG) stacks.
Convert S-expressions into JSONL or NDJSON for compatibility.

---

## JSONL

JSON Lines (JSONL) is a newline-delimited format of JSON objects.
You use JSONL widely for streaming structured data and integrations.

### Syntax and structure

Each JSON object appears on a single line, separated by a newline.

Example:

```json
{"action": "move", "from": "blockA", "to": "blockB"}
```

### Primary use cases

| Use case                             | Suitability | Reason                               |
| ------------------------------------ | ----------- | ------------------------------------ |
| Streaming structured data            | Very high   | Easy line-by-line parsing            |
| RAG pipelines                        | Very high   | Directly integrates into data stores |
| LLM prompt and dataset serialization | Very high   | Widely accepted benchmark format     |

### Strengths and limitations

| Strengths                                | Limitations                            |
| ---------------------------------------- | -------------------------------------- |
| Ubiquitous enterprise support            | Verbose compared to symbolic formats   |
| Streamable, easy incremental parsing     | Less elegant for deeply nested data    |
| Highly interoperable and well-documented | Requires full parsing for nested logic |

### Enterprise adoption

Widely adopted by major cloud platforms, including AWS, Azure, and Google Cloud.
Commonly used for logs, event streams, and data ingestion pipelines.

### Agentic systems

Dominant format in modern agentic tools.
Use JSONL for agent action logs, observations, and function-call outputs.

### RAG integrations

Native support in RAG frameworks (LangChain, LlamaIndex).
Use JSONL to store document chunks, metadata, and embeddings.

---

## NDJSON

Newline-delimited JSON (NDJSON) standardizes JSONL with the MIME type `application/x-ndjson`.
You use NDJSON similarly to JSONL but in streaming and logging contexts.

### Syntax and structure

Identical to JSONL in structure but explicitly standardized for streaming APIs.

Example:

```json
{"event": "move", "from": "blockA", "to": "blockB"}
```

### Primary use cases

| Use case                          | Suitability | Reason                              |
| --------------------------------- | ----------- | ----------------------------------- |
| Streaming APIs                    | Very high   | MIME type explicitly supported      |
| Structured logs and observability | Very high   | Integrates directly into log stores |
| Bulk data ingestion               | High        | Preferred format for bulk uploads   |

### Strengths and limitations

| Strengths                                  | Limitations                          |
| ------------------------------------------ | ------------------------------------ |
| Explicit MIME type support                 | Slightly verbose for small data      |
| Ideal for real-time structured logging     | Less common than JSONL               |
| Easy interoperability with logging systems | Needs additional parsing for nesting |

### Enterprise adoption

Commonly used in log aggregation systems (Elasticsearch, Splunk, Logstash).
Supported as a standard streaming format by many enterprise data tools.

### Agentic systems

Increasingly adopted for structured event logs from agentic pipelines.
Use NDJSON if your agents rely heavily on streaming structured data to observability tools.

### RAG integrations

Directly compatible with most JSONL tools in RAG stacks.
Use NDJSON primarily for high-scale ingestion or structured logging alongside RAG operations.

---

## Summary comparison

| Criterion                | S-expr   | JSONL      | NDJSON     |
| ------------------------ | -------- | ---------- | ---------- |
| Enterprise adoption      | Low      | Very high  | High       |
| Agentic systems          | Low      | Very high  | High       |
| RAG integration          | Low      | Very high  | High       |
| LLM research usage       | Medium   | Very high  | High       |
| Information architecture | Symbolic | Structured | Structured |

### Recommendations for use

* Use **S-expressions** when your system explicitly involves symbolic logic, grammar, or recursion-heavy operations.
* Adopt **JSONL** universally in general RAG, agentic systems, and structured data exchange due to broad interoperability.
* Choose **NDJSON** specifically if streaming data or structured logging with formal MIME type standardization is required.
