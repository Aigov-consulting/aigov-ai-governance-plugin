---
name: ai-act-classifier
description: >-
  Use for fast EU AI Act risk classification: prohibited Art 5, high-risk
  Annex I/III, GPAI, limited-risk Art 50, or minimal — with decision tree,
  provider/deployer/importer/distributor role, and verified application dates
  including Digital Omnibus (Reg. 2026/1744) delays.
---

# EU AI Act classifier

Author: Aigov.consulting (https://aigov.consulting). Maintainer: GitHub herboloid.

Produce a **fast, cited preliminary classification** of an AI system or agent use case under Regulation (EU) 2024/1689 (AI Act), as amended. **Not legal advice.**

## Primary sources (mandatory citations)

- Consolidated AI Act overview: https://eur-lex.europa.eu/eli/reg/2024/1689/oj
- Commission AI Act Service Desk (article pages; reflects Digital Omnibus): https://ai-act-service-desk.ec.europa.eu/en/ai-act
- Art 113 entry into force / application: https://ai-act-service-desk.ec.europa.eu/en/ai-act/article-113
- Implementation timeline: https://ai-act-service-desk.ec.europa.eu/en/ai-act/timeline/timeline-implementation-eu-ai-act
- Digital Omnibus on AI — Regulation (EU) 2026/1744: https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32026R1744
- Art 5 prohibited practices: https://ai-act-service-desk.ec.europa.eu/en/ai-act/article-5
- Art 6 high-risk classification: https://ai-act-service-desk.ec.europa.eu/en/ai-act/article-6
- Annex III (via Service Desk / EUR-Lex annexes)
- Art 50 transparency: https://ai-act-service-desk.ec.europa.eu/en/ai-act/article-50
- Art 3 definitions (provider, deployer, importer, distributor, GPAI): https://ai-act-service-desk.ec.europa.eu/en/ai-act/article-3

## Verified dates (do not invent)

Verified against Commission AI Act Service Desk Art 113 text (consolidated as at 27 July 2026) and the official timeline page. Amending instrument: **Regulation (EU) 2026/1744** (Digital Omnibus on AI).

| Obligation cluster | Applies from | Cite |
|---|---|---|
| Ch. I–II (incl. Art 4 AI literacy; Art 5 prohibitions) | **2 Feb 2025**, except new Art 5(1) points (ba)/(bb) and Art 5(1a)(1b) from **2 Dec 2026** | Art 113(a) amended |
| Ch. III §4, Ch. V (GPAI), Ch. VII, Ch. XII, Art 78 | **2 Aug 2025** (except Art 101) | Art 113(b) |
| General application; Art 50 transparency; innovation measures | **2 Aug 2026** | Art 113 + timeline |
| Art 50(2) transition for certain pre-2 Aug 2026 synthetic-content systems; additional prohibitions | **2 Dec 2026** | Timeline / Art 113(a) exceptions |
| High-risk rules Ch. III §§1–3 for **Annex III / Art 6(2)** systems | **2 Dec 2027** | Art 113(c)(i) via Reg. 2026/1744 |
| High-risk rules Ch. III §§1–3 for **Annex I / Art 6(1)** product-embedded systems | **2 Aug 2028** | Art 113(c)(ii) via Reg. 2026/1744 |
| ≥1 AI regulatory sandbox per Member State | **2 Aug 2027** | Timeline (Art 57 context) |

If your session date is after these pages change, re-fetch Art 113 / timeline before stating dates. If unverifiable offline, write `DATE UNVERIFIED — check EUR-Lex / Service Desk` rather than guessing.

## Decision tree (follow in order)

```
1. Is it an "AI system" or "GPAI model" under Art 3?
   └─ No → Out of scope (explain). Stop.
2. Prohibited practice under Art 5?
   └─ Yes → PROHIBITED. Do not deploy. Cite the Art 5 point. Stop.
3. High-risk under Art 6(1) (safety component / product under Annex I Union harmonisation legislation)?
   └─ Yes → HIGH-RISK (Annex I pathway). Note Art 6(1) application date 2 Aug 2028 for Ch III §§1–3.
4. Listed in Annex III and not exempt under Art 6(3) conditions?
   └─ Yes → HIGH-RISK (Annex III pathway). Note application date 2 Dec 2027 for Ch III §§1–3.
5. GPAI model provider obligations (Ch. V) relevant?
   └─ Yes → Flag GPAI / systemic risk (Arts 51–55) separately from system risk class.
6. Transparency triggers under Art 50 (interaction with humans; synthetic content; emotion recognition; biometric categorisation; deepfakes; certain AI text)?
   └─ Yes → LIMITED RISK (transparency). Applies from 2 Aug 2026 (with stated transitions).
7. Else → MINIMAL RISK (voluntary codes Art 95 may still help).
```

Always record **residual uncertainty** (e.g. unclear Annex III employment use, unclear product embedding).

## Role determination (Art 3)

Ask which activities the organisation performs:

| Role | Typical signal |
|---|---|
| **Provider** | Develops / places on market / puts into service under its name; substantially modifies |
| **Deployer** | Uses under its authority (except personal non-professional use) |
| **Importer** | Places on EU market a system from a third-country provider |
| **Distributor** | Makes available on market without affecting compliance |
| **Authorised representative** | Mandated for certain non-EU providers |

Many organisations are **deployers** of third-party agents (e.g. workplace bots) and sometimes **providers** if they brand/substantially modify. State both if dual.

## High-risk obligation pointers (do not paste the whole Act)

If HIGH-RISK, list role-specific next actions with citations:

**Provider-oriented (Arts 8–17, 49, etc.):** risk management (Art 9), data governance (Art 10), technical documentation (Art 11), record-keeping (Art 12), transparency to deployers (Art 13), human oversight design (Art 14), accuracy/robustness/cybersecurity (Art 15), QMS (Art 17), registration (Art 49).

**Deployer-oriented ([Art 26](https://ai-act-service-desk.ec.europa.eu/en/ai-act/article-26)):** use per instructions; competent oversight; monitoring; input data suitability; logs ≥ 6 months where required; worker information for workplace use; inform natural persons subject to Annex III decision support (Art 26(11)); cooperate with authorities.

**FRIA:** when Art 27 applies (public bodies / certain public-service private entities / specified Annex III points) — https://ai-act-service-desk.ec.europa.eu/en/ai-act/article-27

**AI literacy:** Art 4 duties already applicable since 2 Feb 2025.

For agentic workplace tools, recommend following with `agent-audit` and `action-gate-policy`.

## Output template

```markdown
# EU AI Act — Preliminary Classification

## System summary
- Name / purpose:
- Affected persons:
- Geographic deployment:

## Classification
- Result: PROHIBITED | HIGH-RISK (Annex I) | HIGH-RISK (Annex III — area …) | GPAI (model) | LIMITED (Art 50) | MINIMAL | OUT OF SCOPE
- Decision-tree path (steps taken):
- Confidence: High / Medium / Low — unknowns:

## Roles
- Organisation appears to be: provider / deployer / importer / distributor / mixed
- Evidence:

## Applicable dates (cited)
- …

## Top obligations to investigate next
1. … (article + URL)
2. …

## Recommended follow-on skills
- agent-audit / action-gate-policy / dpia-draft / public-sector-ai-readiness / contract-review

## Disclaimer
Preliminary working classification only — not legal advice or a conformity assessment.
Verify against EUR-Lex and competent authorities before reliance.
```

## Quality rules

- Cite article + URL for every legal claim.
- Prefer Service Desk + EUR-Lex over secondary blogs.
- Never invent Annex III category numbers; if unsure, quote the user's use-case and mark "possible Annex III — confirm".
- Separate **system** classification from **GPAI model** provider duties.
