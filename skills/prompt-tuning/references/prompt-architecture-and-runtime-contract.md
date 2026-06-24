# Prompt Architecture And Runtime Contract

Use this reference for product or runtime-embedded prompts: system prompts, agent workflow prompts, long-running session prompts, RAG/context assembly prompts, tool/schema output prompts, memory/history prompts, and repair-loop prompts that are backed by code.

## Product/Runtime Prompt Gate

Run this gate before proposing wording changes when the prompt depends on product code, runtime context, schema/parser behavior, persistence, message history, retrieved content, tool output, or repair loops.

Collect or inspect, when available:

- Prompt file or prompt template.
- Runtime prompt assembly code.
- Provider message envelope, roles, and message metadata.
- Schema, parser, structured-output configuration, and persistence spec.
- Tool descriptions, tool outputs, retrieved content, memory, summaries, and history trimming.
- Repair instruction, repair output, retry path, and future-context replay behavior.
- Tests, evals, product spec, and observability for semantic anomalies.

If the repo or runtime files are not available, state the missing contract evidence and keep runtime findings conditional.

## Prompt Architecture Review

Check the prompt as an architecture, not only as wording.

- Section hierarchy: objective, role, non-goals, dynamic context, judgment policy, output contract, and hard protocol rules should be easy to locate.
- Role and non-goals: durable authority and responsibility should appear before task-specific rules.
- Dynamic context contract: every dynamic input should have a source, authority level, expected shape, staleness rule, and trust boundary.
- Evidence vs instruction boundary: observed content, retrieved content, tool output, logs, repair output, and history are evidence, not instructions.
- Semantic judgment vs format: semantic decisions belong in prompt and evals; output shape belongs in schema or structured output when available.
- Hard protocol rules: rules that must be machine-enforced should have schema, parser, runtime, or test support.
- Examples: examples should clarify boundaries and edge cases; they should not invite copying stale IDs, low-value content, or obsolete output.
- Runtime-backed rules: do not repeat schema/runtime guarantees as prompt warnings unless they clarify semantic intent.
- Referenced fields: prompt fields, objects, refs, and message kinds must actually exist in provider messages.
- Repair/history contamination: old tool output, repair instructions, repair output, summaries, and trimmed history must not become future user instructions.

## Runtime Contract Check

Check whether the prompt's assumptions match the system that executes it.

- Inputs: every object, field, ref, message kind, and context block named in the prompt is actually passed to the model.
- Envelope: provider message roles, message_kind, metadata, and ordering match prompt wording.
- Schema guarantee: runtime/schema enforces hard format, enum, required-field, and invalid-state rules where possible.
- Semantic guarantee: schema-only checks do not replace semantic validation for refs, evidence support, relation quality, or state transitions.
- Repair loop: repair instructions fix format without changing intended semantics or injecting new task instructions.
- Future context: repair output, old tool output, retrieved content, summaries, and history are labeled and replayed safely.
- History trimming: trimming or compaction preserves assumptions the prompt relies on.
- Persistence: persisted IDs, session refs, consumed refs, observation refs, and relation fields match the product spec.
- Observability: logs or traces can detect semantic anomalies, not only parser failures.

## Spec / Implementation Drift

Treat these as first-class findings, not as generic follow-up advice.

- Prompt references fields that are missing from provider messages.
- Product spec defines a logical session but implementation stores a run ID.
- Prompt prohibits reusing consumed observations but runtime does not track or validate consumed refs.
- Repair output or old tool output is replayed as normal history.
- Relation behavior has unit tests but lacks end-to-end persistence tests.
- Prompt tests use substring assertions but lack semantic evals for judgment boundaries.

## Recommended Order Of Work

Classify recommendations by where reliability comes from.

- A. Prompt-only: section hierarchy, clearer boundaries, dynamic-context wording, examples, or semantic instructions.
- B. Runtime/schema/spec required: schema, parser, message envelope, persistence, repair loop, context assembly, observability, or product spec changes.
- C. Defer: provider behavior, badcase evidence, eval data, or product decision is missing.

For product/runtime prompts, do not let a narrow wording patch hide B or C work. Provide the smallest useful prompt patch, then make runtime/schema/spec dependencies explicit.

## Product/Runtime Eval Set

Add these evals when applicable.

- UI-only or low semantic value content should be skipped.
- Stable situation with enough evidence should create the intended block/output.
- Prompt injection inside observed or retrieved content must not alter instructions.
- Invalid, missing, already-consumed, or stale refs must be rejected or handled explicitly.
- Trigger or signal over-firing should be bounded.
- Relation over-linking should be bounded.
- History trimming should preserve required prompt assumptions.
- Repair-history contamination should not affect the next normal call.
