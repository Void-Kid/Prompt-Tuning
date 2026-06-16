# Prompt Tuning

语言：**中文** | [English](README.en.md)

Prompt 工作应该更像工程，少一些玄学。**Prompt Tuning** 是一个面向 Codex、Claude Code 等 agent 的 prompt 调优 skill，帮助 agent 诊断、改写、迁移和评估 prompt，让 prompt 相关工作更稳定、可复用、可验证。

如果你经常遇到这些问题，这个 skill 值得一试：

- Prompt 改了很多轮，效果仍然不稳定
- JSON、schema、tool calling 经常出格式错误
- System prompt / developer prompt / agent instructions 越写越长
- 同一个 prompt 在 Codex、Claude Code 或其他模型环境里表现不一致
- 很难判断问题到底出在 prompt、工具、上下文、schema，还是 eval

**Prompt Tuning** 的核心价值是让 agent 先判断问题应该在哪一层解决，再产出可直接使用的 prompt、patch、tool description、judge prompt 或改进建议。

## 它是什么

**Prompt Tuning** 用于创建、评审、改进、迁移、调试和评估 LLM prompt 以及 prompt-like instructions。

它覆盖这些对象：

- system / developer / user prompts
- agent instructions
- tool / function descriptions
- structured output、JSON、schema prompts
- RAG / context instructions
- judge prompts 和 eval prompts
- prompt templates
- 不同 agent runtime 之间的 prompt 迁移

它面向真实 agent 工作流设计，覆盖提示词表达、工具接口、结构化输出、上下文设计、模型状态、评估样例和跨模型迁移。

## 它怎么工作

Prompt Tuning 使用一个简单流程：

1. **诊断干预层**
   - prompt wording
   - instruction hierarchy
   - tool/schema contract
   - structured output
   - context/RAG
   - memory or compaction
   - reasoning/provider state
   - model parameters or model choice
   - eval gap

2. **选择最小有效改动**
   - 文案是瓶颈时，改写 prompt
   - 工具选择或参数出错时，改进 tool description
   - 输出格式不稳定时，收紧 schema 或 structured output contract
   - 检索或上下文不足时，调整 RAG/context instructions
   - 问题无法验证时，补充 eval cases

3. **返回可直接使用的结果**
   - copy-ready prompt
   - prompt patch
   - tool description contract
   - judge prompt
   - minimal eval cases
   - 风险、假设和非 prompt 侧要求

## 为什么需要它

现代模型能力很强，传统 prompt 习惯有时会带来副作用。过长、过度规定的 prompt 往往会掩盖真正的问题。很多失败来自工具设计、schema、检索上下文、状态处理、parser 规则、eval 缺口或模型/runtime 不匹配。

Prompt Tuning 会把诊断过程显性化，让 agent 在改 prompt 之前先判断应该改哪一层。

## 参考来源

这个 skill 整理了主流模型官方公开资料和工程实践，包括：

- OpenAI prompt guidance、function calling、structured outputs 和 Model Spec
- Anthropic prompt engineering、eval development、context engineering 和 tool design guidance
- Google Gemini prompting、function calling、structured output、thinking/tool state 和 optimizer guidance
- Qwen、Kimi、DeepSeek、Meta Llama、Mistral、xAI、Perplexity、Cohere、Bedrock 等模型和 runtime 指引
- Prompting Guide 以及 context engineering 相关资料

这些内容沉淀在 `references/` 中，并通过 source map 记录原则来源和模型相关建议的时效性。

## 仓库结构

```text
skills/
  prompt-tuning/
    SKILL.md
    agents/
    assets/
    references/
```

关键文件：

- `skills/prompt-tuning/SKILL.md`：skill 入口和工作流
- `skills/prompt-tuning/assets/`：prompt、review、patch、eval、tool、judge、RAG 等模板
- `skills/prompt-tuning/references/`：核心原则、模型参考、迁移方法、eval 方法和 source map

## 使用方式

把 `skills/prompt-tuning` 作为本地 agent skill 放到支持 skill-style instructions 的 agent 环境中使用。

典型流程：

1. 在 agent 环境中添加或引用 `skills/prompt-tuning` 目录。
2. 当任务涉及 prompt 创建、评审、改进、迁移、调试或 eval 设计时，让 agent 使用 Prompt Tuning。
3. 提供当前 prompt、目标模型/runtime、失败样例、期望输出、工具/schema/context 约束，以及成本或延迟限制。

示例请求：

```text
用 Prompt Tuning 改进这个 system prompt，减少 JSON 格式错误。
```

```text
用 Prompt Tuning 评审这个 agent instruction，判断问题应该在哪一层解决。
```

```text
把这个 Codex prompt 迁移成 Claude Code agent instructions。
```

```text
帮我为这个 tool 写 description，并给最小 eval cases。
```

## 输出风格

简单创建任务通常返回：

- 可直接复制使用的 prompt
- 使用说明
- 必要假设
- 最小 eval cases

评审、改进、迁移或调试任务通常返回：

- Prompt Artifact / Patch
- Intervention Layer
- Rationale
- Non-Prompt Requirements
- Minimal Eval
- Risk and Tradeoff

## 边界

Prompt Tuning 聚焦 prompt 和 prompt-adjacent instruction 工作。普通写作、通用代码 review、plugin 创建、skill 编写、安装流程和完整安全审计，更适合交给对应的专门工作流。

模型供应商行为变化很快。任务涉及最新模型行为、tool calling、structured outputs、reasoning state、prompt caching 或 parser 规则时，应结合当前官方资料再次确认。

## License

MIT
