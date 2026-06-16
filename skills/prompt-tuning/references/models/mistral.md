# Mistral Prompt Guidance

## Prompt Implications

- State task, context, constraints, and output format clearly.
- Use examples when output style or classification boundary is hard to describe.
- Expect model updates to change prompt behavior; keep evals close to important prompt changes.

## Tool And Structured Output Implications

- Use structured output when parseable shape matters.
- Describe tool calls with clear trigger conditions, required arguments, and failure handling.
- Do not rely on prompt wording for validation that schema or application code can enforce.

## Reasoning/Thinking State

- For Magistral or reasoning workflows, separate reasoning configuration from prompt wording when the API exposes controls.

## Staleness Risk

- Mistral model lineup, reasoning options, and structured-output support can change. Verify official docs for version-specific claims.
