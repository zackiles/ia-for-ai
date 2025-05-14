# Evaluators for AI

Evaluations are used to provide criteria for which a LLMs can qualify their outputs. They're especially critical in multi-turn or agentic workflows where maintaining coherence is difficult without a static set of qualifiers the LLM can use to evaluate its outcomes. They're the "test-suites for AI" and arguably play a larger role in guiding deterministic outcomes than the prompt that started the turn.

## What They Look Like

Anything an agent can access can be used to evaluate output. Software engineering orginizations typically adopting agentic workflows typically fall into three levels of increasing complexity.

### Level 1 – Prompted Executors (Individual Use)

Agents operate as stateless assistants invoked via imperative prompts. They execute tightly scoped tasks like:

> “Implement the function. Run the test suite. Fix any errors. Don’t respond until all tests pass.”

There is no memory, role coordination, or interaction between agents. The entire context is encoded in the prompt, and the agent behaves like an intelligent script running in a tight loop.

- Usage is local to the developer’s IDE (e.g., Copilot, Cursor)
- Prompts drive implementation, validation, and retries
- No persistent logs, no planning, no agent-to-agent handoff

Organizations at this level are in an experimentation phase. Adoption is bottom-up, driven by individual productivity gains rather than system-wide integration.

---

### Level 2 – Role-Based Critique (Team-Aware)

Agents are given explicit roles—implementer, reviewer, tester—and interact in structured feedback loops. One agent creates an artifact, another evaluates it, possibly using a test suite, coding standard, or quality rubric. The result is either approval or a rejection with instructions for revision.

> Implementer submits code → Critic reviews output → Implementer refines → Verifier runs tests → Loop until acceptance.

This introduces:

- Defined agent roles with clear responsibilities
- Multi-agent collaboration using structured prompts
- Lightweight memory across steps, such as recent diffs or feedback summaries

Organizations at this level pilot team-level workflows with agent checkpoints, validation stages, and retry logic. Agents begin to simulate internal software engineering rituals like code review and QA.

---

### Level 3 – Autonomous Collaboration (Org-Integrated)

Agents function as a coordinated system handling end-to-end workflows. A planner agent interprets goals or tickets, decomposes them into tasks, assigns them to implementers, and routes outputs to evaluators. Failures trigger replanning or escalation. Shared memory allows agents to retain logs, diffs, feedback, and state across turns.

> Planner breaks down ticket → Implementers generate code → Critics evaluate → Retry on failure → Integrator merges or files PR.

This level includes:

- Multi-role agent systems with dynamic task routing
- Long-lived shared memory (e.g., changelogs, CI output, ticket metadata)
- Integration with organizational systems (version control, CI/CD, ticketing)

Organizations here treat agents as autonomous collaborators, not just tools. Infrastructure supports continuous execution, visibility, and agent-level accountability across the development lifecycle.
