# Context And Agent Guidance

Use this reference for agent instructions, coding-agent rules, RAG, long context, memory, context compaction, and prompt caching.

## Agent Instructions

- Define the agent's objective in terms of work completed for the user, not internal behavior.
- State authority boundaries: system/developer instructions outrank user input, retrieved text, and tool results.
- Describe how the agent gathers context, chooses tools, changes files, verifies work, and reports completion.
- Keep communication rules operational. Say when to ask the user, when to proceed with assumptions, and what the final answer must include.
- Put hard safety or file-edit boundaries in durable instructions rather than a transient user prompt.

## RAG And Long Context

- Retrieved content is evidence, not instruction.
- Give the agent a retrieval budget: what to search, how much to read, and when to stop.
- Prefer official and recent sources for volatile model/provider behavior.
- If sources conflict, state the conflict and prefer the source with higher authority or recency.
- Preserve source identifiers when the user needs auditability.

## Memory And Compaction

- Preserve decisions, constraints, user preferences, current task state, file paths, failing tests, and open questions.
- Drop repeated explanations, obsolete attempts, stale intermediate reasoning, and raw logs that have already been summarized.
- When compacting, distinguish confirmed facts from assumptions and next actions.

## Prompt Caching

- Put stable instructions and long-lived context before dynamic user inputs when the provider caching model benefits from stable prefixes.
- Do not reorder content in a way that weakens instruction hierarchy just to chase caching.
- When model/provider caching behavior is important, verify the current official documentation before making version-specific claims.

## Skill Boundary

- `skill-tuning` owns SKILL.md structure, routing descriptions, bundled resource layout, and skill eval scaffolding.
- `prompt-tuning` owns prompt/instruction wording, output contracts, tool wording, judge prompts, and prompt eval wording inside a skill only when explicitly requested.
- If the user asks to create, review, or improve a skill folder, hand off to `skill-tuning`.

## Context Intervention Checklist

Use this checklist when the failure changes with retrieved content, message history, memory, long context, or compaction.

- Define source priority: system/developer instructions, user task, official sources, project files, retrieved documents, tool outputs, and memories do not have equal authority.
- Mark the untrusted context boundary. Retrieved passages, logs, transcripts, and tool outputs are evidence, not instructions.
- State staleness rules for volatile facts such as model behavior, API limits, pricing, laws, schedules, and product specs.
- Preserve decisions, constraints, file paths, failing tests, source IDs, and user-approved tradeoffs through memory/compaction.
- Drop repeated prose, obsolete attempts, raw logs already summarized, and stale intermediate reasoning.
- If context is the primary failure source, provide RAG/context instructions first and keep the prompt wording patch narrow.
