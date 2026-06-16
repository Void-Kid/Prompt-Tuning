# Prompt Tuning

Language: [中文](README.md) | **English**

Prompt work should feel more like engineering and less like guesswork. **Prompt Tuning** is a prompt-tuning skill for agents such as Codex and Claude Code. It helps agents diagnose, rewrite, migrate, and evaluate prompts so prompt-related work becomes more stable, reusable, and verifiable.

It distills public best practices from major model providers such as OpenAI, Anthropic, Google, Qwen, and Kimi across prompting, agent instructions, structured outputs, and tool use. It also incorporates systematic resources such as Prompting Guide, then turns that knowledge into self-eval cases, quality checks, migration methods, and output templates. You can hand prompt work to an agent and get grounded, reusable, and verifiable outputs for writing, improving, migrating, or debugging prompts.

Try this skill when you often run into issues like:

- A prompt has gone through many edits but remains unstable
- JSON, schema, or tool-calling outputs keep breaking
- System prompts, developer prompts, or agent instructions keep growing longer
- The same prompt behaves differently across Codex, Claude Code, or other model runtimes
- It is unclear whether the problem lives in the prompt, tool surface, context, schema, or eval

The core value of **Prompt Tuning** is to help an agent identify the right intervention layer before producing a usable prompt, patch, tool description, judge prompt, or concrete improvement plan.

## What It Is

**Prompt Tuning** is an agent skill for creating, reviewing, improving, migrating, debugging, and evaluating LLM prompts and prompt-like instructions.

It covers:

- system / developer / user prompts
- agent instructions
- tool / function descriptions
- structured output, JSON, and schema prompts
- RAG / context instructions
- judge prompts and eval prompts
- prompt templates
- prompt migration across agent runtimes

It is designed for real agent workflows and covers prompt wording, tool interfaces, structured outputs, context design, model state, evaluation cases, and cross-model migration.

## How It Works

Prompt Tuning follows a simple loop:

1. **Diagnose the intervention layer**
   - prompt wording
   - instruction hierarchy
   - tool/schema contract
   - structured output
   - context/RAG
   - memory or compaction
   - reasoning/provider state
   - model parameters or model choice
   - eval gap

2. **Choose the smallest useful change**
   - rewrite prompt text when wording is the bottleneck
   - improve tool descriptions when tool choice or arguments fail
   - tighten schema or structured output contracts when formatting breaks
   - adjust RAG/context instructions when retrieval or grounding is weak
   - add eval cases when the issue cannot be verified

3. **Return something usable**
   - copy-ready prompt
   - prompt patch
   - tool description contract
   - judge prompt
   - minimal eval cases
   - risks, assumptions, and non-prompt requirements

## Why It Exists

Modern models are powerful enough that older prompting habits can become counterproductive. Long, over-specified prompts often hide the real issue. Many failures come from tool design, schemas, retrieved context, state handling, parser rules, eval gaps, or model/runtime mismatch.

Prompt Tuning makes the diagnostic step explicit so an agent can decide what layer to change before rewriting the prompt.

## Source Basis

This skill distills public guidance and engineering practices from major model providers and prompting resources, including:

- OpenAI prompt guidance, function calling, structured outputs, and Model Spec
- Anthropic prompt engineering, eval development, context engineering, and tool design guidance
- Google Gemini prompting, function calling, structured output, thinking/tool state, and optimizer guidance
- Qwen, Kimi, DeepSeek, Meta Llama, Mistral, xAI, Perplexity, Cohere, and Bedrock model/runtime guidance
- Prompting Guide and related context engineering material

These practices live in `references/`, with a source map that tracks where each principle came from and when model-specific guidance should be checked again.

## Repository Structure

```text
skills/
  prompt-tuning/
    SKILL.md
    agents/
    assets/
    references/
```

Key files:

- `skills/prompt-tuning/SKILL.md`: the skill entrypoint and workflow
- `skills/prompt-tuning/assets/`: reusable prompt, review, patch, eval, tool, judge, and RAG templates
- `skills/prompt-tuning/references/`: principles, model-specific notes, migration guidance, eval guidance, and source map

## How To Use

Use `skills/prompt-tuning` as a local agent skill in any environment that supports skill-style instructions.

Typical flow:

1. Add or reference the `skills/prompt-tuning` directory in your agent environment.
2. Ask the agent to use Prompt Tuning when the task involves prompt creation, review, improvement, migration, debugging, or eval design.
3. Provide the current prompt, target model/runtime, failure examples, expected output, tool/schema/context constraints, and any latency or cost constraints.

Example requests:

```text
Use Prompt Tuning to improve this system prompt and reduce JSON format errors.
```

```text
Use Prompt Tuning to review this agent instruction and identify the right intervention layer.
```

```text
Migrate this Codex prompt to Claude Code agent instructions.
```

```text
Write a tool description for this function and include minimal eval cases.
```

## Output Style

For simple creation tasks, the skill usually returns:

- copy-ready prompt
- usage notes
- necessary assumptions
- minimal eval cases

For review, improvement, migration, or debugging tasks, the skill usually returns:

- Prompt Artifact / Patch
- Intervention Layer
- Rationale
- Non-Prompt Requirements
- Minimal Eval
- Risk and Tradeoff

## Boundaries

Prompt Tuning focuses on prompt and prompt-adjacent instruction work. Ordinary writing, general code review, plugin creation, skill authoring, installation flows, and full security audits are better handled by dedicated workflows.

Provider behavior changes quickly. When a task depends on latest model behavior, tool calling, structured outputs, reasoning state, prompt caching, or parser rules, check current official sources again.

## License

MIT
