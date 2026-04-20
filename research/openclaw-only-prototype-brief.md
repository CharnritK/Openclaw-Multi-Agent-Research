# OpenClaw-Only Prototype Brief

## Objective

Create a small execution-ready prototype brief for the OpenClaw-only control case so future implementation can start without re-planning the architecture.

## Prototype statement

The prototype is not a new platform. It is a tightened operating pattern that proves OpenClaw can remain the center of the stack without immediate Paperclip or Hermes adoption.

## Single clear outcome

Document and validate one small OpenClaw-only workflow that demonstrates:
- planning bundle ownership
- bounded task progression
- modular task-level commits
- explicit criteria for when external layers are still unnecessary

## Scope

### In scope
- define the OpenClaw-only control-case workflow
- define expected artifacts and decision points
- define what success looks like for this control case
- define signals that would justify future Paperclip or Hermes spikes

### Out of scope
- deploying Paperclip
- installing Hermes
- building bridge infrastructure
- implementing a broad automation loop
- changing OpenClaw core behavior

## Deliverables

- a short prototype workflow description
- explicit success criteria
- explicit failure or escalation criteria
- a follow-up trigger list for Paperclip and Hermes

## Proposed prototype workflow

1. start from a planning bundle and explicit current task
2. perform one bounded research or documentation task in OpenClaw
3. close the unit with a modular commit
4. update status and next-best-task state
5. check whether operator pain or specialist-runtime pain appeared

## Success criteria

The prototype succeeds if:
- the workflow remains understandable end to end
- commit discipline is easy to maintain
- status and task readiness stay current
- no external orchestration layer is needed to keep work moving
- triggers for future Paperclip or Hermes adoption remain hypothetical rather than urgent

## Failure criteria

The prototype fails if:
- the operator lacks enough visibility to manage the work comfortably
- cost or portfolio concerns demand a management layer immediately
- the workflow clearly needs remote persistence, stronger scheduling, or specialist runtime behavior that OpenClaw alone does not cover well
- the control case cannot stay simple without constant manual rescue

## Escalation triggers

### Escalate toward Paperclip if
- multiple active agent surfaces need one oversight layer
- budgeting and agent governance become concrete pain points
- portfolio-level visibility becomes a repeated blocker

### Escalate toward Hermes if
- a specific workflow needs long-lived remote execution
- messaging-heavy continuity becomes central
- built-in scheduling or specialist runtime behavior becomes a real requirement

## Non-goals

- proving every possible integration path
- comparing every agent framework again
- designing a full production operating system

## Recommendation

Treat this prototype as the control case. If it works cleanly, keep the architecture simple. If it fails on a concrete pain point, use that pain point, not general curiosity, to choose the next integration spike.
