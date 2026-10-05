# EXAMPLE ONLY — fictional AI Agent Audit excerpt

> This document is a **labelled fictional example** for the Aigov.consulting
> `aigov-ai-governance` plugin README / marketplace review.
> Organisation, systems, and findings are invented. Do not treat as a real audit.

# AI Agent Audit Report
**Classification:** Internal — draft governance assessment (EXAMPLE)
**Agent / system:** NordicOps Secretary v2.3 (fictional workplace agent)
**Audit date:** 2026-10-05 (Europe/Madrid)
**Scope:** Slack read + Gmail draft/send + Drive read; production tenant “demo-corp”

## 1. Executive summary

NordicOps Secretary drafts operational emails from Slack threads and can send via Gmail.
**Control Maturity Score: 48/100 (Developing).** Recommendation: **Go-with-conditions**.

| ID | Severity | One-line |
|---|---|---|
| F-01 | Critical | `gmail.send_message` callable without human approval |
| F-02 | High | Email bodies injected into planner without untrusted fence |
| F-03 | Medium | Logs lack approval fields; retention 14 days |

**7-day actions:** remove send scope; enforce L1 gate; publish kill-switch runbook.

## 6. Scoring worksheet (abbrev.)

| Domain | Points |
|---|---|
| Inventory | 8/10 |
| Action gates | 4/20 |
| Audit trail | 6/15 |
| Data protection | 9/15 |
| Injection resilience | 5/15 |
| Credentials | 8/10 |
| Kill-switch / IR | 5/10 |
| Oversight / evals | 3/5 |
| Critical deduction | −0 (would apply until F-01 closed; shown pre-deduction band Developing) |
| **Total** | **48** |

## 7. Regulatory snapshot (illustrative)

- Class: unclear — internal drafting aid vs possible Annex III employment use if applied to HR decisions → run `ai-act-classifier`.
- Role: **deployer** of third-party agent platform.
- If Annex III high-risk under Art 6(2): Ch III §§1–3 apply from **2 Dec 2027** ([Art 113(c)(i)](https://ai-act-service-desk.ec.europa.eu/en/ai-act/article-113), amended by Reg. (EU) 2026/1744).
- Art 50 transparency from **2 Aug 2026** if interacting with natural persons.

## 9. Disclaimer

Preliminary fictional illustration of report shape only.
