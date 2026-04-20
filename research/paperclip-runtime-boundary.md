# Paperclip Runtime Boundary

## Objective

Test whether Paperclip is truly a clean management layer above OpenClaw, or whether it acts as a stronger co-orchestrator than first-pass materials suggested.

## Short answer

Paperclip is **not** just a passive management dashboard.

The deeper evidence shows that Paperclip defines and enforces a real orchestration contract around:
- heartbeat-driven execution
- task and issue ownership
- checkout rules
- wake triggers
- session persistence
- run liveness and continuation behavior
- budget-enforced pausing

At the same time, it does **not** fully own runtime-service management. Its current workspace model keeps runtime services manually controlled rather than heartbeat-managed.

So the refined answer is:
- Paperclip is stronger than a thin governance layer
- but it is still not trying to own every runtime concern
- the cleanest use is as the top-level company/task operating system for agents it manages
- it is a worse fit as a light supervisory shell wrapped around an already-orchestrating OpenClaw workflow

## Evidence inspected

Primary deeper-evidence source: `paperclipai/paperclip` at local clone head `16b2b84`.

Key files inspected:
- `docs/agents-runtime.md`
- `docs/guides/agent-developer/how-agents-work.md`
- `docs/guides/agent-developer/heartbeat-protocol.md`
- `docs/guides/agent-developer/task-workflow.md`
- `docs/guides/board-operator/managing-tasks.md`
- `docs/guides/board-operator/costs-and-budgets.md`
- `docs/guides/board-operator/execution-workspaces-and-runtime-services.md`
- `server/src/services/heartbeat.ts`
- `server/src/services/budgets.ts`
- `server/src/services/issues.ts`

## Findings

### 1. Paperclip owns the heartbeat execution model

Paperclip's runtime guide says agents do not run continuously. They run in heartbeats, and each heartbeat starts the configured adapter, passes prompt and context, captures results, and updates the UI.

This matters because heartbeat scheduling is not just monitoring. It is the execution loop.

Observed evidence:
- `docs/agents-runtime.md` says agents run in heartbeat-triggered execution windows and can wake on timer, assignment, on-demand, or automation.
- `docs/guides/agent-developer/how-agents-work.md` says Paperclip calls the adapter, the adapter spawns the runtime, and the agent then uses Paperclip APIs during the run.
- `server/src/services/heartbeat.ts` contains the central run service, active-run tracking, sessioned local adapters, wake metadata, and run liveness continuation machinery.

Implication:
- Paperclip is directly in the execution path, not just observing another system's execution.

### 2. Paperclip owns task workflow semantics

The heartbeat protocol and task workflow guides define a specific issue lifecycle and require Paperclip-managed checkout before work starts.

Observed evidence:
- `docs/guides/agent-developer/heartbeat-protocol.md` requires `GET /api/companies/{companyId}/issues`, `POST /api/issues/{issueId}/checkout`, `PATCH /api/issues/{issueId}`, and child issue creation through Paperclip APIs.
- The same guide states issue status remains authoritative for workflow and that continuations re-wake the same assigned agent when policy allows.
- `docs/guides/board-operator/managing-tasks.md` says issues are the unit of work and form a hierarchy that traces back to company goals.
- `server/src/services/issues.ts` codifies the issue status model: `backlog`, `todo`, `in_progress`, `in_review`, `blocked`, `done`, `cancelled`.

Implication:
- Paperclip is not merely passing high-level goals to an external orchestrator. It expects work to flow through its own issue system and checkout rules.

### 3. Paperclip owns agent identity, wake context, and session continuity

Paperclip injects runtime identity and wake-specific context into the agent and persists session state across heartbeats.

Observed evidence:
- `docs/guides/agent-developer/how-agents-work.md` documents runtime variables like `PAPERCLIP_AGENT_ID`, `PAPERCLIP_API_URL`, `PAPERCLIP_API_KEY`, `PAPERCLIP_TASK_ID`, and approval-related wake context.
- `docs/agents-runtime.md` and `docs/guides/agent-developer/how-agents-work.md` both describe saved session IDs and automatic session reuse.
- `server/src/services/heartbeat.ts` tracks `sessionIdBefore`, `sessionIdAfter`, and explicitly treats several local adapters as sessioned runtimes.

Implication:
- Paperclip is shaping agent continuity and task context directly. That is stronger than a detached oversight layer.

### 4. Paperclip enforces budget behavior operationally, not just analytically

Budget handling is not just reporting. Paperclip auto-pauses agents and can cancel work in response to budget policy.

Observed evidence:
- `docs/guides/board-operator/costs-and-budgets.md` says 100 percent budget usage results in a hard stop and auto-paused agent with no more heartbeats.
- `server/src/services/budgets.ts` updates agent, project, or company pause state for budget reasons and provides `pauseAndCancelScopeForBudget`.

Implication:
- Paperclip has real operational control over whether work continues.

### 5. Paperclip does not fully own runtime-service lifecycle

This is the main limiting counterweight.

Observed evidence:
- `docs/guides/board-operator/execution-workspaces-and-runtime-services.md` says workspace commands are manually controlled from the UI.
- The same guide says Paperclip does not automatically start or stop workspace services during issue execution and does not auto-restart them on server boot.
- It still resolves execution workspaces during heartbeats, but describes that as code-location and session-continuity handling rather than runtime-service control.

Implication:
- Paperclip is not a total runtime platform in the strongest sense.
- It is strongest in task, heartbeat, coordination, and governance ownership, while leaving some runtime service control manual.

## Recommendation impact

### What changed from the first-pass assessment

The first-pass read left room to describe Paperclip as a relatively clean management layer above OpenClaw.

The deeper evidence narrows that claim.

A more accurate statement is:
- Paperclip can sit above OpenClaw only if OpenClaw is treated as a Paperclip-managed agent runtime or endpoint
- Paperclip is a poor fit as a thin supervisory wrapper around an already-active OpenClaw control plane that still wants to own task decomposition, wake logic, status flow, and durable execution context for the same work

## Refined recommendation

### Still valid
- keep Paperclip optional, not required
- do not adopt it for Point's current repo-centered OpenClaw workflow by default
- avoid shared orchestration between Paperclip and OpenClaw on the same unit of work

### Stronger caution now
- if Paperclip is adopted, let it own the company-level task system, heartbeats, budget controls, and issue workflow for the agents it manages
- do not try to let both Paperclip and OpenClaw act as first-class orchestrators over the same tasks

### Why the recommendation is still not a full rejection
- Paperclip's runtime model is opinionated, but coherent
- it may still be valuable when Point wants a genuine company-level operating system for many agents, budgets, and goal hierarchies
- the workspace-service model is less invasive than a fully automated runtime owner, which leaves some room for selective coexistence

## Bottom line

The recommendation is **unchanged in direction but strengthened in confidence**.

Paperclip is less like a lightweight oversight layer than the README-level read suggested. It is a real orchestration system for heartbeats, issues, sessions, and budget-enforced execution. That makes it more useful when Point wants to hand company-level coordination to Paperclip, and less suitable as a thin layer above an already-orchestrating OpenClaw workflow.
