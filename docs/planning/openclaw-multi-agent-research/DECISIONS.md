# DECISIONS

## D-001 Keep OpenClaw central

- status: accepted
- decision: OpenClaw remains the center of the target architecture and evaluation rubric.
- rationale: The user asked for a setup suitable for existing OpenClaw usage, not a framework replacement.

## D-002 Prefer small, auditable orchestration

- status: accepted
- decision: Prefer bounded, approval-aware, file-backed operating patterns over broad autonomous swarm designs.
- rationale: Point's current operating model already emphasizes control planes, approval gates, durable artifacts, and reviewability.

## D-003 Treat Paperclip and Hermes as integration tracks, not default dependencies

- status: accepted
- decision: Research Paperclip and Hermes as optional layers with explicit fit tests instead of assuming they belong in the core stack.
- rationale: This avoids architecture lock-in before evidence exists.

## D-004 Enforce modular task-level commits

- status: accepted
- decision: Each bounded completed task should be committed promptly in a modular Git commit before moving to the next best ready task.
- rationale: The user explicitly asked for regular task-level commits and continuous follow-through.
