# SPEC

## Real problem

Point does not need a generic multi-agent hype stack. He needs a practical research and decision surface for choosing a small, controllable, auditable multi-agent architecture that keeps OpenClaw as the working center while selectively adding Paperclip and Hermes where they create real leverage.

## Clarified spec

Create a research roadmap and living research workspace that:
- defines the objective, approach, and success criteria
- compares relevant multi-agent frameworks against Point's actual operating model
- studies Paperclip integration as a supervisory or management layer
- studies Hermes Agent integration as a peer, bridge, or specialized-runtime path
- produces a prioritized implementation and validation checklist
- supports continued research in modular increments with regular commits

## Hard requirements

- keep OpenClaw central to the final recommendation
- optimize for bounded orchestration, approval gates, durable artifacts, and human oversight
- prefer file-backed continuity over opaque autonomous memory systems
- distinguish planning from execution
- keep recommendations practical, not just academically interesting
- capture decisions, risks, assumptions, and next steps in canonical files
- use modular task-level Git commits

## Exploration space

- which external orchestration framework, if any, should sit above OpenClaw
- whether Paperclip should be used for budgeting, heartbeat scheduling, org-chart coordination, or not at all
- whether Hermes should be bridged at the gateway, tool, skill, or channel level
- whether a reference implementation should stay documentation-first or progress into a thin prototype
- which evaluation criteria matter most: durability, observability, approval control, cost governance, or UX simplicity

## Non-goals / out of scope

- building a full production agent platform in this repo
- replacing OpenClaw with another framework
- broad autonomous loops without explicit approval
- deep benchmark chasing unrelated to Point's usage
- implementing every possible integration path

## Open questions and assumptions

### Open questions
- Does Point want Paperclip mainly as operator dashboard, company layer, or task orchestration engine?
- Does Hermes need to share channels with OpenClaw, or is side-by-side capability enough?
- Should the first prototype target Discord, WeChat, webchat, or a neutral local environment?
- How much operational complexity is acceptable in exchange for better delegation and supervision?

### Assumptions
- OpenClaw remains the primary working environment and decision surface.
- Research should favor minimal additional infrastructure.
- A good outcome is a short list of viable architectures with one recommended path and one fallback path.
- The repo should serve as a durable working notebook, not just a one-time report.
