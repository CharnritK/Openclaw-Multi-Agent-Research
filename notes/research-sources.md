# Research Sources

## OpenClaw-local context

- `/home/point/.openclaw/workspace/MULTI_AGENT_MODEL.md`
- `/home/point/.openclaw/AGENTS.md`
- `/home/point/.openclaw/workspace/docs/openclaw-managed-browser-skills.md`

## Upstream repositories and docs reviewed

- `paperclipai/paperclip`
- `rungerunge/paperclip-openclaw`
- `NousResearch/hermes-agent`
- `AaronWong1999/hermesclaw`
- `langchain-ai/langgraph`
- `FoundationAgents/MetaGPT`
- `camel-ai/camel`
- `microsoft/autogen`

## Evidence note

This repo started with README-level and public-documentation evidence for first-pass narrowing.

Deeper inspection now includes:
- Paperclip runtime and server-source review from `paperclipai/paperclip` local clone head `16b2b84`, covering heartbeat, task-workflow, workspace-runtime, and budget-enforcement surfaces
- Hermes runtime, gateway, session, cron, memory, and delegation review from `NousResearch/hermes-agent` local clone head `dcd763c`, covering practical narrow-use seams versus broad orchestration ownership

Bridge-runtime complexity has not been inspected to the same depth and remains intentionally deferred unless a real shared-channel requirement appears.
