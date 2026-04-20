# Hermes Worker Contract

## Objective

Define one bounded Hermes-owned workflow contract that can be reopened later without importing Hermes as a second primary control plane.

## Evidence base

Primary current sources:
- `research/hermes-integration.md`
- `research/hermes-practical-boundary.md`
- `research/validation-and-decision-gates.md`
- `research/architecture-review.md`

Upstream Hermes surfaces already inspected in this repo:
- `NousResearch/hermes-agent/README.md`
- `NousResearch/hermes-agent/AGENTS.md`
- `NousResearch/hermes-agent/run_agent.py`
- `NousResearch/hermes-agent/agent/prompt_builder.py`
- `NousResearch/hermes-agent/hermes_state.py`
- `NousResearch/hermes-agent/gateway/session.py`
- `NousResearch/hermes-agent/gateway/run.py`
- `NousResearch/hermes-agent/cron/jobs.py`
- `NousResearch/hermes-agent/cron/scheduler.py`
- `NousResearch/hermes-agent/tools/delegate_tool.py`

## Workflow

A long-lived remote research watcher that scans a fixed upstream watchlist for changes relevant to the OpenClaw multi-agent decision surface and returns structured findings back to OpenClaw.

Bounded watchlist examples:
- `paperclipai/paperclip`
- `NousResearch/hermes-agent`
- one bridge repo only if a real shared-channel requirement appears

Bounded questions:
- did a tracked upstream runtime add or remove capabilities that materially change the current architecture recommendation?
- did a previously deferred trigger become more or less plausible?

## Owner

Hermes owns:
- the remote scheduled watcher runtime
- the watch cadence
- transient remote execution state for this workflow
- collection of raw upstream deltas within the approved watchlist

OpenClaw owns:
- the backlog, planning bundle, and decision criteria
- approval to start, stop, or materially re-scope the watcher
- interpretation of findings into repo decisions
- all canonical artifacts under `docs/planning/`, `research/`, and `notes/`

## Input brief

The watcher input must be explicit and fixed at kickoff:
- watchlist repos or docs
- change categories that matter
- cadence
- stop conditions
- output schema
- escalation thresholds

Minimum input brief:
- `watchlist`: approved upstream repos or docs only
- `goal`: detect decision-relevant changes, not general news
- `filters`: Paperclip ownership changes, Hermes narrow-use seams, bridge requirement changes
- `output format`: structured Markdown summary with source refs, why it matters, and recommended action
- `stop conditions`: no decision-relevant delta for a defined interval, or the workflow starts requiring shared-channel or repo-write access

## Output artifact

Hermes returns one structured finding artifact per reporting interval with:
- `sources reviewed`
- `observed delta`
- `decision relevance`
- `recommended action`
- `confidence`
- `open question`

Canonical outputs must land in OpenClaw-owned files such as:
- `notes/`
- `research/`
- planning bundle updates after explicit OpenClaw review

Hermes should not commit, push, or mutate repo planning state on its own.

## State boundary

Hermes may keep:
- ephemeral job history
- remote session continuity needed for the watcher itself
- temporary summaries needed to finish one report

Hermes must not become the canonical store for:
- architecture decisions
- repo task readiness
- long-term multi-workflow state shared with OpenClaw
- shared user-facing channel continuity for the same workstream

## Approval boundary

OpenClaw approval is required to:
- create the watcher
- change the watchlist materially
- change cadence materially
- broaden the watcher into a bridge, gateway, or multi-workflow orchestrator
- write findings into canonical planning files

Hermes may operate autonomously only inside the pre-approved watcher scope.

## Failure handling

If the watcher hits any of these conditions, it must return a failure artifact to OpenClaw instead of expanding scope:
- source access fails repeatedly
- the watchlist begins requiring shared-channel or gateway ownership
- findings are too ambiguous to classify against the current decision gates
- the watcher starts needing repo writes to stay useful
- the workflow begins depending on persistent shared memory with OpenClaw

The failure artifact should include:
- failure condition
- last successful scan window
- affected sources
- recommended next human decision

## Escalation triggers

Escalate back to OpenClaw if:
- the watcher needs to reply on a shared user-facing channel
- the workflow starts overlapping with repo-local task execution
- Hermes scheduling becomes the real owner of work that OpenClaw still claims to own
- the watcher needs its own budget, approvals, or memory model beyond the bounded contract
- a bridge or migration path starts looking necessary rather than optional

## Why Hermes Instead Of OpenClaw Alone

Hermes is only justified here if the workflow truly benefits from:
- long-lived remote persistence
- built-in scheduling or unattended cadence
- isolation from the local OpenClaw control plane
- a specialist runtime that can watch upstream movement without turning the main OpenClaw session into a permanent monitor

If those benefits are not concrete, OpenClaw alone remains the better default.

## What Would Overturn This Conclusion

Revisit this contract if one of these becomes true:
- OpenClaw can cover the same remote watcher workflow with comparable low operational overhead
- stronger upstream evidence shows Hermes cannot stay useful without shared gateway, memory, or scheduler ownership
- the highest-value Hermes use case turns out not to be remote watching but a different single workflow with a cleaner contract

## Bottom line

The cleanest Hermes reopen path is one bounded remote watcher workflow. Hermes owns the watcher runtime; OpenClaw owns the decision surface. If that boundary cannot stay explicit, Hermes should stay deferred.
