# Recommended Architecture

## Decision summary

### Recommended path

Use **OpenClaw as the primary control plane**, keep **Paperclip optional as a management layer above it**, and treat **Hermes as a side-by-side specialist runtime or narrow backend integration candidate**, not as a default co-owner of the same workflow.

### Fallback path

If operator-level scaling pain never materializes, stay with **OpenClaw alone** plus repo-local planning bundles and skip both Paperclip and Hermes for the first implementation phase.

## Why this is the recommended path

This path best matches Point's stated and observed preferences:
- bounded orchestration over swarm theater
- approval-aware execution
- durable artifacts and explicit task state
- modular task-level progression
- minimal extra infrastructure unless it pays for itself

It preserves what already fits while leaving room for additional layers only where they create clear leverage.

## Target architecture

### Layer 1, primary control plane: OpenClaw

Role:
- planning, task shaping, repo execution, approvals, and synthesis

Responsibilities:
- own task state and roadmap state for active work
- manage bounded execution units and modular commits
- keep durable artifacts in repo files and planning bundles
- remain the primary operator-facing working environment

Why it stays central:
- strongest fit with Point's current workflow
- lowest architecture risk
- keeps the system explainable and auditable

### Layer 2, optional management layer: Paperclip

Role:
- portfolio supervision when needed

Responsibilities if adopted:
- budgets and cost governance
- org-chart and multi-agent oversight
- high-level goals and portfolio visibility
- heartbeats only at the company or portfolio level, not repo-level task ownership

Boundary:
- Paperclip should not become the co-owner of OpenClaw task decomposition or repo-local control-plane state

Adoption trigger:
- adopt only when multi-agent oversight, budget control, or multi-company visibility becomes painful enough to justify the extra runtime and UI layer

### Layer 3, optional specialist runtime: Hermes Agent

Role:
- specialist runtime for selected capabilities that OpenClaw does not natively optimize for

Potential responsibilities if adopted:
- long-lived remote execution
- richer built-in scheduling and unattended automations
- messaging-heavy or remote continuity workflows
- experimental specialist jobs behind a narrow boundary

Boundary:
- Hermes should not be a default co-owner of the same task and approval flow
- prefer side-by-side specialization first
- consider narrow service-style integration later if the benefit is strong enough

### Shared-channel bridge stance

Bridge solutions like HermesClaw are valid only when a shared channel is a hard requirement. They are not the recommended first prototype because they raise routing complexity and make ownership blurrier.

## Prototype scope

### Smallest useful prototype

Prototype only the minimum architecture that can answer the key decision questions:

1. **Baseline mode**
   - OpenClaw-only workflow with the planning bundle and modular commit discipline already established in this repo

2. **Optional Paperclip spike**
   - connect a small OpenClaw setup to Paperclip only for supervision concepts such as budgets, heartbeat cadence, or dashboard visibility
   - do not let Paperclip own repo task state

3. **Optional Hermes spike**
   - test Hermes side-by-side on one clearly separated workflow
   - avoid shared task ownership
   - avoid shared-channel bridging unless that exact problem must be solved

## What not to prototype first

- full dual-control-plane orchestration
- shared default channel routing between Hermes and OpenClaw
- deep automation loops spanning OpenClaw, Paperclip, and Hermes simultaneously
- broad autonomous company simulations

## Decision gates

### Gate 1, OpenClaw baseline sufficiency

Question:
- Does OpenClaw alone already satisfy the practical need with acceptable operator overhead?

If yes:
- defer both Paperclip and Hermes integration

### Gate 2, Paperclip payoff

Question:
- Does portfolio-level supervision, budgeting, or multi-agent visibility create enough value to justify another server and UI layer?

If yes:
- test Paperclip as a management layer above OpenClaw

### Gate 3, Hermes payoff

Question:
- Is there a concrete workflow where Hermes' scheduling, remote persistence, or cross-platform continuity clearly outperforms staying inside OpenClaw?

If yes:
- test Hermes on that bounded workflow only

### Gate 4, bridge necessity

Question:
- Is a shared channel genuinely required, or merely interesting?

If no:
- avoid bridge complexity

## Recommended implementation order

1. strengthen the OpenClaw-only baseline
2. define explicit evaluation gates
3. run a Paperclip supervision spike only if operator-layer pain is real
4. run a Hermes side-by-side specialist spike only if a concrete workflow justifies it
5. revisit narrow service-style integration after evidence exists

## Bottom line

The best current architecture is a conservative layered model: OpenClaw first, Paperclip only above it if management-scale pain appears, and Hermes only beside it or behind it when a specific specialist capability is worth the complexity. The fallback is even simpler, stay OpenClaw-only until the need becomes undeniable.
