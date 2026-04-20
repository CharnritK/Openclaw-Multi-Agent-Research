# First Prototype Spike

## Decision

The first prototype spike should be **OpenClaw-only baseline hardening**, not a Paperclip or Hermes integration spike.

## Why this is the first spike

This choice best matches the current evidence:
- OpenClaw is already the strongest fit for Point's workflow
- both Paperclip and Hermes remain conditional additions, not proven necessities
- the decision gates currently support deferral of both integrations
- a smaller first spike reduces architecture risk and keeps the repo honest

## What this prototype is

A bounded OpenClaw-only prototype that strengthens the operating model already recommended:
- planning bundle as the canonical source of truth
- modular task-level Git commits
- explicit task progression and closeout
- no additional orchestration runtime yet

## What this prototype is not

- not a Paperclip deployment spike
- not a Hermes bridge or shared-channel spike
- not a dual-control-plane experiment
- not a broad autonomous-agent demo

## Prototype objective

Prove that the recommended OpenClaw-centered architecture is sufficient as the default path before adding any extra orchestration layer.

## Scope

### In scope
- formalize the OpenClaw-only operating pattern as the control case
- define what a successful repo-level workflow looks like under this model
- identify the minimum signals that would justify later Paperclip or Hermes adoption

### Out of scope
- deploying Paperclip
- installing Hermes for a shared workflow
- building a bridge such as HermesClaw
- integrating multiple new runtimes at once

## Success criteria

The spike is successful if:
- the recommended OpenClaw-only workflow is documented as a practical default
- later integration triggers are explicit and narrow
- the architecture remains understandable in one diagram or one paragraph
- no additional framework is required to keep the research roadmap moving

## Failure criteria

The spike fails if:
- the OpenClaw-only baseline cannot support the intended workflow clearly enough
- operator visibility or governance gaps are already severe enough to force a Paperclip layer
- remote or scheduled specialist workflows are already critical enough to force Hermes into the stack now

## Why Paperclip is deferred

Paperclip is deferred because:
- operator-layer pain is not yet evidenced strongly enough
- adding a company-layer dashboard now would increase complexity before proving need
- OpenClaw already covers the present research workflow adequately

## Why Hermes is deferred

Hermes is deferred because:
- no single workflow has yet justified its stronger scheduling, persistence, or cross-platform features
- shared-channel and bridge complexity would be premature
- side-by-side specialization remains a future option, not a first move

## Recommendation

Proceed next with a brief that defines the OpenClaw-only prototype in executable terms. Keep Paperclip and Hermes explicitly deferred until the trigger conditions in `validation-and-decision-gates.md` are met.

## Bottom line

Do the smallest useful thing first: prove the OpenClaw-only model as the control case. Only add Paperclip or Hermes after that control case shows a real, specific limit.
