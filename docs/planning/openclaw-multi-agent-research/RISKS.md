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
