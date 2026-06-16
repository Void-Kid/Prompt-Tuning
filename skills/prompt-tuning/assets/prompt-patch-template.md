# Prompt Patch Template

Use when the requested output is a precise change to an existing prompt rather than a full rewrite. Choose the narrowest patch format that can be applied safely. The patch should preserve unrelated wording, keep anchors exact, and make the behavior change auditable. If the prompt text is too ambiguous to patch reliably, switch to the fallback and explain the matching risk in one sentence.

## Unified Diff

Use when the prompt lives in a file.

```diff
--- a/path/to/prompt.md
+++ b/path/to/prompt.md
@@
- Old prompt line that causes the failure.
+ New prompt line that changes the behavior.
```

## SEARCH/REPLACE

Use when the user pasted prompt text.

```text
SEARCH:
Old prompt passage.

REPLACE:
New prompt passage.
```

## Section-Level Patch

Use when the prompt is organized into named sections.

```text
Section: Output Contract
Action: Replace
New content:
- Return JSON matching the configured schema.
- Do not include prose outside the structured output.
```

## Fallback

If the target text cannot be matched safely, provide a complete rewritten prompt and state that exact patching was unsafe because the anchor was ambiguous or missing. Include the behavioral intent, the replaced section name when known, and one eval case that would have failed before the change.

## Smallest Effective Change

After the patch, state why this is the narrowest change that controls the observed failure. Mention the primary intervention layer and the old failure the patch should prevent.

## Non-Prompt Coordination

If the patch depends on schema, tool description, context boundary, provider state replay, parser behavior, model parameters, or evals, list that dependency next to the patch. If the dependency is the main fix, keep the prompt patch small and say that the non-prompt change carries the reliability guarantee.
