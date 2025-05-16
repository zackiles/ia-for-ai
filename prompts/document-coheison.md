# Final Cohesion and Precision Review

Ensure a technical document, such as an RFC or an ADR, is internally consistent, terminologically precise, and publication-ready.

* **Role**: Expert systems-architect reviewer
* **Model**: o3, Gemini 2.5 (large context window preferred) 

## Use Cases

* Final review of technical documents or design-doc validation before publication
* Long technical document consistency checks
* Pre-merge architectural reviews

## Inputs

* `@document`: latest RFC markdown file
* `@document` (optional): markdown & code standards
* Tool access: `grep`, file split, vector search

## Prompt

````markdown
## Final Cohesion + Precision Review of Technical Document

**Role**  
You act as expert systems-architect reviewer, specializing in technical writing.

**Objective**  
Check the RFC for unified concepts, exact terms, accurate design flow.

**Plan (write before work)**  
1 List sections to scan.  
2 Note tools to call (`grep`, split, vector-search).  
3 Set tags for pulled text `[Sec#:Line#-#]`.

### 1 Global Concept Consistency  
* Read every section fast.  
* Flag mismatched concepts, redefine once.  
* Track ripple effects; update linked parts.

### 2 Code Snippet Alignment  
* Skim each block.  
* Verify logic fits revised model.  
* Suggest tight edits or inline notes.

### 3 Terminology + Clarity  
* Build single glossary as you read.  
* Replace synonyms with canon term.  
* Shorten fuzzy phrases.

### 4 Formatting + Editorial  
* Fix markdown headers, lists, fences.  
* Remove typos, split run-ons, align style.

### 5 Integration Points  
* Trace component talks.  
* Confirm state flow, external calls, error paths.  
* Cite exact lines for each check.

### 6 Tool-Guided Retrieval  
* When context > window, issue targeted queries.  
* Tag all returns `[Tag]`; reuse tags in reasoning.  
* Never load full doc at once.

### 7 Stepwise Reasoning  
* For each task:  
  1 Restate question.  
  2 Pull tagged evidence.  
  3 Think in numbered steps.  
* After sections, merge insights.

### 8 Consistency + Reference Tracking  
* Quote source lines with tags beside claims.  
* If info missing, write “not found”.  
* Resolve term collisions.

### 9 Output Form  
* Markdown, mirrors doc structure.  
* Bullet brevity; short clauses.  
* Final summary: list confirmed areas ➜ list issues.

**Deliverables**  
* Diff patch files.  
* Review report with tags, evidence, fixes.

**Research Note**  
2025 studies show tagged retrieval + stepwise analysis boosts long-context accuracy; apply throughout.
````

## Output Format

* `diff`: unified diff blocks
* `report`: markdown with headers

  * *Confirmed*
  * *Issues* (each with tag references)

## Example Output

```diff
--- rfc.md
+++ rfc.md
@@ Section 3, Line 12-16 @@
- The worker spawns child agents asynchronously.
+ The worker forks child agents concurrently (see §2.3).
```

```markdown
### Confirmed
* All core terms match glossary.  
* State diagram lines 45-60 align with §4 text.

### Issues
1 Agent fork term mismatch `[Sec3:12-16]` ↔ `[Sec2:30-33]`.  
2 Missing error path description for HTTP 503 `[Sec5:22-28]`.

### Next Steps
* Apply patch; add HTTP 503 flow diagram.  
* Re-run review on updated file.
```
