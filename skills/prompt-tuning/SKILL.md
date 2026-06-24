---
name: prompt-tuning
description: 'Use when the target artifact or failure root cause is LLM prompt or instruction wording, including product/runtime system prompts, agent workflow prompts, and prompts backed by code. Covers prompt creation, review, improvement, migration, debugging, evaluation, agent instructions, tool/function descriptions, structured-output prompts, RAG/context instructions, judge/eval prompts, and prompt templates. Also use for prompt assembly or runtime contract failures when user intent is to change or evaluate a prompt target. Do NOT use for pure schema/parser/runtime debugging without a prompt target, ordinary content writing, code review, product review, creating or tuning agent skills, SKILL.md work, plugin creation, skill installation, general AI education, or full security audits. Triggers include "帮我写 prompt", "优化这个提示词", "评估产品 system prompt", "review this prompt", and "prompt tuning".'
---

# Prompt Tuning

Use this skill to create, review, improve, patch, migrate, debug, and evaluate prompts or prompt-like instructions. The default output is a usable prompt, an applicable prompt patch, or concrete prompt modification advice.

## Workflow

1. Classify the request type: `create`, `review`, `improve`, `migrate`, `debug`, `eval`, or `model-specific`.
2. Identify the target object: `system prompt`, `developer prompt`, `user prompt`, `agent instructions`, `tool description`, `structured-output prompt`, `RAG/context instructions`, `judge prompt`, or `eval prompt`.
3. Identify the target model/provider, runtime, input variables, expected output, failure examples, tool/schema/context constraints, cost constraints, latency constraints, and current/latest/provider-specific claims.
4. Apply the Product/Runtime Prompt Gate when the prompt is embedded in a product pipeline, agent workflow, long-running session, RAG/context assembly, tool/schema output, memory/history flow, persistence path, or repair loop. Skip this gate for standalone pasted prompts without backing code or runtime context. When the gate applies, inspect or request the prompt file, runtime prompt assembly, schema/parser, repair loop, tests, and spec before treating the prompt as isolated text.
5. Diagnose the primary intervention layer before rewriting:
   - `prompt wording`
   - `instruction hierarchy`
   - `prompt architecture`
   - `tool/schema contract`
   - `structured output`
   - `context/RAG`
   - `memory/compaction`
   - `reasoning/provider state`
   - `model params/model choice`
   - `eval gap`
6. Choose the smallest effective intervention. If schema, tool surface, context, provider state, model parameters, runtime contract, persistence, spec drift, repair flow, or evals are the real bottleneck, still provide the smallest useful prompt change and list the required non-prompt change separately.
7. Apply the Freshness Gate for current/latest/provider-specific behavior: use official current sources or a recently checked `references/source-map.md` entry before making model/provider claims.
8. Load only the resources needed by the table below.
9. Produce the prompt, prompt patch, tool description, judge prompt, architecture recommendations, runtime findings, or concrete recommendations before theory.
10. Add minimal eval cases for important changes.
11. Explain user impact, risk, and added complexity briefly.

## Low-Info Requests

- If the user only says "帮我写 prompt" or equivalent with no task goal, ask one key question: what should the model accomplish?
- If the user gives a basic goal but omits model, API, business context, or failure examples, produce a model-agnostic v0 prompt with explicit assumptions and replaceable variables.
- Ask at most one round of 1-3 questions. When a reasonable assumption is possible, draft first.

## Freshness Gate

- If the user asks about current, latest, mainstream-model, or provider-specific behavior, verify against official current sources or a `references/source-map.md` entry checked within the last 30 days.
- Treat PromptingGuide as a technique taxonomy, not as current authority when official provider docs disagree.
- If a provider behavior depends on tool calling, structured outputs, reasoning state, thinking mode, prompt caching, context window, or parser rules, state that dependency in the output.
- If freshness cannot be verified during the task, label the provider-specific recommendation unverified and keep the prompt artifact model-agnostic where possible.

## Resource Loading

| Situation | Load |
| --- | --- |
| Complex review/improve/debug/migration or user asks for rationale | `references/core-principles.md` |
| Diagnosing intervention layer, non-prompt root cause, or smallest effective change | `references/core-principles.md`, then the specific reference for the selected layer |
| Product/runtime system prompt, long-running agent prompt, prompt assembly, schema/parser, persistence, repair loop, history/memory, or spec drift is involved | Load `references/core-principles.md` and `references/prompt-architecture-and-runtime-contract.md` first; then load `references/context-and-agent-guidance.md`, `references/tool-and-structured-output-guidance.md`, or `references/eval-and-optimization-method.md` only when the diagnosed layer requires them |
| Target model/provider is named or migration is requested | `references/models/index.md`, then the relevant provider file |
| Current/latest/provider-specific claims or source freshness checks | `references/source-map.md`, and official provider docs when the source map is stale |
| Agent instructions, RAG, memory, long context, prompt caching, or context compaction | `references/context-and-agent-guidance.md` |
| Tool/function descriptions, structured outputs, JSON mode, schema wording, or tool-call failure | `references/tool-and-structured-output-guidance.md` |
| Prompt evals, judge prompts, failure examples, regression cases, or optimization loops | `references/eval-and-optimization-method.md` |
| Legacy prompt stack migration | `references/migration-playbook.md` |
| User asks for source basis or official-practice traceability | `references/source-map.md` |
| Updating this skill, its routing, output contract, or eval policy | `references/self-eval-cases.json` |
| Creating a new prompt | `assets/create-prompt-template.md` |
| Reviewing, improving, migrating, or debugging a prompt | `assets/prompt-review-template.md` |
| Applying a local prompt patch | `assets/prompt-patch-template.md` |
| Writing a tool/function description | `assets/tool-description-contract.md` |
| Writing a judge prompt | `assets/judge-prompt-rubric.md` |
| Writing agent instructions | `assets/agent-instructions-skeleton.md` |
| Writing RAG/context instructions | `assets/rag-context-instructions-template.md` |
| Creating eval cases | `assets/eval-cases-template.json` |

## Output Policy

Artifact first. Do not output empty sections.
Default to Chinese-first labels and prose. Keep canonical contract terms such as Prompt Artifact / Patch, Intervention Layer, Non-Prompt Findings, and the compatibility alias Non-Prompt Requirements visible when they are part of the template or eval contract; for primarily English users, use English-first labels and prose. Keep enum values, file paths, commands, schema keys, and provider API names literal.
For review/improve/debug tasks, this SKILL.md keeps only the output section order. Use `assets/prompt-review-template.md` as the detailed source for section content when the Resource Loading table loads it.

For simple creation or "just give me the prompt" requests:

```text
Prompt:
<copy-ready prompt>

Usage:
- <where to place it, how to substitute variables, applicable model/runtime>

Assumptions:
- <omit this section when no assumption matters>

Minimal Eval Cases:
- happy-path: <case>
- edge-or-regression: <case>
- forbidden-or-format-failure: <case>
```

For review, improve, migrate, or debug requests:

```text
Prompt 产物 / Patch（Prompt Artifact / Patch）:
<copy-ready artifact or patch>

干预层（Intervention Layer）:
<primary layer; add supporting layer only when needed>

Prompt Architecture:
<include only for product/runtime prompts>

Runtime Contract:
<include only when runtime context matters>

调整依据（Rationale）:
<why this is the smallest effective intervention>

非 Prompt 发现（Non-Prompt Findings） / 非 Prompt 侧要求（Non-Prompt Requirements）:
<omit when none matter>

Spec / Implementation Drift:
<omit when none matter>

Eval Coverage:
<omit only for simple prompt creation>

最小 Eval（Minimal Eval）:
<happy-path, edge, forbidden/format regression, and product-runtime regression when applicable>

Recommended Order of Work:
<include only when product/runtime review, mixed prompt/non-prompt work, or sequencing matters>

风险和取舍（Risk And Tradeoff）:
<complexity, cost, latency, portability, provider fit, or source risk>
```

## Patch Formats

- For prompts stored in files, use unified diff.
- For pasted prompt text, use SEARCH/REPLACE blocks.
- For structured prompts, use section-level patch.
- If an exact patch is unsafe, provide a full rewrite and state why.

## Gotchas

- Do not turn every issue into a longer prompt. Prefer schema, tool contracts, context design, or provider parameters when they control behavior more reliably.
- Do not treat product/runtime prompts as isolated text artifacts. If a prompt controls a long-running agent or workflow, check context assembly, schema, memory/history, repair loop, persistence, and spec drift before proposing only wording changes.
- Do not add chain-of-thought instructions by default. For current reasoning models, prefer outcome-first instructions and provider reasoning controls.
- Reasoning artifacts are API/context state, not ordinary prompt text. Check provider preserve, strip, replay, or parse rules in multi-turn tool flows.
- Tool-use failures often come from tool surface design, not wording. Check tool count, namespaces, deferred tools, merge candidates, code-known parameters, return shape, side effects, and idempotency.
- Few-shot examples are useful for format, style, and hard boundaries, but poor examples lock in errors.
- If a prompt change matters, add eval cases. Without eval, label the recommendation unverified.
- `skill-tuning` owns SKILL.md/skill folder structure and routing. Use prompt-tuning only for prompt/instruction wording inside a skill when explicitly requested.
