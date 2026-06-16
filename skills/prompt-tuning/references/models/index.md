# Model Guidance Index

Read only the provider file needed for the user's target model. If the model is unknown, stay model-agnostic and avoid provider-specific claims.

| Provider or model family | Read |
| --- | --- |
| OpenAI GPT-5.x, Responses API, Model Spec, structured outputs | `openai.md` |
| Claude, Anthropic Messages API, adaptive thinking, XML-style prompts | `anthropic.md` |
| Gemini 3.x, thinking, thought signatures, long context | `google.md` |
| Mistral and Magistral | `mistral.md` |
| Meta Llama | `meta-llama.md` |
| DeepSeek | `deepseek.md` |
| Qwen | `qwen.md` |
| Kimi / Moonshot | `kimi.md` |
| xAI, Perplexity, Cohere, AWS Bedrock | `xai-perplexity-cohere-bedrock.md` |

If the user asks for latest/current behavior, context windows, pricing, tool protocols, reasoning/thinking API behavior, or structured-output behavior, verify against official sources before making a version-specific claim.
