# RISKS

## R-001 README-level evidence risk

- severity: medium
- risk: Early research may rely too heavily on README material and public positioning instead of deeper implementation evidence.
- mitigation: Mark assumptions explicitly, keep recommendations provisional, and deepen evidence before prototype decisions.

## R-002 Orchestration overlap risk

- severity: high
- risk: Paperclip or another framework could duplicate OpenClaw control-plane responsibilities and create ambiguous ownership.
- mitigation: Separate operator layer, orchestration layer, and execution layer in every recommendation.

## R-003 Shared-channel bridge brittleness

- severity: high
- risk: Hermes and OpenClaw sharing message channels or gateways may create token conflicts, routing ambiguity, and hard-to-debug state drift.
- mitigation: Treat side-by-side and explicit bridge boundaries as safer defaults than shared live control surfaces.

## R-004 Research sprawl risk

- severity: medium
- risk: The initiative can expand into generic agent-framework exploration with weak relevance to the user's actual workflow.
- mitigation: Keep OpenClaw fit and next-step decisions as the primary scoring lens.

## R-005 Commit discipline drift

- severity: medium
- risk: Work can pile up uncommitted, breaking the modular task-level history the user requested.
- mitigation: Treat commit-and-push as part of task completion, not an optional cleanup step.

## R-006 Hermes boundary drift

- severity: high
- risk: Hermes can start as a narrow specialist runtime but drift into shared gateway, scheduler, memory, or task ownership, recreating the dual-control-plane ambiguity the research is trying to avoid.
- mitigation: Assign one owning control plane per workflow, prefer side-by-side or backend-style boundaries, and treat shared-channel operation as opt-in exception work.

## R-007 Paperclip framing drift

- severity: medium
- risk: The phrase "management layer above OpenClaw" can be interpreted too loosely and hide the fact that Paperclip becomes a stronger orchestration owner once adopted for a workflow.
- mitigation: Describe Paperclip as an owner of the managed workflow surfaces it adopts, not as a passive wrapper around an unchanged OpenClaw loop.
