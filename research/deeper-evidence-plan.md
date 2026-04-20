# Deeper Evidence Plan

## Objective

Identify the smallest set of deeper inspections that could materially change the current architecture recommendation.

## Why this exists

The current recommendation is strong enough to narrow choices, but still relies heavily on README-level evidence. The next research loop should target only the questions that could change the recommended path.

## Decision-sensitive unknowns

### 1. Paperclip runtime boundary

Open question:
- In real operation, how strongly does Paperclip assume ownership of orchestration versus acting as a pure management layer?

Why it matters:
- if Paperclip is cleaner as a high-level governance layer than it currently appears, adoption becomes more attractive
- if it strongly co-owns execution, it becomes a worse fit for Point

Evidence to inspect next:
- architecture and runtime docs
- agent heartbeat behavior
- how tasks, tickets, and governance map to external agents
- where state is expected to live

### 2. Hermes practical integration boundary

Open question:
- Which Hermes capabilities can be used narrowly without importing its whole memory-and-orchestration model into the stack?

Why it matters:
- if Hermes can be used cleanly as a specialist runtime or service, it becomes a stronger future option
- if it assumes broad ownership, deferral remains the right choice

Evidence to inspect next:
- integration and architecture docs
- messaging gateway ownership model
- subagent and scheduling boundaries
- migration and memory behavior relevant to coexistence with OpenClaw

### 3. Bridge complexity versus value

Open question:
- In practice, are shared-channel bridges like HermesClaw thin enough to stay operationally sane, or do they become hidden orchestration layers?

Why it matters:
- if bridges stay truly thin, they are viable only for channel constraints
- if they become operationally thick, they should stay a last resort

Evidence to inspect next:
- HermesClaw install and runtime details
- how routing ownership is expressed
- failure and maintenance burden

## Priority order

### Priority 1
- Paperclip runtime boundary
- Hermes practical integration boundary

Reason:
- either one could materially change the recommended architecture or future prototype order

### Priority 2
- bridge complexity versus value

Reason:
- important only if a shared-channel constraint becomes real

## Evidence rules

- prefer architecture docs, config surfaces, and runtime behavior over marketing pages
- inspect only what could change the recommendation
- keep explicit notes on what would count as disconfirming evidence
- avoid broad framework wandering that does not move a decision

## Recommended next unit

First deeper inspection target should be **Paperclip runtime boundary**, because it is the strongest candidate optional layer and the largest remaining ambiguity in the current recommendation.

## Stop conditions

Stop a deeper inspection when:
- the evidence no longer seems decision-relevant
- the finding would not change the recommendation
- the inspection starts expanding into implementation work

## Bottom line

The next research loop should not be broad. It should answer one question first: whether Paperclip is genuinely a clean supervision layer above OpenClaw, or whether it pulls too hard toward co-owning orchestration.
