# Decision-Hardening Review

## Objective

Re-review the architecture after publishing the Paperclip adoption trigger, the Hermes worker contract, and the decision evidence map.

## Evidence base

Primary current sources:
- `research/paperclip-adoption-trigger.md`
- `research/hermes-worker-contract.md`
- `notes/evidence-map.md`
- `research/recommended-architecture.md`
- `research/validation-and-decision-gates.md`
- `research/architecture-review.md`

Upstream evidence already relied on by this checkpoint:
- `paperclipai/paperclip/docs/agents-runtime.md`
- `paperclipai/paperclip/docs/guides/agent-developer/heartbeat-protocol.md`
- `paperclipai/paperclip/server/src/services/heartbeat.ts`
- `paperclipai/paperclip/server/src/services/budgets.ts`
- `NousResearch/hermes-agent/run_agent.py`
- `NousResearch/hermes-agent/agent/prompt_builder.py`
- `NousResearch/hermes-agent/gateway/run.py`
- `NousResearch/hermes-agent/tools/delegate_tool.py`

## Verdict

Keep the current architecture **unchanged**.

The decision-hardening artifacts improved the precision of the recommendation, but they did not produce evidence that justifies changing the architecture direction:
- OpenClaw remains the primary control plane.
- Paperclip remains optional and should reopen only for real portfolio-level oversight pain.
- Hermes remains a bounded specialist runtime candidate, with the remote watcher contract as the cleanest reopen path.
- Shared-channel bridge work remains deferred unless a hard channel requirement appears.

## What improved in Phase 7

### 1. Paperclip now has a concrete reopen trigger

The repo no longer says only "use Paperclip if it becomes worth it." It now says exactly which workflow would justify reopening it and which ownership surfaces must stay with OpenClaw.

### 2. Hermes now has a single explicit specialist contract

The repo no longer relies on a vague future backend-style idea. It now has one bounded workflow that can be evaluated without turning Hermes into a second primary control plane.

### 3. Major claims are now traceable

The evidence map makes it possible to see:
- which claims are strong
- which claims are still only medium-confidence
- what counterevidence already exists
- what exact trigger would justify reopening each question

## What did not change

- No live Paperclip, Hermes, or bridge prototype was run.
- Bridge-runtime complexity is still intentionally less explored than Paperclip and Hermes source ownership questions.
- The architecture remains medium-confidence for direction, not proof of implementation payoff.

## Deferred questions that remain correctly deferred

### Paperclip

Stay deferred until portfolio-level visibility, budgets, and cross-workstream supervision become operational pain rather than possibility value.

### Hermes

Stay deferred until one specialist workflow clearly benefits from remote persistence or scheduling beyond what OpenClaw alone covers well.

### Bridge work

Stay deferred until a real shared-channel requirement appears. The repo still has no reason to pay bridge complexity preemptively.

## What Would Overturn This Checkpoint

Reopen this review only if one of these becomes true:
- the Paperclip adoption trigger is met in live operation
- the Hermes remote watcher workflow becomes concrete and worth trialing
- a messaging-channel requirement makes bridge behavior decision-critical
- a new framework or upstream runtime change materially threatens the current recommendation rather than merely adding optionality

## Bottom line

Phase 7 improved the repo's decision quality without broadening scope. The architecture is still conservative by design, but it is now harder to reopen casually and easier to reopen for one precise reason at a time.
