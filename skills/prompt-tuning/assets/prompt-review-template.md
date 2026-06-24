# Prompt Review Template

Use for review, improve, migrate, and debug tasks. Lead with the usable artifact, then explain the behavior change and its tradeoffs. Review prompts against the target model, runtime, tool surface, schema, context sources, and failure examples. If the root cause is outside the prompt, still provide the smallest useful wording change and clearly separate schema, API, retrieval, parser, product, persistence, repair, or spec recommendations.

For product/runtime prompts, do not treat the prompt as an isolated text artifact. Review the prompt architecture and runtime contract before proposing a local wording patch.

Prompt 产物 / Patch（Prompt Artifact / Patch）:

```text
<copy-ready improved prompt, replacement, SEARCH/REPLACE patch, unified diff, section-level patch, tool description, or judge prompt>
```

干预层（Intervention Layer）:
- primary: prompt wording | instruction hierarchy | prompt architecture | tool/schema contract | structured output | context/RAG | memory/compaction | reasoning/provider state | model params/model choice | eval gap
- supporting: second layer only when it changes the fix

Prompt Architecture:
- Check section hierarchy, role/non-goals, dynamic context contract, evidence vs instruction boundary, semantic judgment vs format layering, hard protocol rules, and examples.
- Omit this section for simple pasted prompts where product/runtime architecture is not relevant.

Runtime Contract:
- Check prompt assembly, actual input objects, provider message envelope, role/message_kind metadata, schema/parser guarantees, repair loop, history trimming, persistence, and observability.
- If runtime files are missing, state what cannot be verified.

调整依据（Rationale）:
- Name the issue, user impact, and why the current prompt causes it.
- Explain why this intervention layer is the smallest effective change.
- Call out missing eval evidence when the recommendation is not yet verified.

非 Prompt 发现（Non-Prompt Findings） / 非 Prompt 侧要求（Non-Prompt Requirements）:
- Use this for schema, tool surface, context, provider state, model parameters, evals, parser, API, repair, persistence, observability, or product changes.
- Omit this section only when no non-prompt finding matters.

Spec / Implementation Drift:
- List mismatches between prompt wording, product spec, runtime implementation, schemas, parser, persistence, and tests.
- Omit this section only when no drift is found or enough evidence is unavailable.

Eval Coverage:
- List existing eval quality, semantic gaps, runtime/schema coverage, missing badcases, and whether tests only assert substrings.
- For product/runtime prompts, include semantic evals beyond happy-path, edge, and format cases.

最小 Eval（Minimal Eval）:
- happy-path:
- edge-or-ambiguous:
- forbidden-or-format-regression:
- provider-or-runtime-regression:
- product-runtime-regression:

Recommended Order of Work:
- A. prompt-only:
- B. runtime/schema/spec required:
- C. defer pending evidence:
- Include only when product/runtime review, mixed prompt/non-prompt work, or sequencing matters; omit for simple prompt creation or single-layer fixes.

风险和取舍（Risk And Tradeoff）:
- Include added complexity, cost, latency, portability, provider-specific risk, and source freshness risk.
- Note whether the improvement makes the prompt longer, narrower, more model-specific, or more dependent on external context.
