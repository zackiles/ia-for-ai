<!--
Fill in each section below to document and categorize the enclosed prompt.
Use this format as a "prompt wrapper" to ensure clarity and reusability in prompt libraries or agent systems.
-->

# Prompt Template <!-- Title of the Prompt, e.g., "Summarize Technical Document" -->

<!-- What is the high-level goal of this prompt? What should the AI accomplish? -->


* **Role**: <!-- Describe the assumed AI persona or capabilities the prompt invokes (e.g., Expert Reviewer, Data Analyst, Technical Writer). -->
* **Model**:  <!-- Preferred model -->

## Use Cases
<!-- List common scenarios where this prompt would be used, e.g., RFC review, long-form summarization, schema generation. -->

## Inputs
<!-- Enumerate required input types or fields the prompt expects, e.g., "A markdown document", "A list of tasks", "Source code block". -->

## Prompt
````markdown
# Prompt Template: [Insert Prompt Name Here]

## Objective
<!-- Describe the purpose of this prompt in a general and abstract way.
Example: Enable the AI to perform structured classification or transformation of provided inputs according to defined analytical categories. -->

## AI Role
<!-- Define the perspective or function the AI should adopt when executing this prompt.
Example: An expert analyst trained in pattern recognition, data classification, and domain-specific reasoning. -->

---

## Inputs
<!-- List all inputs expected by the prompt, with generic placeholder names and brief descriptions.
Example:
- `input_data`: The raw data or artifact to be analyzed or processed.
- `metadata` (optional): Contextual or supplementary information that informs processing. -->

---

## Task

<!-- Insert the raw prompt here exactly as it's sent to the LLM.
Example:
Analyze the following input_data and classify its components using the specified framework.
1. Identify key patterns or entities.
2. Map features to known categories.
3. Highlight ambiguous or novel items.

Return a structured output using the defined format below.

Input: {input_data}
Metadata: {metadata}
-->

---

## Output Format and Structure
<!-- Describe how the response should be formatted. Be abstract and extensible.
Example:
Return a markdown table with these columns:

| element | classification | confidence | notes | supporting evidence |

Include any additional required formatting like bullet points, headers, or section dividers for summary insights.
-->

---

## Examples
<!-- Provide minimal, domain-agnostic examples of how the prompt works.
Example:

**Input:**
input_data: "alpha, beta, gamma"
metadata: "Category set A"

**Output:**

| element | classification | confidence | notes | supporting evidence |
|---------|----------------|------------|-------|---------------------|
| alpha   | Type-1         | 0.92       | Clear match | in Category A |
| beta    | Type-2         | 0.75       | Ambiguous term | overlaps with Type-1 |
| gamma   | Novel          | 0.40       | Unknown pattern | no precedent found |

**Summary Insights:**
- 2 elements classified with high confidence.
- 1 novel element identified.
- Suggest review of ambiguous category boundary.
-->

---

## Summary
<!-- Recap what the prompt is meant to achieve in flexible terms.
Example: This template supports repeatable analysis of arbitrary inputs across domains, guiding the AI to return structured, interpretable classifications or insights.
-->
`````

## Output Format

<!-- Describe the structure or rules for the expected output (e.g., "JSON list", "Bullet summary", "Markdown table"). -->

## Example Output

<!-- Provide a realistic and formatted sample output generated from the prompt. -->

```
