# Paperclip Adoption Trigger

## Objective

Define one bounded workflow-level trigger that would justify reopening Paperclip as an optional supervision layer without letting it take over OpenClaw repo task ownership.

## Evidence base

Primary current sources:
- `research/paperclip-integration.md`
- `research/paperclip-runtime-boundary.md`
- `research/validation-and-decision-gates.md`
- `research/architecture-review.md`

Upstream Paperclip surfaces already inspected in this repo:
- `paperclipai/paperclip/docs/agents-runtime.md`
- `paperclipai/paperclip/docs/guides/agent-developer/how-agents-work.md`
- `paperclipai/paperclip/docs/guides/agent-developer/heartbeat-protocol.md`
- `paperclipai/paperclip/docs/guides/board-operator/costs-and-budgets.md`
- `paperclipai/paperclip/server/src/services/heartbeat.ts`
- `paperclipai/paperclip/server/src/services/budgets.ts`
- `paperclipai/paperclip/server/src/services/issues.ts`

## Candidate workflow

Portfolio-level oversight for three or more parallel OpenClaw workstreams, where each workstream already has its own planning bundle and repo task state, but the operator now needs one place to:
- see high-level status across all active workstreams
- enforce per-agent or per-project budget ceilings
- pause, resume, or reprioritize work at the portfolio layer
- observe heartbeat cadence and inactivity without opening each repo separately

This is deliberately **not** a repo-task orchestration workflow. It is a multi-workstream oversight workflow.

## OpenClaw-owned surfaces

- initiative planning bundles under `docs/planning/<initiative>/`
- repo task decomposition, readiness, and acceptance criteria
- repo-local execution artifacts, commits, and closeout
- approval-aware implementation work
- final synthesis and architecture decisions inside the repo

## Paperclip-owned surfaces

- cross-workstream dashboard visibility
- budget ceilings and budget-triggered pausing
- company-, project-, or agent-level status rollups
- portfolio-level wake cadence and supervision for the agents or runtimes that Paperclip explicitly manages
- operator actions such as pause, reprioritize, or terminate at the portfolio layer

Paperclip is allowed to own these surfaces only if the managed unit is explicitly a Paperclip-managed agent or endpoint. It must not silently inherit repo task ownership.

## Value hypothesis

Paperclip becomes worth testing only if the operator problem is no longer "how do I run one OpenClaw workstream well?" and has become "how do I supervise several active workstreams with budget and liveness controls from one surface?"

The expected payoff is:
- less operator context switching across repos
- clearer budget enforcement than repo-local notes alone
- faster detection of stalled or overactive workstreams
- portfolio-level governance without moving repo task state out of OpenClaw

## Rejection signals

Reject a Paperclip reopen if any of these remain true:
- one primary OpenClaw workflow still dominates the real workload
- budget pain is still hypothetical rather than operational
- Paperclip would need to mirror or replace repo task cards to feel useful
- the operator can already get enough visibility from OpenClaw-native planning bundles and status files
- the extra Node server, UI, and database would add more operational work than they remove

## Adoption trigger

Reopen Paperclip only when at least two of these are true in the same operating period:
- three or more active OpenClaw workstreams need shared visibility
- cost governance or per-agent budget ceilings have become an operational concern
- top-level status visibility is repeatedly painful across workstreams
- pause, resume, or reprioritize actions are needed at a portfolio layer rather than inside one repo

If reopened, the first prototype should be a supervision-only spike that leaves repo task ownership inside OpenClaw.

## Decision impact

If the trigger is met:
- keep the current architecture direction
- reopen Paperclip only as an optional supervision spike
- define the spike around budgets, visibility, and portfolio cadence rather than around repo issue ownership

If the trigger is not met:
- keep Paperclip deferred
- treat OpenClaw planning bundles as the sufficient control surface for now

## What Would Overturn This Conclusion

This conclusion should be revisited if one of these becomes true:
- stronger upstream evidence shows Paperclip can supervise external runtimes without materially owning heartbeat, issue, and session semantics
- OpenClaw-native oversight grows enough that portfolio visibility and budget control can be handled cleanly without another runtime
- real operator pain shows that Paperclip must own repo task flow to create value, which would weaken the current separation model

## Bottom line

Paperclip should reopen only as a response to real portfolio-level oversight pain. The trigger is not "Paperclip looks useful"; it is "multiple parallel OpenClaw workstreams now need shared visibility and budget governance without relocating repo task state."
