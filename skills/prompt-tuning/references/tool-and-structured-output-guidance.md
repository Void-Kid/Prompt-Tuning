# Tool And Structured Output Guidance

Use this reference for tool/function descriptions, tool schemas, structured outputs, JSON mode, parser failures, and multi-step tool-call failures.

## Tool Description Contract

- Define use when, do not use when, required inputs, valid enums, side effects, idempotency, return shape, error shape, and retry guidance.
- Mark code-known parameters so the model does not fill values that code already knows.
- Keep tool returns token-efficient and decision-ready.
- Describe failures in a way the agent can act on: retry, ask user, switch tool, or stop.

## Tool Surface Audit

Run this tool surface audit before adding more prompt wording.

- Count visible tools and reduce the initial set when selection quality drops.
- Use deferred tool search when the tool catalog is large.
- Use namespace conventions to distinguish domains and capabilities.
- merge tools that are always called together.
- Make invalid states impossible through schema where possible.
- Test different tool counts with evals when tool selection is unstable.
- Check whether a prompt wording issue is actually a tool surface issue before adding longer instructions.

## Structured Outputs

- Prefer structured outputs or JSON schema over prompt-only formatting promises.
- Put schema guarantees in API configuration when available.
- Use prompt wording for semantic constraints that schema cannot express.
- If a parser fails, inspect the actual model output, hidden reasoning behavior, tool replay state, and provider structured-output rules before rewriting the prompt.

## Provider State Rules

- OpenAI: preserve reasoning items in Responses/tool-loop flows when required by the API.
- Google Gemini: return thought signatures in function-calling conversations that include thinking.
- DeepSeek: for the older reasoner flow, remove `reasoning_content` before the next request when the API requires it.
- Kimi: preserve `reasoning_content` for thinking tool-call flows when required.
- Perplexity: reasoning outputs can include `<think>` before structured output; strip or parse it before JSON validation when the API/model returns it.

## Prompt Patch Pattern

Anti-pattern:
- "Always call the right tool and output JSON."

Patch:
- Put the tool choice rule in the tool description.
- Put the JSON shape in structured output configuration.
- Use prompt text only for semantic intent and fallback behavior.

Minimal eval:
- Case with two adjacent tools.
- Case with invalid schema field.
- Case with tool error and retry decision.

## Non-Prompt Root Cause

Many prompt failures are actually tool/schema contract failures. Treat these as non-prompt root causes when the behavior depends on valid parameters, output shape, parser expectations, tool visibility, or side effects.

- Use hard guarantees when available: structured outputs, JSON schema, enum constraints, required fields, and invalid-state prevention beat repeated prompt warnings.
- Use prompt wording for semantic intent, fallback behavior, and user-facing judgment that schemas cannot express.
- Use tool/schema contract changes for when-to-call rules, do-not-call rules, side effects, idempotency, retry policy, code-known parameters, and return shape.
- If the model calls adjacent tools incorrectly, compare names, namespaces, descriptions, schemas, and visible tool count before changing the system prompt.
- If the parser fails after a tool or reasoning turn, inspect provider state and structured-output rules before adding "return valid JSON" language.
