# Anthropic Prompt Guidance

## Prompt Implications

- Define success criteria and tests before making prompt changes.
- Use clear task framing, representative examples, and XML-style tags when they make boundaries easier to parse.
- Keep prompts direct. Do not solve missing evaluation or tool design with longer prose.
- For Claude agent prompts, describe decisions, required actions, optional actions, and quality standards explicitly.

## Tool And Structured Output Implications

- Treat tool definitions like prompts: clear names, precise descriptions, input contracts, and useful returns.
- For large tool sets, reduce visible tools, group by namespace, or defer tool discovery.
- Use structured outputs or tool-mediated validation when strict shape matters.

## Reasoning/Thinking State

- Current Claude models may use adaptive or extended thinking depending on model/API. Prompt for concise summaries or decision criteria when needed, not raw hidden reasoning.

## Staleness Risk

- Claude model names, thinking controls, context windows, and tool behavior change. Verify official docs when the user asks about latest/current model behavior.

## 2026-06-16 Intervention Notes

- Treat agent prompt work as context engineering: system instructions, tools, MCP resources, external data, message history, memory, and runtime state all affect behavior.
- Optimize context utility against constraints such as cost, latency, attention, tool availability, and verification.
- Anthropic tools for agents guidance treats tool definitions and tool surface quality as core to effective agent behavior.
- When a Claude agent fails, inspect tool names, descriptions, schemas, return shapes, and context curation before adding longer prompt wording.
