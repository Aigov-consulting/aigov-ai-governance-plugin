# Aigov AI Governance (v2) — Grok Build plugin

**Institutional control and audit of AI agents** for public-sector and enterprise deployers.

This plugin turns Grok Build into a governance workbench: inventory agent tools and permissions, force *decision-before-action* policies, classify systems under the EU AI Act (including Digital Omnibus dates), ready government pilots for scale, and draft DPIAs / contract redlines — with citations to primary law and standards.

**Author:** [Aigov.consulting](https://aigov.consulting) (Estonia)  
**Maintainer:** [@herboloid](https://github.com/herboloid)  
**License:** MIT  
**Plugin slug:** `aigov-ai-governance` (unchanged from v1 for marketplace continuity)  
**Version:** 2.0.0

## Why v2

v1 shipped four generic instruction skills. v2 is built around Aigov.consulting’s flagship strength: **accountable AI agents** — workplace bots, MCP-connected agents, Slack/Gmail copilots — with audit-grade structure, severity-rated findings, and verified regulatory dates.

## Skills

| Skill | Use when |
|---|---|
| **`agent-audit`** (flagship) | You need a structured audit of an AI agent / multi-agent setup: tools & permissions, autonomy, human approval gates, logging, data flows, prompt-injection exposure, credentials, kill-switch, evals — mapped to EU AI Act, NIST AI RMF, ISO/IEC 42001 themes, OWASP LLM & Agentic Top 10. |
| **`action-gate-policy`** | You need a *decision-before-action* policy: action classes, approval matrix, JSON audit-log schema, retention, incidents. |
| **`ai-act-classifier`** | Fast risk class (Art 5 / Annex I / Annex III / GPAI / Art 50 / minimal), role (provider/deployer/…), and application dates verified against Reg. (EU) 2026/1744. |
| **`public-sector-ai-readiness`** | A government buyer moves from pilot to scale: procurement, FRIA Art 27, records, oversight, lock-in, citizen explainability. |
| **`dpia-draft`** | GDPR DPIA draft for AI/agent processing (mailbox, chat, documents, model hosts). |
| **`contract-review`** | MSA / MoU / NDA / AI vendor offer — training-data use, roles, audit rights, agent scopes. |

**Removed in v2:** `funding-sandboxes` (diluted the agent-governance focus).  
**Renamed:** `ai-act-assessment` → `ai-act-classifier` (decision tree + verified Omnibus dates).

## What this plugin does **not** do

- No MCP servers, hooks, shell scripts, or network calls — **skills (markdown) only**.
- No credentials required; never paste secrets into prompts.
- Outputs are **preliminary working drafts**, not legal advice, not conformity assessment, not ISO certification.

## Example prompts

```text
Audit our Grok Team Bot that can read Slack, draft Gmail, and open GitHub PRs.
Produce a full agent-audit report with scoring.
```

```text
Draft an action-gate policy for a ministry ops agent that must never send
external email or delete files without human approval. Include the JSON log schema.
```

```text
Classify this hiring-screening assistant under the EU AI Act and list
application dates after the Digital Omnibus.
```

```text
We piloted a citizen chatbot in one municipality. Checklist to scale nationwide,
including FRIA and procurement clauses.
```

## Sample output (fictional example)

> **EXAMPLE ONLY — fictional organisation, fictional findings. Not a real audit.**

### Executive summary (excerpt)

**System:** “NordicOps Secretary” workplace agent (fictional)  
**Maturity score:** 48 / 100 — **Developing**  
**Recommendation:** **Go-with-conditions** — disable `gmail.send_message` and `drive.trash` until action gates land.

| ID | Severity | Finding |
|---|---|---|
| F-01 | Critical | External email send without human approval (OWASP LLM06; ASI02) |
| F-02 | High | Tool results from email bodies concatenated into planner without untrusted-content fence (LLM01; ASI01) |
| F-03 | Medium | Audit logs omit approver identity and retention &lt; 30 days (gap vs Art 26 logging practice for high-risk deployers) |

**Immediate actions (7 days):** revoke send scope; ship `action-gate-policy` Annex A = empty; enable kill-switch runbook.  
**Regulatory snapshot:** likely **not** Annex III solely as an internal drafting aid — confirm if used for employment evaluation (Annex III §4). Art 50 transparency may still apply if the bot interacts with natural persons. High-risk Annex III *obligations* (Ch III §§1–3), **if** classified high-risk under Art 6(2), apply from **2 Dec 2027** per Art 113(c)(i) as amended by Reg. (EU) 2026/1744 ([Service Desk Art 113](https://ai-act-service-desk.ec.europa.eu/en/ai-act/article-113)).

*— end of fictional example —*

## Install

In Grok Build, open `/plugin`, search for **aigov-ai-governance**, and install. Source repository: [Aigov-consulting/aigov-ai-governance-plugin](https://github.com/Aigov-consulting/aigov-ai-governance-plugin). Catalog: [xAI plugin marketplace](https://github.com/xai-org/plugin-marketplace).

## Security

Markdown skill instructions only. No executable components, no `postinstall`, no telemetry, no secret reads. Declared network endpoints: **none**.

## Attribution

Built and maintained by [Aigov.consulting](https://aigov.consulting) for public use under MIT.
