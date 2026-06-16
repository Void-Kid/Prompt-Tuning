# Tool Description Contract

Use for function/tool descriptions and tool schemas. A good tool description tells the model when to call the tool, when not to call it, what arguments are valid, and what consequences the call has. Keep wording operational rather than promotional. If the model repeatedly chooses the wrong tool, audit the tool surface before adding more instructions, because overlapping tools and loose schemas often cause the failure.

Tool purpose:
- What the tool does in one operational sentence.

Use when:
- The exact conditions that should trigger this tool.
- Observable cues in the user request, conversation state, or runtime state.

Do not use when:
- Adjacent tasks that should use another tool or no tool.
- The model lacks required inputs and must ask, infer from code-owned state, or use a safer read-only tool first.

Inputs:
- Required fields, valid ranges, enums, and defaults.
- Mark code-known parameters that should be filled by code, not the model.
- Prefer schemas that make invalid states impossible instead of relying only on prose.

Side effects and idempotency:
- Whether the tool reads, writes, sends, deletes, bills, or triggers external action.
- Whether retrying is safe.

Returns:
- The shortest useful success shape.
- Error shape and retry guidance.
- Keep return fields token-efficient while preserving the identifiers and status details the model needs for the next step.

Tool surface audit:
- Is this tool always called with another tool? Merge if yes.
- Should it be hidden behind deferred tool search?
- Does the namespace distinguish domain and capability?
- Are invalid states impossible in the schema?

Intervention note:
- Treat this as a tool/schema contract, not only a wording task.
- Put hard guarantees in schema fields, enums, required parameters, invalid-state prevention, and return shapes when possible.
- Use prompt wording for semantic intent, fallback decisions, and user-facing judgment that the schema cannot express.
