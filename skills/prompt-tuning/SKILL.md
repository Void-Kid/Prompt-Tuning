---
name: prompt-tuning
description: 'Use when the target artifact or failure root cause is LLM prompt or instruction wording: create, review, improve, rewrite, migrate, debug, evaluate, or tune system/developer/user prompts, agent instructions, tool/function descriptions, structured-output prompts, RAG/context instructions, judge prompts, eval prompts, or prompt templates. Triggers include "帮我写 prompt", "优化这个提示词", "改进 system prompt", "review this prompt", "migrate this prompt", "tool description 怎么写", "写一个 judge prompt", and "prompt tuning". Do not use for ordinary content writing, code review, product review, creating or tuning agent skills, SKILL.md work, plugin creation, skill installation, general AI education, or full security audits.'
---

# Prompt Tuning

Use this skill to create, review, improve, patch, migrate, debug, and evaluate prompts or prompt-like instructions. The default output is a usable prompt, an applicable prompt patch, or concrete prompt modification advice.

## Workflow

1. Classify the request type: `create`, `review`, `improve`, `migrate`, `debug`, `eval`, or `model-specific`.
2. Identify the target object: `system prompt`, `developer prompt`, `user prompt`, `agent instructions`, `tool description`, `structured-output prompt`, `RAG/context instructions`, `judge prompt`, or `eval prompt`.
3. Identify the target model/provider, runtime, input variables, expected output, failure examples, tool/schema/context constraints, cost constraints, latency constraints, and current/latest/provider-specific claims.
4. Diagnose the primary intervention layer before rewriting:
   - `prompt wording`
   - `instruction hierarchy`
   - `tool/schema contract`
   - `structured output`
   - `context/RAG`
   - `memory/compaction`
   - `reasoning/provider state`
   - `model params/model choice`
   - `eval gap`
5. Choose the smallest effective intervention. If schema, tool surface, context, provider state, model parameters, or evals are the real bottleneck, still provide the smallest useful prompt change and list the required non-prompt change separately.
6. Apply the Freshness Gate for current/latest/provider-specific behavior: use official current sources or a recently checked `references/source-map.md` entry before making model/provider claims.
7. Load only the resources needed by the table below.
8. Produce the prompt, prompt patch, tool description, judge prompt, or concrete recommendations before theory.
9. Add minimal eval cases for important changes.
10. Explain user impact, risk, and added complexity briefly.

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
| Target model/provider is named or migration is requested | `references/models/index.md`, then the relevant provider file |
| Current/latest/provider-specific claims or source freshness checks | `references/source-map.md`, and official provider docs when the source map is stale |
| Agent instructions, RAG, memory, long context, prompt caching, or context compaction | `references/context-and-agent-guidance.md` |
| Tool/function descriptions, structured outputs, JSON mode, schema wording, or tool-call failure | `references/tool-and-structured-output-guidance.md` |
| Prompt evals, judge prompts, failure examples, regression cases, or optimization loops | `references/eval-and-optimization-method.md` |
| Legacy prompt stack migration | `references/migration-playbook.md` |
| User asks for source basis or official-practice traceability | `references/source-map.md` |
| Updating this skill, its routing, output contract, or eval policy | `references/self-eval-cases.json` |
| Creating a new prompt | `assets/create-prompt-template.md` |
| Reviewing or improving a prompt | `assets/prompt-review-template.md` |
| Applying a local prompt patch | `assets/prompt-patch-template.md` |
| Writing a tool/function description | `assets/tool-description-contract.md` |
| Writing a judge prompt | `assets/judge-prompt-rubric.md` |
| Writing agent instructions | `assets/agent-instructions-skeleton.md` |
| Writing RAG/context instructions | `assets/rag-context-instructions-template.md` |
| Creating eval cases | `assets/eval-cases-template.json` |

## Output Policy

Artifact first. Do not output empty sections.
Default to Chinese-first labels and prose. Keep canonical contract terms such as Prompt Artifact / Patch, Intervention Layer, and Non-Prompt Requirements visible when they are part of the template or eval contract; for primarily English users, use English-first labels and prose. Keep enum values, file paths, commands, schema keys, and provider API names literal.

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
<copy-ready prompt, replacement, SEARCH/REPLACE patch, unified diff, section-level patch, tool description, or judge prompt>

干预层（Intervention Layer）:
- primary: prompt wording | instruction hierarchy | tool/schema contract | structured output | context/RAG | memory/compaction | reasoning/provider state | model params/model choice | eval gap
- supporting: optional second layer when it affects the fix

调整依据（Rationale）:
- <why this intervention layer is the smallest effective change and what user-visible failure it addresses>

非 Prompt 侧要求（Non-Prompt Requirements）:
- <schema, tool, context, runtime, model params, provider state replay, parser, or eval requirements; omit when none matter>

最小 Eval（Minimal Eval）:
- happy-path: <representative input that should pass>
- edge-or-ambiguous: <short, missing, ambiguous, or adversarial input>
- forbidden-or-format-regression: <case that catches hard-rule, schema, parser, or old-failure regression>

风险和取舍（Risk And Tradeoff）:
- <complexity, cost, latency, portability, provider fit, or unverified source risk>
```

## Patch Formats

- For prompts stored in files, use unified diff.
- For pasted prompt text, use SEARCH/REPLACE blocks.
- For structured prompts, use section-level patch.
- If an exact patch is unsafe, provide a full rewrite and state why.

## Gotchas

- Do not turn every issue into a longer prompt. Prefer schema, tool contracts, context design, or provider parameters when they control behavior more reliably.
- Do not add chain-of-thought instructions by default. For current reasoning models, prefer outcome-first instructions and provider reasoning controls.
- Reasoning artifacts are API/context state, not ordinary prompt text. Check provider preserve, strip, replay, or parse rules in multi-turn tool flows.
- Tool-use failures often come from tool surface design, not wording. Check tool count, namespaces, deferred tools, merge candidates, code-known parameters, return shape, side effects, and idempotency.
- Few-shot examples are useful for format, style, and hard boundaries, but poor examples lock in errors.
- If a prompt change matters, add eval cases. Without eval, label the recommendation unverified.
- `skill-tuning` owns SKILL.md/skill folder structure and routing. Use prompt-tuning only for prompt/instruction wording inside a skill when explicitly requested.
