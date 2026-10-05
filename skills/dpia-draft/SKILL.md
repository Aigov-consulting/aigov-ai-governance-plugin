---
name: dpia-draft
description: >-
  Use when drafting a GDPR data protection impact assessment (DPIA) for an
  AI system or AI agent that processes personal data — including workplace
  agents with mailbox, chat, or document access.
---

# DPIA draft (AI / agent-aware)

Author: Aigov.consulting (https://aigov.consulting). Maintainer: GitHub herboloid.

Produce a **draft DPIA** aligned to GDPR Articles 35–36. Final sign-off belongs to the controller's DPO / data-protection lead. **Not legal advice.**

## Primary sources

- GDPR (Reg. (EU) 2016/679): https://eur-lex.europa.eu/eli/reg/2016/679/oj — Arts 5, 6, 9, 32, 35, 36
- WP29/EDPB DPIA guidelines (WP248 rev.01): https://www.edpb.europa.eu/our-work-tools/our-documents/guidelines/guidelines-data-protection-impact-assessment-dpia-and_en
- AI Act interaction: deployer may use AI Act Art 13 info to support GDPR DPIA ([Art 26(9)](https://ai-act-service-desk.ec.europa.eu/en/ai-act/article-26)); FRIA under [Art 27](https://ai-act-service-desk.ec.europa.eu/en/ai-act/article-27) is complementary — do not conflate the two.

## Agent-specific issues to cover

When the system is an agent with tools:

- Which mailboxes, drives, tickets, or CRM objects are readable?
- Are message bodies / attachments ingested into model context or long-term memory?
- Can the agent send external messages or write back to systems of record?
- Prompt-injection leading to unauthorized disclosure (map to GDPR confidentiality breach risk)
- Training / fine-tuning / vendor improvement use of personal data
- Sub-processors (model host, MCP SaaS, email API)

## Workflow

1. Describe processing: purposes, categories of data subjects, personal data categories, sources, recipients, international transfers, retention, assets (models, stores, logs).
2. Necessity & proportionality vs stated public/enterprise purpose.
3. Lawful basis (Art 6); special categories (Art 9) if any.
4. Risk register: for each risk — threat, affected rights, likelihood, severity, existing controls, residual risk.
5. Measures: minimisation, purpose binding, access control, encryption, DLP, action gates, redaction in logs, processor Art 28 terms, retention, injection defenses.
6. Consult DPO; decide if prior consultation (Art 36) is needed (high residual risk).
7. Mark **DRAFT**; controller decides whether to proceed.

## Risk catalogue (seed — adapt)

| Risk ID | Example |
|---|---|
| R1 | Excessive collection from mailbox/Drive beyond purpose |
| R2 | Disclosure via agent send tools (wrong recipient / prompt injection) |
| R3 | Special-category inference (health, political, etc.) |
| R4 | Unlawful transfer to model provider outside adequate safeguards |
| R5 | Retention of prompts/logs beyond necessity |
| R6 | Automated decision with legal/similar effect lacking Art 22 safeguards |
| R7 | Re-identification from embeddings or eval sets |

## Output structure

```markdown
# DPIA — DRAFT — [System name]

## A. Document control
Version, author, DPO reviewer, status=DRAFT

## B. Processing description
## C. Lawful basis & special categories
## D. Necessity & proportionality
## E. Risks to rights and freedoms
(table)
## F. Measures and residual risk
## G. Consultation & Art 36 decision
## H. Link to AI Act FRIA / classification (if any)
## I. Sign-off block (controller)

Disclaimer: draft only; not a determination of GDPR compliance.
```

## Quality rules

- Cite GDPR articles for legal claims.
- Do not invent supervisory-authority positions.
- Prefer concrete data flows over abstract "AI risk" language.
- If FRIA likely required, say so and point to `public-sector-ai-readiness` / Art 27 — do not replace FRIA with this DPIA.
