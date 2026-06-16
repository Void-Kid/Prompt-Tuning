# Meta Llama Prompt Guidance

## Prompt Implications

- Use the prompt format expected by the target Llama release and serving stack.
- Keep task instructions compact and examples representative.
- For smaller or local models, traditional techniques like few-shot examples and prompt chaining may matter more than with frontier reasoning models.

## Tool And Structured Output Implications

- Follow the model-specific tool-use template rather than inventing ad hoc function-call text.
- Use prompt-ops or eval-driven optimization when moving prompts across Llama model families.
- Prefer schemas and parsers for strict output shape.

## Reasoning/Thinking State

- Treat visible chain-of-thought requests as model and product dependent. Use concise rationale requirements only when visible reasoning is required.

## Staleness Risk

- Llama prompt formats and tool templates differ by release and inference framework. Verify official model cards or prompt-format docs.
