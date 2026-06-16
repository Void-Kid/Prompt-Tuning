# Qwen Prompt Guidance

## Prompt Implications

- Decide whether the task should run in thinking or non-thinking mode.
- For Qwen3-style hybrid models, explicit thinking controls can matter more than longer process instructions.
- Use examples for multilingual style, output format, and classification boundaries when needed.

## Tool And Structured Output Implications

- Function calling often depends on the framework parser and prompt template.
- Use the recommended tool-call template for the selected Qwen runtime.
- Do not mix incompatible parser styles in the same prompt stack.

## Reasoning/Thinking State

- Preserve or omit thinking content according to the selected runtime and parser.
- Treat tool-call traces as structured state when the framework exposes them.

## Staleness Risk

- Qwen model releases, parser guidance, and thinking controls change quickly. Verify official docs for runtime-specific behavior.

## 2026-06-16 Intervention Notes

- Qwen3-Instruct-2507 is documented as non-thinking only, while Qwen3-Thinking-2507 is documented as thinking only.
- Thinking and non-thinking behavior is version-specific. Do not assume one Qwen3 prompt mode applies to every Qwen3 release.
- When tool calling is enabled, align the prompt template, parser, thinking mode, and framework expectations.
- If output includes thinking markers or tool-call traces, treat them as runtime/parser state rather than ordinary prompt text.
