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

## D-005 Treat Paperclip as a full coordination layer when adopted

- status: accepted
- decision: If Paperclip is adopted later, treat it as owning the company-level heartbeat, issue, session, and budget workflow for the agents it manages, not as a thin wrapper around an already-active OpenClaw orchestration loop.
- rationale: Deeper Paperclip runtime evidence shows it directly owns heartbeat execution, issue workflow semantics, session continuity, and budget-enforced pausing, even though workspace runtime services remain more manual.

## D-006 Treat Hermes as a bounded specialist runtime, not a blended co-owner

- status: accepted
- decision: If Hermes is adopted later, keep OpenClaw as the primary control plane and use Hermes only for explicitly bounded specialist workflows or a narrow backend-style service contract, not as a shared default gateway, scheduler, memory surface, or task owner for the same work.
- rationale: Deeper Hermes runtime evidence shows both strong orchestration overlap and real narrow-use seams. The safe value comes from explicit boundary control, not casual coexistence.

## D-007 Defer bridge deepening unless a channel constraint becomes real

- status: accepted
- decision: Shared-channel bridge complexity does not need a separate deeper inspection unit yet and should stay deferred unless a real messaging-channel constraint makes bridge behavior decision-critical.
- rationale: The current architecture recommendation already avoids bridges by default. Further bridge detail is unlikely to change the recommendation before a concrete shared-channel need exists.

## D-008 Run a docs-first decision-hardening pass before any live integration spike

- status: accepted
- decision: Convert the current medium-confidence architecture direction into explicit adoption triggers, worker contracts, and an evidence map before any live Paperclip, Hermes, or bridge prototype is reopened.
- rationale: The remaining gaps are traceability and bounded reopen conditions, not missing framework breadth.

## D-009 Reopen research only through one bounded trigger question at a time

- status: accepted
- decision: Reopen Paperclip through a single portfolio-oversight adoption-trigger study, reopen Hermes through a single specialist worker contract, and keep broad framework comparison closed unless a new candidate materially threatens the current recommendation.
- rationale: The architecture review identified these as the only remaining questions likely to change the recommendation without inviting research sprawl.
