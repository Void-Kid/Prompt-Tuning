# OpenAI Prompt Guidance

## Prompt Implications

- Prefer outcome-first prompts with clear success criteria.
- Re-evaluate legacy step-by-step prompts when using current reasoning models.
- Use developer instructions for durable behavior and user messages for task data.
- Follow instruction hierarchy and chain-of-command boundaries from Model Spec.

## Tool And Structured Output Implications

- Prefer Structured Outputs for parseable JSON and schema-constrained responses.
- Write tool descriptions as contracts with use conditions, inputs, side effects, and returns.
- Reduce tool surface complexity before adding longer tool instructions.

## Reasoning/Thinking State

- In Responses/tool-loop flows, preserve reasoning items when the API requires replaying previous reasoning/tool state.
- Use reasoning effort and verbosity controls when available instead of asking for visible chain of thought.

## Staleness Risk

- Version-specific GPT-5.x guidance, Responses API behavior, reasoning controls, and model limits are volatile. Verify official docs when the user asks for latest/current behavior.

## 2026-06-16 Intervention Notes

- Current prompt guidance favors shorter outcome-first prompts over legacy process-heavy prompt stacks.
- For tool-heavy Responses flows, inspect assistant-item replay, preamble, phase, reasoning items, and tool state before rewriting prompt wording.
- Use Structured Outputs for reliable type and JSON shape when the target API supports it.
- Use function descriptions as contracts: clear names, when-to-use rules, inputs, side effects, return shape, and edge cases.
- Verify official docs for current/latest GPT behavior before making version-specific claims.
