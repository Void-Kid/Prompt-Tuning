# Migration Playbook

Use this reference when moving prompts from old models, old prompt stacks, or prompt-only workflows to current reasoning and agentic model workflows.

## Delete

- Delete duplicated, conflicting, and process-heavy legacy instructions.
- Remove repeated role statements that do not change behavior.
- Remove hardcoded chain-of-thought requests unless the target API and product explicitly need visible reasoning.
- Remove prompt-only JSON guarantees when structured output is available.

## Move To API Or Tool Layer

- Move output schemas to structured output APIs when possible.
- Move tool-use rules into tool descriptions and schema.
- Move code-known defaults and identifiers out of model-filled parameters.
- Move retrieval and freshness policy into context orchestration when prompt text cannot enforce it reliably.

## Replace

- Replace visible CoT requests with reasoning effort, thinking level, concise planning, or hidden reasoning controls.
- Replace large few-shot blocks with the smallest representative examples that cover format, style, and boundary cases.
- Replace broad "be careful" instructions with measurable success criteria and eval cases.

## Retest

- Retest temperature, reasoning effort, verbosity, max tokens, context ordering, prompt caching, and parser behavior.
- Retest tool choice with adjacent tools and tool errors.
- Retest structured output with malformed, ambiguous, and long inputs.
- Compare baseline and optimized behavior before treating the migration as complete.

## Multi-Turn Tool Migration

- For multi-turn tool + structured-output migration, inspect prompt text, tool schema, message replay, reasoning/thinking artifacts, and parser.
- Confirm provider-specific state rules before replaying or stripping reasoning artifacts.
- Add a regression case for the exact failure that appeared during migration.

## Intervention Migration Order

When migrating a legacy prompt stack, do not copy the old stack directly. Move in this order:

1. Preserve the user-visible objective and success criteria.
2. Remove duplicated, conflicting, and process-heavy legacy prompt stack instructions.
3. Move output shape to structured output or schema where the target runtime supports it.
4. Move tool rules into tool descriptions and schemas.
5. Define context/RAG, memory/compaction, and source priority outside transient user prompt text.
6. Replace visible chain-of-thought instructions with provider reasoning controls or concise planning rules.
7. Check provider state requirements for reasoning items, thought signatures, `reasoning_content`, thinking mode, parser behavior, and tool-loop replay.
8. Add regression evals for failures observed in the source runtime and the target runtime.

If provider state is the primary migration risk, the prompt patch should be small and the runtime instructions should carry the main fix.
