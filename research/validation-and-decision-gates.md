# Validation and Decision Gates

## Purpose

Convert the research into explicit pass, fail, or defer criteria so the next prototype spike can be chosen without reopening the whole architecture debate.

## Default baseline

The default baseline remains:
- OpenClaw-only workflow
- repo-local planning bundle
- modular task-level commit discipline
- no added Paperclip or Hermes dependency unless a concrete payoff appears

Any added layer must beat this baseline clearly enough to justify complexity.

## Gate set

### Gate A, keep OpenClaw-only or expand?

Pass condition for staying OpenClaw-only:
- current workflow remains understandable and controllable
- lack of Paperclip does not create painful operator blind spots
- lack of Hermes does not block an important workflow
- no urgent need exists for shared dashboarding, budget controls, or long-lived remote runtime behavior

Expansion trigger:
- at least one concrete workflow is materially constrained by the OpenClaw-only baseline

If no clear trigger exists:
- defer expansion

## Paperclip decision gates

### Gate B, should Paperclip be prototyped?

Prototype Paperclip only if at least two of these are true:
- multiple active agents or companies need one management surface
- cost governance or per-agent budgets matter operationally
- top-level visibility is missing and actively painful
- the user wants org-level delegation and governance beyond repo-local planning

Defer Paperclip if any of these are true:
- work is still centered on one primary OpenClaw workflow
- cost governance is not yet a real issue
- Paperclip would mostly duplicate task state already handled by OpenClaw
- the extra Node server, database, and UI would add more overhead than relief

Successful Paperclip spike means:
- Paperclip improves visibility or governance without taking ownership of OpenClaw repo tasks
- budgets, dashboarding, or high-level heartbeats provide obvious operator value
- the team can describe the Paperclip/OpenClaw boundary in one sentence

Failed Paperclip spike means:
- control-plane ownership becomes ambiguous
- Paperclip and OpenClaw duplicate orchestration work
- operator overhead increases instead of dropping

## Hermes decision gates

### Gate C, should Hermes be prototyped?

Prototype Hermes only if at least one high-value workflow clearly benefits from:
- long-lived remote execution
- stronger built-in scheduling and unattended operation
- cross-platform gateway continuity
- specialist runtime behavior that OpenClaw does not target as well

Defer Hermes if any of these are true:
- the main workload remains repo-local and approval-heavy
- the benefit is only theoretical or curiosity-driven
- introducing Hermes would create two competing memory or control-plane models without a clear boundary
- shared-channel operation is not actually required

Successful Hermes spike means:
- Hermes owns one bounded specialist workflow cleanly
- OpenClaw remains the primary control plane
- the operator can say exactly why Hermes is present and what it alone owns

Failed Hermes spike means:
- task ownership becomes blurry
- the same workflow starts bouncing between Hermes and OpenClaw
- the integration needs a bridge before a real need exists

## Bridge decision gate

### Gate D, is a shared-channel bridge necessary?

Prototype a bridge such as HermesClaw only if:
- one messaging account must reach both systems
- separate channels are not acceptable operationally
- the routing complexity is justified by real channel constraints

Defer bridge work if:
- separate channels or separate workflows are acceptable
- the bridge is only interesting as a demo
- failure analysis and ownership would become harder than the channel benefit is worth

Successful bridge spike means:
- channel conflict is actually resolved
- routing ownership remains explicit
- bridge logic stays thin and operationally understandable

Failed bridge spike means:
- debugging complexity increases sharply
- users cannot tell which system is handling what
- bridge behavior becomes part of the product instead of a narrow workaround

## Prototype selection rule

Choose the first prototype spike using this order:
1. stay OpenClaw-only if no strong trigger exists
2. Paperclip spike only if operator-layer pain is already real
3. Hermes spike only if a specific specialist workflow clearly benefits
4. bridge spike only if shared-channel constraints are unavoidable

## Current recommendation

Based on current evidence, the best next action is:
- keep OpenClaw-only as the live baseline
- defer Paperclip until operator-level scaling pain is concrete
- defer Hermes until one specialist workflow justifies it
- defer bridge work unless a shared-channel requirement becomes non-negotiable

## Bottom line

OpenClaw-only remains the control case. Paperclip, Hermes, and bridge work each need to beat that control case with a concrete operational payoff, not just possibility value.
