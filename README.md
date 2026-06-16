# Prompt Tuning

Prompt work should feel less like guessing and more like engineering. **Prompt Tuning** gives agents such as Codex and Claude Code a reusable way to diagnose, rewrite, migrate, and evaluate prompts with current model practices in mind.

如果你经常遇到这些问题，这个 skill 值得一试：

- Prompt 改了很多轮，效果仍然不稳定
- JSON、schema、tool calling 经常出格式错误
- System prompt / developer prompt / agent instructions 越写越长
- 同一个 prompt 在 Codex、Claude Code 或其他模型环境里表现不一致
- 很难判断问题到底出在 prompt、工具、上下文、schema，还是 eval

**Prompt Tuning** 的目标是把 prompt 相关工作变成一套可复用的诊断、改写和验证流程，让 agent 先判断问题应该在哪一层解决，再产出可直接使用的 prompt、patch、tool description、judge prompt 或改进建议。

## What It Is

**Prompt Tuning** is an agent skill for creating, reviewing, improving, migrating, debugging, and evaluating LLM prompts and prompt-like instructions.

It covers:

- system / developer / user prompts
- agent instructions
- tool and function descriptions
- structured output and JSON/schema prompts
- RAG and context instructions
- judge prompts and eval prompts
- prompt templates and migration between agent runtimes

它面向真实的 agent 工作流设计，关注的不只是“怎么把提示词写清楚”，还包括工具接口、结构化输出、上下文设计、模型状态、评估样例和跨模型迁移。

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
   - tighten schema or structured output contracts when format breaks
   - adjust context/RAG instructions when retrieval or grounding is weak
   - add eval cases when the issue cannot be verified

3. **Return something usable**
   - a copy-ready prompt
   - a prompt patch
   - a tool description contract
   - a judge prompt
   - minimal eval cases
   - clear risks, assumptions, and non-prompt requirements

## Why This Exists

Modern models are strong enough that older prompting habits can become counterproductive. Long, over-specified prompts often hide the real issue. Many failures come from tool surfaces, schemas, retrieved context, state handling, parser rules, eval gaps, or model/runtime mismatch.

Prompt Tuning helps an agent avoid blind prompt piling by making the diagnosis explicit before changing the prompt.

## Source Basis

This skill distills public guidance and engineering practices from major model providers and prompting resources, including:

- OpenAI prompt guidance, function calling, structured outputs, and Model Spec
- Anthropic prompt engineering, eval development, context engineering, and tool design guidance
- Google Gemini prompting, function calling, structured output, thinking/tool state, and optimizer guidance
- Qwen, Kimi, DeepSeek, Meta Llama, Mistral, xAI, Perplexity, Cohere, and Bedrock model/runtime guidance
- Prompting Guide and related context engineering material

The skill keeps these practices in `references/` and uses a source map to track where each principle came from and when model-specific guidance should be checked again.

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

Typical usage:

1. Add or reference the `skills/prompt-tuning` directory in your agent environment.
2. Ask the agent to use Prompt Tuning when the task involves prompt creation, review, improvement, migration, debugging, or eval design.
3. Provide the current prompt, target model/runtime, failure examples, expected output, tools/schema/context constraints, and any latency or cost constraints.

Example requests:

```text
Use Prompt Tuning to improve this system prompt and reduce JSON format errors.
```

```text
用 Prompt Tuning 评审这个 agent instruction，判断问题是不是 prompt 本身导致的。
```

```text
Migrate this Codex prompt to Claude Code agent instructions.
```

```text
帮我为这个 tool 写 description，并给最小 eval cases。
```

## Output Style

For simple creation tasks, the skill returns:

- copy-ready prompt
- usage notes
- assumptions when needed
- minimal eval cases

For review, improvement, migration, or debugging tasks, the skill returns:

- Prompt Artifact / Patch
- Intervention Layer
- Rationale
- Non-Prompt Requirements
- Minimal Eval
- Risk and Tradeoff

## Boundaries

Prompt Tuning focuses on prompt and prompt-adjacent instruction work. For ordinary writing, general code review, plugin creation, skill authoring, installation workflows, and broad security audits, use a more specific workflow.

Provider-specific behavior changes quickly. When a task depends on latest model behavior, tool calling, structured outputs, reasoning state, prompt caching, or parser rules, the skill uses a freshness gate and should be checked against current official sources.

## English Summary

**Prompt Tuning** is a practical agent skill for prompt engineering, context engineering, tool description design, structured output prompting, prompt migration, and prompt evaluation. It helps agents diagnose the right intervention layer before rewriting, then produce usable prompts, patches, contracts, or eval cases grounded in current model-provider guidance.

## License

MIT
