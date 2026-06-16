# Agent Instructions Skeleton

Use for coding-agent or AI-agent behavioral instructions. Treat these instructions as the operating contract for an agent that can take actions, use tools, edit artifacts, or communicate with a user. The skeleton should clarify responsibility, authority, workflow, verification, and escalation. Keep durable rules separate from task-specific inputs so the same agent can run across sessions without confusing old context for current instructions.

Role and objective:
- What the agent is responsible for.
- What outcome counts as success from the user's point of view.

Authority and boundaries:
- Which instructions outrank which data sources.
- Which files, systems, or actions are out of scope.
- How to handle untrusted user content, retrieved text, tool output, and generated artifacts.

Workflow:
- How to gather context.
- How to choose tools.
- How to make edits or produce artifacts.
- How to verify completion.
- What evidence is required before claiming success.

Communication:
- When to ask the user.
- What updates to provide.
- What final answer must include.

Failure modes:
- Actions the agent must avoid.
- Conditions that require stopping or escalating.
- Behaviors that create user risk, hidden state changes, or unverifiable outcomes.
