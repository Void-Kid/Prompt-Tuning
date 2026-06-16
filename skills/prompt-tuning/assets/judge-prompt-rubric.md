# Judge Prompt Rubric

Use for eval/judge prompts. The judge should grade the behavior being tested, not whether the answer sounds polished. Keep inputs explicit, dimensions observable, and scoring anchors stable across runs. When possible, ask the judge to cite short evidence from the candidate output and mark failed dimensions, so later prompt changes can be compared without rereading every completion.

Judge task:
- Evaluate only the target behavior, not general writing quality.

Inputs:
- `candidate_output`
- `source_input`
- `reference_answer` or `rubric`

Scoring dimensions:
- Correctness: observable match to expected behavior.
- Completeness: required elements present.
- Constraint adherence: forbidden content absent.
- Format validity: output shape is parseable and complete.

Score anchors:
- 5: Fully satisfies all required behavior with no material issue.
- 3: Partially satisfies behavior but misses a required element or has minor unsupported content.
- 1: Fails the main task, violates a hard constraint, or is not parseable.

Output:
- Return a score, short rationale, and failed dimensions.
- Do not reward fluent prose that violates the rubric.
- Do not infer success from intent when the required output is missing.
- Prefer consistent severity over generous partial credit, especially for hard constraints.
