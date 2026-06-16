# xAI, Perplexity, Cohere, And Bedrock Prompt Guidance

## Prompt Implications

- xAI: use Responses-style stateful interactions, structured outputs, tool/code execution, and prompt caching guidance when available.
- Perplexity: user input drives search behavior more than a generic system prompt; use API parameters for domains, dates, region, and step limits.
- Cohere: use Command model guidance for structured output, tool use, and vision inputs when relevant.
- AWS Bedrock: prompt optimization should be data-driven with examples, metrics, and baseline comparison.

## Tool And Structured Output Implications

- Prefer provider structured-output features or tool APIs over prompt-only formatting instructions.
- For search-backed models, use request parameters for retrieval control instead of asking the model to search differently in prose.
- For Bedrock prompt optimization, keep fixed prompt, variables, sample inputs, metric, baseline, and optimized result together.

## Reasoning/Thinking State

- Perplexity reasoning models can include `<think>` before structured output; parser design may need to strip or handle it before JSON validation.
- xAI reasoning and prompt-caching behavior is API-specific and should be verified for current models.

## Staleness Risk

- Model names, search behavior, prompt optimizer features, and structured-output support are provider-specific and time-sensitive.
