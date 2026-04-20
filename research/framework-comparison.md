# Framework Comparison

## Research objective

Compare practical multi-agent operating models and frameworks against Point's actual OpenClaw workflow, which values bounded orchestration, approval gates, durable artifacts, and clear operator control more than autonomous swarm breadth.

## Evaluation criteria

- OpenClaw fit
- support for durable state and resumability
- human oversight and approval control
- clarity of orchestration boundaries
- implementation complexity
- risk of replacing rather than extending OpenClaw

## Candidates

### 1. OpenClaw control-plane-first pattern

Summary:
- strongest direct fit for Point's current workflow
- already aligned with file-backed continuity, bounded delegated work, explicit approvals, and planning-versus-execution separation

Strengths:
- closest match to the operating model already in use
- durable state can live in files, memory notes, and repo-local planning bundles
- approval boundaries are explicit and reviewable
- does not require introducing another orchestration runtime just to coordinate work

Weaknesses:
- less turnkey than opinionated orchestration frameworks
- persistent delegated-worker support can depend on runtime/channel constraints
- operator tooling for budgets and dashboarding is thinner than Paperclip's company-layer model

Fit assessment:
- best default foundation

### 2. LangGraph

Summary:
- a low-level orchestration framework for long-running, stateful agents with durable execution and human-in-the-loop controls

Strengths:
- strongest general-purpose framework fit for explicit stateful orchestration
- good match when Point wants a programmable workflow graph around OpenClaw-adjacent logic
- durable execution and interruptibility align with approval-aware operations

Weaknesses:
- adds a separate orchestration substrate
- can pull the stack toward custom application development instead of lightweight operator control
- benefits are highest when building a system, not just running an agent workflow

Fit assessment:
- best external framework candidate when deeper orchestration is truly needed

### 3. Paperclip

Summary:
- not a core execution framework in the same sense as LangGraph, but a company-layer orchestration product with org charts, goals, budgets, heartbeats, and dashboarding

Strengths:
- strong operator-facing supervision story
- clearest option for budget tracking, team structure, and high-level goal management across multiple agents
- conceptually fits above OpenClaw rather than inside it

Weaknesses:
- can overlap with OpenClaw control-plane ownership if responsibilities are not sharply separated
- introduces another server, UI, and data layer
- best value appears at multi-agent fleet scale, not necessarily a small focused stack

Fit assessment:
- promising supervisory layer, not a default replacement for OpenClaw orchestration

### 4. Hermes Agent

Summary:
- a broader agent runtime with learning loop, persistent knowledge patterns, gateway reach, subagents, scheduling, and remote execution surfaces

Strengths:
- very capable agent runtime with broader native automation surfaces than Point's current OpenClaw posture
- attractive when remote persistence, built-in scheduling, or cross-platform continuity are primary requirements
- has active examples of coexistence with OpenClaw through bridge projects like HermesClaw

Weaknesses:
- more autonomous and memory-heavy by design than Point's current file-backed control-plane preference
- higher risk of overlap around gateway ownership, memory, scheduling, and delegation behavior
- easy to create operational ambiguity if both systems act as first-class orchestrators

Fit assessment:
- useful as a peer runtime or specialist system, risky as a blended co-owner of the same workflow

### 5. MetaGPT

Summary:
- software-company-style multi-agent framework built around explicit roles such as product manager, architect, and engineer

Strengths:
- strong for research into role-based software-company orchestration
- provides a clear structured team metaphor

Weaknesses:
- more opinionated and heavier than Point likely needs
- risks importing a role theater that duplicates the smaller OpenClaw control-plane model already working here
- stronger as inspiration than as the direct operating substrate

Fit assessment:
- useful reference model, weak primary recommendation

### 6. CAMEL

Summary:
- research-heavy multi-agent framework focused on large-scale agent behavior, tasks, and environments

Strengths:
- strong research value
- broad environment for experiments and agent-systems investigation

Weaknesses:
- not optimized for Point's main need, which is practical operator-ready orchestration
- higher research breadth than immediate implementation payoff

Fit assessment:
- background research source, not a leading implementation choice

### 7. AutoGen

Summary:
- established multi-agent framework, but now in maintenance mode with Microsoft steering new users toward Microsoft Agent Framework

Strengths:
- historically important and still useful for understanding patterns

Weaknesses:
- maintenance-mode status weakens it as a new core bet
- introduces framework churn risk immediately

Fit assessment:
- do not choose as the primary new foundation for this repo

## Comparative recommendation

### Best shortlist

1. OpenClaw control-plane-first pattern as the core
2. LangGraph as the strongest optional orchestration substrate if deeper programmable workflows become necessary
3. Paperclip as the strongest optional supervisory layer if operator dashboards, budgets, and org management become worth the added complexity
4. Hermes Agent as a bounded peer or specialist integration track, not a shared default control plane

### Current recommendation

- keep OpenClaw as the center
- treat LangGraph as the main "build-if-needed" orchestration candidate
- treat Paperclip as the top operator-layer candidate
- treat Hermes as an interoperability and specialization question, not a framework replacement question
- do not invest further in AutoGen as the main path

## What this means for the roadmap

- next, determine whether Paperclip adds enough operator leverage to justify a separate company layer
- then determine whether Hermes should integrate side-by-side, via bridge, or not at all for the first prototype
- only after those answers should the repo lock a target architecture

## Confidence and limits

This is a first-pass baseline built from public project descriptions, repo READMEs, and Point's current OpenClaw operating model. It is good enough to narrow the field, but not yet good enough for a final implementation commitment without deeper validation.
