# Hermes Practical Boundary

## Objective

Test whether Hermes can be used narrowly as a specialist runtime or service without importing its broader memory and orchestration model into Point's stack.

## Short answer

Yes, but only **deliberately**.

The deeper evidence shows two things at once:
- Hermes is built as a broad full-stack agent runtime with first-class memory, session persistence, messaging gateway, cron delivery, and delegation
- but the runtime also exposes real controls for narrower use, including skipping memory/context injection, turning off session persistence, and running delegated child agents with isolated context and no shared memory writes

So the refined answer is:
- Hermes is **not** a naturally thin add-on around OpenClaw
- Hermes **can** still be used narrowly as a specialist runtime or service if Point keeps the boundary explicit
- the strongest narrow boundary is backend-style invocation or side-by-side specialization
- shared channel, gateway, and scheduling ownership remain the main ways Hermes would pull broader orchestration into the stack

## Evidence inspected

Primary deeper-evidence source: `NousResearch/hermes-agent` at local clone head `dcd763c`.

Key files inspected:
- `README.md`
- `AGENTS.md`
- `run_agent.py`
- `agent/prompt_builder.py`
- `hermes_state.py`
- `gateway/session.py`
- `gateway/run.py`
- `cron/jobs.py`
- `cron/scheduler.py`
- `tools/delegate_tool.py`

## Findings

### 1. Hermes is designed as a broad runtime, not a thin plugin

The top-level docs describe Hermes as one system that combines memory, skills, session search, gateway messaging, cron automation, delegation, and multiple execution backends.

Observed evidence:
- `README.md` describes Hermes as having a built-in learning loop, cross-session memory, multi-platform gateway reach, scheduled automations, and isolated subagents.
- `AGENTS.md` lays out these surfaces as core packages: `gateway/`, `cron/`, `hermes_state.py`, `tools/delegate_tool.py`, and the main runtime loop in `run_agent.py`.
- `README.md` also includes direct migration support from OpenClaw, including imported memories, skills, allowlists, messaging settings, and API keys.

Implication:
- Hermes should be treated as a broad adjacent runtime by default, not assumed to be a lightweight extension.

### 2. Memory and cross-session continuity are first-class defaults

Hermes does not treat memory as an optional afterthought. It is part of the default prompting and storage model.

Observed evidence:
- `agent/prompt_builder.py` explicitly tells the agent that it has persistent memory across sessions, that memory is injected into every turn, and that session search should be used for past-conversation recall.
- `hermes_state.py` defines a persistent SQLite state store for full message history, model configuration, and FTS5 session search across CLI and gateway sessions.
- `README.md` presents persistent memory, session search, and user modeling as headline capabilities rather than edge features.

Implication:
- If Point adopts Hermes casually, it will tend to import Hermes' own continuity model.
- This strengthens the caution against treating Hermes and OpenClaw as equal co-owners of the same long-lived task state.

### 3. Gateway and cron ownership are deeply integrated with Hermes session context

Hermes' messaging and scheduling model is not just an adapter shell. It carries session context, home-channel routing, and autonomous delivery semantics.

Observed evidence:
- `gateway/session.py` builds a `SessionContext` that explicitly includes source platform, connected platforms, home channels, and session metadata for prompt injection.
- `gateway/run.py` manages running agents per session, session model overrides, pending approvals, session-search support, and cron-related reset and delivery behavior.
- `cron/scheduler.py` says the gateway calls cron every 60 seconds, resolves delivery targets across platforms, and routes outputs to configured destinations.
- `cron/jobs.py` stores jobs and cron output under Hermes home and normalizes schedules, skills, and job metadata inside Hermes' own state model.

Implication:
- If Point uses Hermes for gateway ownership or unattended scheduling on the same workflow, Hermes is no longer just a specialist execution backend. It starts to own routing, delivery, and session semantics too.

### 4. Hermes still provides real controls for narrow usage

This is the most important disconfirming evidence against an overly negative reading.

Observed evidence:
- `run_agent.py` exposes `skip_memory`, `skip_context_files`, and `persist_session` in the core `AIAgent` constructor, alongside explicit session and platform parameters.
- `tools/delegate_tool.py` builds child agents with isolated context, restricted toolsets, `skip_context_files=True`, and `skip_memory=True`.
- The same delegation code blocks child access to `delegate_task` recursion and to shared `memory` writes, while keeping the child in its own conversation and terminal session.

Implication:
- Hermes does contain practical seams for narrow use.
- A bounded integration can disable or sidestep the broadest continuity features instead of accepting the whole Hermes operating model.

### 5. Narrow Hermes use is strongest when Hermes is treated as an explicit worker or service

The codebase makes narrow use more plausible when Hermes is invoked through a sharply defined boundary rather than through shared channels.

What the evidence supports:
- Hermes can plausibly act as a specialist worker with memory/context persistence reduced or disabled
- delegated or isolated runs can be constrained away from shared memory writes
- results can be returned as summaries without exposing the whole intermediate orchestration surface to the parent system

What the evidence does not support:
- casual shared ownership of one messaging surface, one session history, or one scheduler without architectural tension

Implication:
- backend-style invocation and side-by-side specialization look stronger after deeper inspection than they did from README-level material alone
- shared live control surfaces look weaker

### 6. OpenClaw migration support confirms overlap, not clean separation

Observed evidence:
- `README.md` includes `hermes claw migrate` and says Hermes can import OpenClaw settings, memories, skills, command allowlists, messaging settings, API keys, TTS assets, and workspace instructions.

Implication:
- Hermes clearly expects to be able to absorb large parts of the OpenClaw user environment.
- That is useful for switching, but it is also evidence of architectural overlap and collision risk if both systems stay equally primary.

## Recommendation impact

### What changed from the first-pass assessment

The first-pass read already favored Hermes as a side-by-side specialist runtime over shared orchestration.

The deeper evidence sharpens that into two stronger claims:
- the negative case is stronger: Hermes' gateway, cron, memory, and session model are more first-class than a light integration story would imply
- the positive narrow-use case is also stronger: Hermes exposes enough runtime controls that Point could deliberately use it as a constrained worker or service without inheriting every Hermes default

### Refined recommendation

#### Stronger confidence in these paths
- keep OpenClaw as the primary control plane
- treat Hermes first as a side-by-side specialist runtime
- treat backend-style Hermes invocation as the most promising future integration path if Point wants Hermes-specific capabilities

#### Stronger caution on these paths
- do not let Hermes and OpenClaw co-own the same live gateway, scheduler, memory surface, or long-running task workflow by default
- do not treat migration overlap as evidence that dual-primary coexistence will stay simple

## Practical boundary for Point

Hermes remains viable if Point keeps the boundary explicit.

### Cleanest narrow-use cases
- remote or persistent worker runtime owned by Hermes, with OpenClaw still owning task shaping and approvals
- specialist automation jobs where Hermes' cron or messaging strengths are valuable and the workflow is clearly assigned to Hermes
- explicit handoff or service-style invocation where Hermes returns results to OpenClaw without shared task-state ownership

### Warning signs that the boundary is getting too broad
- both systems replying on the same user-facing channel as equal brains
- both systems trying to maintain authoritative memory or session continuity for the same work
- Hermes cron/gateway becoming the real delivery path for workflows OpenClaw is still supposed to own
- migration-style reuse turning into quiet role replacement instead of intentional specialization

## Bottom line

The recommendation is **unchanged in direction, but more precise**.

Hermes is not a naturally narrow add-on. Its broad runtime surfaces are real and first-class. But unlike the most pessimistic reading, the source also shows credible seams for constrained use. That means Hermes still makes sense as a side-by-side specialist runtime or future backend-style service, while shared gateway or shared orchestration ownership should remain a strong default no-go.
