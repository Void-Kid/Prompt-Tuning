# Eval And Optimization Method

Use this reference when designing prompt evals, judge prompts, regression cases, or prompt optimization loops.

## Minimum Eval Set

- Happy path: representative input that should pass.
- Edge case: missing, short, ambiguous, or adversarial input.
- Forbidden behavior: input that tempts the model to violate a hard rule.
- Format or schema failure: input that previously broke output shape.
- Regression: failure example that motivated the prompt change.

## Optimizer-Grade Artifact

`eval-cases-template.json` should be runnable or easy to wire into a runner. It must include:

- `input_variables`
- `fixed_prompt`
- `dynamic_context`
- `expected_behavior`
- `rubric_or_ground_truth`
- `scorer_type`
- `pass_threshold`
- `baseline_result`
- `optimized_result`
- `failure_taxonomy`
- `cost_latency_notes`

Use `baseline_result` and `optimized_result` to compare before and after behavior. Include cost and latency notes when a prompt adds context, examples, reasoning effort, tools, or extra model calls.

## Judge Prompt Rules

- Judge only observable target behavior, not general writing quality.
- Define scoring dimensions, score anchors, and disqualifying failures.
- Include at least one non-perfect example so the judge does not collapse into lenient grading.
- Require a short rationale tied to rubric dimensions.
- Keep the judge prompt independent from the prompt being evaluated.

## Completion Standard

A prompt improvement is complete only when the agent provides:

- The improved prompt or applicable patch.
- Assumptions and non-prompt recommendations when relevant.
- Eval cases that would catch the old failure.
- Known risk, especially provider-specific behavior or unverified claims.

If no eval data exists, label the recommendation unverified and provide the smallest practical eval set.

## Intervention Evaluation

Evaluate the selected intervention layer, not only the prompt wording.

- Record provider/runtime assumptions such as model name, API surface, structured-output mode, tool loop protocol, reasoning effort, thinking mode, parser, and context assembly.
- Use `failure_taxonomy` values that distinguish prompt wording, instruction hierarchy, tool selection, schema failure, context contamination, provider state error, unsupported claim, verbosity mismatch, and eval gap.
- Compare baseline and optimized behavior before treating the prompt as improved.
- When the primary fix is non-prompt, include one eval that would still fail if only the prompt wording changed.
- For judge prompts, score observable behavior and add disqualifying failures for schema breakage, unsafe tool use, unsupported claims, and ignored context priority.
