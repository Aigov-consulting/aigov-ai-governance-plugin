---
name: contract-review
description: >-
  Use when reviewing a contract, MoU, NDA, MSA, or AI/vendor offer for
  governance risks — especially AI provider vs deployer roles, data use for
  training, agent/MCP permissions, audit rights, and public procurement.
---

# Contract risk review (AI / agent governance lens)

Author: Aigov.consulting (https://aigov.consulting). Maintainer: GitHub herboloid.

Produce a structured risk review of a contract or offer. **Does not replace local counsel.** Focus on AI governance, data, agent tooling, and (where relevant) public procurement.

## Workflow

1. Confirm which party the user represents, governing law, and document completeness (schedules, DPAs, SLA, security annex).
2. Summarise parties, subject matter, term, fees, and key obligations.
3. Flag risks with clause citations, why it matters, and proposed redlines.
4. Separate **must-fix before signature** from **negotiate if feasible**.
5. Escalate novel / high-stakes clauses to counsel explicitly.

## AI- and agent-specific review points

| Topic | What to look for | Why |
|---|---|---|
| Role allocation | Provider / deployer / processor language matching AI Act Art 3 reality | Mis-labelling shifts compliance burden unfairly |
| Training use | Vendor may use customer content / prompts / tickets to train models | Data protection + confidentiality + competitive leakage |
| Subprocessors | Model hosts, log stores, support access | GDPR Art 28 chain; sovereignty |
| Agent permissions | Broadscope OAuth; "access all mailboxes"; silent scope expansion | Excessive agency; security |
| Audit & logs | Right to audit controls; access to action logs | Art 26-style deployer accountability; investigations |
| Incident notice | Timelines for breach / serious AI incident | Align with GDPR and AI Act reporting expectations |
| Liability / indemnity | Caps that exclude AI regulatory fines or data incidents | Residual balance-sheet risk |
| IP of prompts / outputs | Ownership of policies, eval sets, fine-tunes | Lock-in / continuity |
| Exit | Data return, deletion cert, transition | Public-service continuity |
| Public sector | Audit by SAI, transparency law, assignment limits | Local admin / procurement rules |

Also apply classic review: unilateral termination, auto-renewal, unlimited liability carve-outs, jurisdiction, confidentiality over-breadth, penalty clauses.

## Output template

```markdown
# Contract risk review — DRAFT

## Document & parties
## Executive risk rating (Critical / High / Medium / Low)
## Summary of deal
## Findings
### F-NN [Title]
- Clause:
- Issue:
- Impact:
- Proposed redline:
- Priority: Must-fix / Negotiate / Accept-with-monitoring

## AI Act / GDPR alignment notes
(cite articles + URLs only when stating legal duties)

## Open questions for counsel
## Disclaimer
Not legal advice. No signature recommendation without qualified counsel
(and procurement officer for public bodies).
```

## Quality rules

- Quote or pinpoint clauses; do not invent clause numbers.
- Prefer precise redlines over vague "strengthen liability".
- When AI Act duties are mentioned, cite Service Desk / EUR-Lex URLs.
- Never send negotiated text to the counterparty unless the user explicitly orders that send.
