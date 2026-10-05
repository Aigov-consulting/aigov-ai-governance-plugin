---
name: public-sector-ai-readiness
description: >-
  Use when a government or public-sector buyer moves an AI pilot to scale:
  procurement clauses, accountability, FRIA Art 27, records, human oversight,
  vendor lock-in, and explainability to citizens.
---

# Public-sector AI readiness (pilot → scale)

Author: Aigov.consulting (https://aigov.consulting). Maintainer: GitHub herboloid.

Produce a **readiness checklist and gap report** for a public body (ministry, agency, municipality, EU institution, or public-service provider) moving from AI pilot to production scale. Preliminary governance aid — **not** legal advice.

## Context

Public deployers face heightened accountability: fundamental rights, transparency to residents, procurement constraints, and — for many high-risk uses — FRIA and registration duties. Agentic tools (workplace bots with mailbox/document access) amplify oversight and logging needs.

## Primary citations

- AI Act Art 26 deployers: https://ai-act-service-desk.ec.europa.eu/en/ai-act/article-26
- AI Act Art 27 FRIA: https://ai-act-service-desk.ec.europa.eu/en/ai-act/article-27
- AI Act Art 49 registration: https://ai-act-service-desk.ec.europa.eu/en/ai-act/article-49
- AI Act Art 50 transparency: https://ai-act-service-desk.ec.europa.eu/en/ai-act/article-50
- AI Act Art 4 literacy: https://ai-act-service-desk.ec.europa.eu/en/ai-act/article-4
- AI Act Art 86 right to explanation of individual decision-making (where applicable): https://ai-act-service-desk.ec.europa.eu/en/ai-act/article-86
- Timeline / Digital Omnibus dates: https://ai-act-service-desk.ec.europa.eu/en/ai-act/timeline/timeline-implementation-eu-ai-act
- GDPR DPIA Art 35 (EUR-Lex): https://eur-lex.europa.eu/eli/reg/2016/679/oj
- NIST AI RMF: https://doi.org/10.6028/NIST.AI.100-1

## Workflow

1. Capture the pilot: purpose, population affected, data classes, vendor, connectors, decision influence (inform / recommend / decide).
2. Run a quick risk screen — point to `ai-act-classifier` for formal class; note Art 5 red flags early.
3. Score each checklist domain: **Met / Partial / Missing / N/A** with evidence.
4. Produce a scale-up plan: blockers, procurement clauses, owners, dates aligned to AI Act milestones.
5. Recommend `agent-audit` before enabling send/publish/delete tools on citizen or staff data.

## Readiness checklist

### 1. Accountability & governance

- [ ] Named senior accountable owner (not only the vendor)
- [ ] Decision rights: what the AI may not decide alone
- [ ] AI literacy plan for staff who oversee or work with the system (Art 4)
- [ ] Oversight roles competent and documented (Art 26; Art 14 design expectations if high-risk)
- [ ] Escalation path to DPO / fundamental-rights officer / ethics board

### 2. Lawful basis, DPIA, FRIA

- [ ] GDPR lawful basis mapped for each processing purpose
- [ ] DPIA completed or updated for high-risk processing (GDPR Art 35)
- [ ] FRIA assessed under Art 27 where deployer is a public-law body / public-service provider / listed Annex III cases — https://ai-act-service-desk.ec.europa.eu/en/ai-act/article-27
- [ ] FRIA template notified to market surveillance authority when required (Art 27(3))
- [ ] Special-category data minimised or excluded with justification

### 3. Procurement & vendor management

- [ ] Contract states AI Act roles (provider vs deployer) and cooperation duties
- [ ] Technical documentation / instructions for use deliverables (Art 13-related information flow)
- [ ] Audit rights, log access, subcontracting transparency
- [ ] Security incident and serious-incident notification timelines
- [ ] Exit: data return/deletion, model/prompt portability, transition assistance
- [ ] No silent training on public-body or citizen data without written authorisation
- [ ] SLA for human fallback when the AI is unavailable
- Cross-link `contract-review` for redlines.

### 4. Human oversight & citizen interface

- [ ] Human review for adverse or legally significant outcomes
- [ ] Staff can override / disregard AI output; overrides logged
- [ ] Citizens informed when subject to Annex III high-risk decision support (Art 26(11)) where applicable
- [ ] Art 50 notices when interacting with AI or consuming deepfakes / certain synthetic content
- [ ] Channel for complaints / explanation requests (consider Art 86)

### 5. Records, logging, monitoring

- [ ] Logs of use, overrides, and incidents retained per policy (≥ 6 months where Art 26 applies)
- [ ] Change control for prompts, tools, models
- [ ] Post-market style monitoring even for non-high-risk (good practice; required pattern for high-risk providers under Art 72)
- [ ] Metrics: error rates, bias proxies, escalation volume, citizen complaints

### 6. Security & agent controls

- [ ] Action-gate policy for any agentic connectors (`action-gate-policy`)
- [ ] Prompt-injection handling for inbound citizen email/forms
- [ ] Secrets not embedded in prompts; least-privilege integrations
- [ ] Tested kill-switch and credential revocation

### 7. Vendor lock-in & sovereignty

- [ ] Data residency / transfer mechanism documented
- [ ] Export formats for cases, prompts, evaluation sets
- [ ] Multi-cloud or exit-tested backup for critical citizen services
- [ ] Open standards preferred for logs and documents

### 8. Explainability & transparency to the public

- [ ] Plain-language description of purpose, data, and human role published where appropriate
- [ ] Accessibility of notices (Art 50(5) accessibility expectation)
- [ ] Register entry if Art 49 deployer registration applies
- [ ] Proactive disclosure for high-impact automated administrative action (local admin-law may add duties — flag for counsel)

## Output template

```markdown
# Public-sector AI readiness — Pilot to scale

## Initiative
- Body / unit:
- System:
- Pilot period → target scale date:
- Populations affected:

## Snapshot score
- Domains Met / Partial / Missing:
- Overall: Not ready / Conditionally ready / Ready with monitoring

## Critical blockers (must fix before scale)

## Checklist results
(table: domain | item | status | evidence | owner)

## Procurement clause pack (draft topics)
(bullet list of clause themes — not final legal text)

## Regulatory milestones to plan against
(cite verified AI Act dates relevant to this system)

## 30 / 60 / 90-day plan

## Disclaimer
Preliminary readiness aid by Aigov.consulting skills — not legal advice,
not a FRIA, not a procurement award decision.
```

## Quality bar

- Concrete gaps with owners, not generic "ensure compliance".
- Cite Art 26 / 27 / 49 / 50 / 4 with URLs when asserting duties.
- Respect national administrative and procurement law: mark where local counsel must confirm.
