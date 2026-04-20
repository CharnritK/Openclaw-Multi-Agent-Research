# Architecture Review

## Verdict

The current research is solid enough to support the present recommendation.

That recommendation should now be stated with **medium confidence for architecture direction**, not as proof that any external integration should be implemented yet.

The stable conclusion is:
- keep OpenClaw central
- treat Paperclip as optional and only for workflows it explicitly owns
- treat Hermes as a bounded specialist runtime or future backend-style service
- defer shared-channel bridge work unless a real channel constraint appears

## What is solid

### 1. The core architecture direction is supported from multiple angles

The baseline comparison, first-pass integration notes, and both deeper boundary notes all converge on the same direction: OpenClaw is the best default center for Point's current workflow.

### 2. The Paperclip caution is now evidence-strong

The deeper Paperclip review materially strengthens the case that Paperclip is not a passive dashboard layer. It owns heartbeat execution, issue workflow, session continuity, and budget-enforced pausing for the work it manages. That makes it a poor fit as a casual wrapper around an already-active OpenClaw orchestration loop.

### 3. The Hermes recommendation is now more precise

The deeper Hermes review shows both real overlap and real seams. Hermes is broad enough to create ownership drift if adopted casually, but narrow enough to remain viable for clearly bounded specialist work. That supports side-by-side or backend-style use more strongly than the first-pass note did.

### 4. The prototype and decision gates are aligned with the evidence

The current gates already force new layers to beat the OpenClaw-only baseline with concrete payoff. That keeps future prototype work bounded and consistent with the research findings.

## Remaining weak spots

### 1. The Paperclip boundary needed tighter wording

The earlier phrase "management layer above OpenClaw" was slightly too clean. After deeper inspection, Paperclip should be described as owning the workflow surfaces it manages, not as a passive layer floating above an unchanged OpenClaw loop.

### 2. Hermes backend-style integration is still architectural, not prototyped

The research now supports Hermes as a plausible bounded worker or service, but it does not yet define the exact contract for inputs, outputs, failure handling, approvals, or state handoff. That is the main remaining gap if Hermes ever moves from optional idea to prototype candidate.

### 3. Bridge complexity remains underexplored in implementation detail

This is a known gap, but it is not a recommendation-critical gap yet. The current recommendation already says to avoid shared-channel bridges by default.

### 4. Some comparison surfaces remain first-pass level

The non-primary candidates remain baseline-level research. That is acceptable because none of them currently threaten the recommended direction enough to justify deeper work now.

## Bridge-depth decision

Shared-channel bridge complexity does **not** need a separate deeper inspection task yet.

Reason:
- the present recommendation already avoids bridges by default
- the architecture does not depend on proving bridges clean
- bridge details would become decision-critical only if a real shared-channel requirement emerges or a Hermes prototype must share a live user-facing surface with OpenClaw

So bridge deepening should stay deferred, not expanded preemptively.

## Next research questions

Only reopen deeper research if one of these becomes concrete:

1. **Hermes worker contract**
   - What exact service boundary would let OpenClaw invoke Hermes cleanly for one specialist workflow?

2. **Paperclip adoption trigger**
   - What concrete operator pain would justify letting Paperclip own any workflow surfaces at all?

3. **Real bridge requirement**
   - Is there an actual messaging-channel constraint that forces OpenClaw and Hermes onto the same account or thread?

## Bottom line

The research package is strong enough to hold the current recommendation without more broad exploration.

What remains is not a generic need for more research. It is a need for one future bounded question at a time, triggered by a real prototype or channel constraint.
