---
name: resolve-ai
description: Use when building or reviewing Àríyá, Re:Solve AI provider/gateway behavior, AI tools, AI drafting/summaries/analysis, AI actions, usage/audit, or optional Portal AI experiences.
---

# Àríyá / Re:Solve AI

Read `04-ai/re-solve-ai.md`, `04-ai/ariya-experience.md`, Action Registry, data provenance, Knowledge, Vault, API/MCP and security rules.

## Identity
The user-facing assistant is **Àríyá**. Internal technical names may remain AIProvider, AIRun, AITool, AIProfile, etc.

Àríyá is native Re:Solve intelligence and remains separate from Chatwoot Captain.

## Permission rule
Àríyá never expands caller authority. Retrieval, summaries and tool execution must use caller-aware services and perform fresh authorization at action time.

## Evidence
When answering from business data, show usable source references/deep links and freshness where material. Clearly distinguish deterministic facts, connector-derived data and AI inference.

## Tools/actions
Prefer controlled registered Actions/tools. Reads and writes have explicit schemas/scopes/risk. Writes require confirmation; sensitive actions may require approval/step-up. Àríyá must not have arbitrary SQL, filesystem or provider access.

## Vault/sensitive data
No generic Vault secret retrieval. Confidential files are processed only when explicit policy and user authorization allow it. Minimize provider payloads and redact irrelevant sensitive information.

## Experience
Use strong TopBar/Command/contextual entry and a dedicated assistant workspace/panel. Avoid the generic floating purple sparkle bubble. Preserve current record/context awareness without scraping inaccessible page content.

## Drafting
Proposal text, project updates, emails, knowledge and other writing remain drafts until a human sends/publishes unless an explicitly approved automation says otherwise.

## Portal
Portal Àríyá is optional and separately scoped to client-visible data. Never expose internal notes, hidden financials, other organisations, unreleased documents or Vault secrets.

## Reliability/usage
Handle provider/model unavailable, timeout, budget, denied tool, invalid output and partial-source states. Track provider/model/usage/cost where available, tool calls, outcome and safe audit metadata without retaining sensitive prompts indefinitely.

## Completion
Verify permission-negative paths, evidence/freshness, fact-vs-inference language, write confirmations, Chatwoot Captain separation, provider abstraction, and a useful non-gimmicky UI.