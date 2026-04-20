# Decision Evidence Map

## Purpose

Centralize the major architecture claims, the strength of the current evidence, the main disconfirming evidence, and the exact trigger that would justify reopening each question.

## Claim 1

- claim: `OpenClaw should remain the primary control plane.`
- current verdict: `Accepted and unchanged.`
- evidence strength: `High for current workflow fit.`
- source class: `Repo-local planning bundle, framework comparison, and architecture synthesis.`
- inspected refs:
  - `research/framework-comparison.md`
  - `research/recommended-architecture.md`
  - `research/architecture-review.md`
  - `docs/planning/openclaw-multi-agent-research/DECISIONS.md`
- counterevidence:
  - `External runtimes offer stronger built-in dashboards, budgets, scheduling, and remote persistence.`
- remaining gap:
  - `This is a directional architecture verdict, not proof that OpenClaw alone covers every future workflow.`
- next trigger:
  - `A concrete workflow becomes materially constrained by the OpenClaw-only baseline.`

## Claim 2

- claim: `Paperclip should stay optional and must not co-own the same repo task flow as OpenClaw.`
- current verdict: `Accepted and strengthened.`
- evidence strength: `Medium-high.`
- source class: `First-pass Paperclip comparison plus deeper upstream docs and server-source review.`
- inspected refs:
  - `research/paperclip-integration.md`
  - `research/paperclip-runtime-boundary.md`
  - `paperclipai/paperclip/docs/agents-runtime.md`
  - `paperclipai/paperclip/docs/guides/agent-developer/heartbeat-protocol.md`
  - `paperclipai/paperclip/server/src/services/heartbeat.ts`
  - `paperclipai/paperclip/server/src/services/issues.ts`
- counterevidence:
  - `Paperclip does not fully own workspace runtime-service lifecycle, which leaves some coexistence room.`
- remaining gap:
  - `The repo still needed one concrete workflow trigger before reopening a Paperclip spike.`
- next trigger:
  - `Portfolio-level oversight, budget governance, and cross-workstream visibility become concrete operator pain at the same time.`

## Claim 3

- claim: `Paperclip is justified only for portfolio supervision, not as a thin wrapper above active OpenClaw repo orchestration.`
- current verdict: `Accepted with explicit trigger conditions.`
- evidence strength: `Medium.`
- source class: `Paperclip architecture notes, runtime-boundary findings, and decision gates.`
- inspected refs:
  - `research/paperclip-adoption-trigger.md`
  - `research/paperclip-integration.md`
  - `research/paperclip-runtime-boundary.md`
  - `research/validation-and-decision-gates.md`
- counterevidence:
  - `If Paperclip later proves it can add value without inheriting issue and heartbeat ownership, the boundary could soften.`
- remaining gap:
  - `No live supervision spike has been run.`
- next trigger:
  - `At least two Gate B conditions become concrete within one operating period.`

## Claim 4

- claim: `Hermes should stay a bounded specialist runtime rather than a blended co-owner of the same workflow.`
- current verdict: `Accepted and made more precise.`
- evidence strength: `Medium-high.`
- source class: `First-pass Hermes comparison plus deeper runtime, gateway, cron, memory, and delegation review.`
- inspected refs:
  - `research/hermes-integration.md`
  - `research/hermes-practical-boundary.md`
  - `NousResearch/hermes-agent/agent/prompt_builder.py`
  - `NousResearch/hermes-agent/hermes_state.py`
  - `NousResearch/hermes-agent/gateway/run.py`
  - `NousResearch/hermes-agent/cron/scheduler.py`
- counterevidence:
  - `Hermes exposes skip-memory, skip-context-files, persist-session, and isolated delegation controls that support narrower use.`
- remaining gap:
  - `The exact specialist contract was previously architectural rather than explicit.`
- next trigger:
  - `One workflow clearly benefits from remote persistence, scheduling, or specialist runtime behavior that OpenClaw alone does not cover as well.`

## Claim 5

- claim: `A Hermes backend-style worker contract is cleaner than shared-channel or shared-memory coexistence.`
- current verdict: `Accepted as the strongest future Hermes reopen path.`
- evidence strength: `Medium.`
- source class: `Hermes practical-boundary findings and the new worker-contract note.`
- inspected refs:
  - `research/hermes-worker-contract.md`
  - `research/hermes-practical-boundary.md`
  - `research/architecture-review.md`
  - `NousResearch/hermes-agent/run_agent.py`
  - `NousResearch/hermes-agent/tools/delegate_tool.py`
- counterevidence:
  - `Shared-channel bridges solve a real problem when channel constraints are unavoidable.`
- remaining gap:
  - `No live remote watcher prototype has been executed.`
- next trigger:
  - `A bounded remote watcher workflow becomes worth running and can stay outside shared gateway ownership.`

## Claim 6

- claim: `Shared-channel bridge work should stay deferred unless a real channel constraint becomes non-negotiable.`
- current verdict: `Accepted and unchanged.`
- evidence strength: `Medium.`
- source class: `Architecture review, validation gates, and research source notes.`
- inspected refs:
  - `research/architecture-review.md`
  - `research/validation-and-decision-gates.md`
  - `notes/research-sources.md`
- counterevidence:
  - `Bridge repos already demonstrate practical routing patterns for specific channels.`
- remaining gap:
  - `Bridge-runtime complexity has not been inspected as deeply as Paperclip and Hermes.`
- next trigger:
  - `One messaging account must reach both systems and separate channels are operationally unacceptable.`

## Bottom line

The architecture is now traceable at the claim level. Further research should reopen only when one of the `next trigger` conditions becomes concrete, not when generic framework curiosity returns.
