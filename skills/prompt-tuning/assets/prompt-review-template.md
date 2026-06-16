# Prompt Review Template

Use for review, improve, migrate, and debug tasks. Lead with the usable artifact, then explain the behavior change and its tradeoffs. Review prompts against the target model, runtime, tool surface, schema, context sources, and failure examples. If the root cause is outside the prompt, still provide the smallest useful wording change and clearly separate schema, API, retrieval, parser, or product recommendations.

Prompt 产物 / Patch（Prompt Artifact / Patch）:

```text
<copy-ready improved prompt, replacement, SEARCH/REPLACE patch, unified diff, section-level patch, tool description, or judge prompt>
```

干预层（Intervention Layer）:
- primary: prompt wording | instruction hierarchy | tool/schema contract | structured output | context/RAG | memory/compaction | reasoning/provider state | model params/model choice | eval gap
- supporting: second layer only when it changes the fix

调整依据（Rationale）:
- Name the issue, user impact, and why the current prompt causes it.
- Explain why this intervention layer is the smallest effective change.
- Call out missing eval evidence when the recommendation is not yet verified.

非 Prompt 侧要求（Non-Prompt Requirements）:
- Use this for schema, tool surface, context, provider state, model parameters, evals, parser, or API changes.
- Omit this section only when no non-prompt requirement matters.

最小 Eval（Minimal Eval）:
- happy-path:
- edge-or-ambiguous:
- forbidden-or-format-regression:
- provider-or-runtime-regression:

风险和取舍（Risk And Tradeoff）:
- Include added complexity, cost, latency, portability, provider-specific risk, and source freshness risk.
- Note whether the improvement makes the prompt longer, narrower, more model-specific, or more dependent on external context.
