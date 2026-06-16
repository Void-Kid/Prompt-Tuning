# Kimi Prompt Guidance

## Prompt Implications

- Use clear instructions and representative examples for stable output.
- Choose thinking or non-thinking mode based on task complexity, latency, and required reliability.
- For long-horizon agent tasks, keep goals, constraints, current state, and tool results well separated.

## Tool And Structured Output Implications

- Follow Kimi tool-call guidance for multi-step tool invocation.
- Keep tool returns concise and preserve identifiers needed for later steps.
- Avoid prompt-only output-shape guarantees when schema or parser support is available.

## Reasoning/Thinking State

- In Kimi thinking tool-call flows, preserve `reasoning_content` when the API or runtime requires it.
- Treat reasoning continuity as provider state, not as user-editable prompt text.

## Staleness Risk

- Kimi model versions, context windows, agent capabilities, and thinking behavior change quickly. Verify official docs for latest claims.

## 2026-06-16 Intervention Notes

- Kimi K2.6 thinking tool-call flows require preserving `reasoning_content` across multi-step tool calling when the runtime expects it.
- `tool_choice` support is constrained by the current Kimi API behavior; check official docs before assuming OpenAI-compatible values beyond documented options.
- Treat `reasoning_content` as provider state, not as prompt text to edit or summarize.
- If a Kimi migration fails after a tool call, inspect reasoning continuity, tool return shape, parser behavior, and context order before rewriting the prompt.
