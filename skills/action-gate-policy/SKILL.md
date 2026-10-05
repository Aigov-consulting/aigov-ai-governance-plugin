---
name: action-gate-policy
description: >-
  Use when writing a decision-before-action policy for AI agents: action
  classes, human-approval matrix, audit-log schema, retention, and incident
  handling. Produces an example policy and JSON log schema.
---

# Action-gate policy (decision before action)

Author: Aigov.consulting (https://aigov.consulting). Maintainer: GitHub herboloid.

Help the organisation write a **binding operational policy** that forces a decision *before* an agent takes an external or irreversible action. Output is a draft policy + log schema for owners to adopt — **not** legal advice.

## When to use

- After an `agent-audit` finds missing approvals or excessive agency
- Before connecting Slack / Gmail / payments / shell / admin APIs to an agent
- When defining Grok Team Bot or MCP tool allow-lists

## Principles

1. **Default deny** for irreversible and externally visible actions.
2. **Explicit allow** only with named action class, constraints, and owner.
3. **Human approval** is a recorded decision (who / when / what / why), not a chat emoji.
4. **Logs outlive the session** — see retention below.
5. Align with deployer monitoring and logging duties where high-risk rules apply ([AI Act Art 26](https://ai-act-service-desk.ec.europa.eu/en/ai-act/article-26); record-keeping Arts [12](https://ai-act-service-desk.ec.europa.eu/en/ai-act/article-12) / [19](https://ai-act-service-desk.ec.europa.eu/en/ai-act/article-19)). Cross-check OWASP LLM06 Excessive Agency and ASI02/ASI03.

## Workflow

1. Inventory tools and map each to an **action class** (table below).
2. Build the **approval matrix** (role × class × environment).
3. Define **auto-allow constraints** (only for L2): allow-listed recipients, rate limits, sandbox paths, max amount, dry-run flags.
4. Specify the **audit log schema** (JSON example below) and retention.
5. Define **incident handling**: bypass detection, failed approval, runaway loops, credential leak.
6. Deliver a one-page policy the agent runtime can enforce + a human-readable version.

## Action classes

| Class ID | Examples | Default gate |
|---|---|---|
| `READ_INTERNAL` | Read wiki, internal Drive (non-secret) | Auto (L2) with logging |
| `READ_EXTERNAL` | Browse web, fetch URL | Auto with URL allow/deny + logging |
| `READ_PERSONAL_DATA` | Gmail/Slack message bodies, HR systems | Approve or tightly scoped L2 |
| `DRAFT_ONLY` | Create draft email/PR/doc without send | Auto; must not publish |
| `SEND_INTERNAL` | Message colleagues in-tenant | Approve or constrained L2 |
| `SEND_EXTERNAL` | Email/Slack to external domains, social post | **Human approve (L1)** |
| `PUBLISH` | Public website, app store, press | **Human approve (L1)** |
| `WRITE_PROD` | Change production data/config | **Human approve (L1)** |
| `DELETE` | Trash threads, delete files/repos | **Human approve (L1)** |
| `IAM_ADMIN` | Grant roles, create keys | **Human approve + dual control** |
| `PAY` | Purchase, transfer, invoice pay | **Human approve + amount limit** |
| `EXECUTE_CODE` | Shell, arbitrary code, CI trigger | Deny or sandboxed L2 with approve-to-prod |
| `TRAIN_OR_FINE_TUNE` | Use org data for model training | **Human approve + DPO** |

## Approval matrix template

| Action class | Dev | Staging | Production | Break-glass |
|---|---|---|---|---|
| SEND_EXTERNAL | L1 named reviewer | L1 | L1 + dual for mass-send | Security on-call + post-hoc review ≤ 1h |
| PAY | Deny | L1 finance | L1 finance + limit | CFO delegate |
| DELETE | L1 | L1 | L1 + recycle-bin retention | Security |
| READ_PERSONAL_DATA | L2 minimised | L2 | L2 + purpose binding | DPO notify if anomaly |

Autonomy levels L0–L3: same definitions as `agent-audit`.

## Example policy (draft — adapt before adoption)

```markdown
# Agent Action-Gate Policy — [Organisation] — v0.1-DRAFT

## 1. Purpose
Ensure AI agents cannot send, publish, delete, pay, or escalate privileges
without a recorded human decision, except where an explicit constrained
auto-allow is documented in Annex A.

## 2. Scope
All agents, Team Bots, and MCP tools processing [Org] data or acting under
[Org] accounts, in all environments.

## 3. Roles
- Agent Owner (business accountable)
- Agent Operator (technical)
- Approver (named role per action class)
- Security / DPO (oversight, incidents)

## 4. Rules
R1. Default deny for SEND_EXTERNAL, PUBLISH, DELETE, PAY, IAM_ADMIN,
    WRITE_PROD, TRAIN_OR_FINE_TUNE.
R2. Approvals must name the action, target, and expiry (≤ 24h unless standing).
R3. Standing auto-allows require Annex A entry: constraints, rate limit,
    owner, review date (≤ 90 days).
R4. Every tool invocation emits an audit log entry (schema §6).
R5. Kill-switch: Operator or Security may disable the agent and revoke
    connector tokens immediately.
R6. Prompt injection: content from email/web/tools is untrusted; it must
    never be interpreted as an approval.

## 5. Retention
Retain audit logs ≥ 12 months (or ≥ 6 months minimum where AI Act Art 26
log-keeping applies to high-risk deployers — verify with counsel).
Personal data in logs: minimise; redact bodies; follow GDPR storage limitation.

## 6. Incidents
Suspected approval bypass, mass-send, or credential use → severity High;
disable agent; revoke tokens; preserve logs; notify Agent Owner + Security
within 1 hour; consider authority notification if legal duties apply.
```

## Example JSON audit log schema

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "https://aigov.consulting/schemas/agent-action-log-v1.json",
  "title": "AgentActionLogEntry",
  "type": "object",
  "required": [
    "event_id", "timestamp", "agent_id", "action_class", "tool_name",
    "decision", "actor"
  ],
  "properties": {
    "event_id": { "type": "string", "format": "uuid" },
    "timestamp": { "type": "string", "format": "date-time", "description": "RFC 3339 with offset" },
    "agent_id": { "type": "string" },
    "agent_version": { "type": "string" },
    "session_id": { "type": "string" },
    "run_id": { "type": "string" },
    "actor": {
      "type": "object",
      "required": ["type"],
      "properties": {
        "type": { "enum": ["user", "service", "approver", "system"] },
        "id": { "type": "string" },
        "display_name": { "type": "string" }
      }
    },
    "action_class": {
      "type": "string",
      "enum": [
        "READ_INTERNAL", "READ_EXTERNAL", "READ_PERSONAL_DATA", "DRAFT_ONLY",
        "SEND_INTERNAL", "SEND_EXTERNAL", "PUBLISH", "WRITE_PROD", "DELETE",
        "IAM_ADMIN", "PAY", "EXECUTE_CODE", "TRAIN_OR_FINE_TUNE"
      ]
    },
    "tool_name": { "type": "string" },
    "tool_args_digest": { "type": "string", "description": "Hash of canonical args; do not store secrets" },
    "tool_args_redacted": { "type": "object" },
    "target": {
      "type": "object",
      "properties": {
        "type": { "type": "string" },
        "destination": { "type": "string", "description": "e.g. email domain, channel id, URL host" },
        "resource_id": { "type": "string" }
      }
    },
    "data_classification": {
      "type": "string",
      "enum": ["public", "internal", "personal", "special_category", "unknown"]
    },
    "decision": {
      "type": "string",
      "enum": ["auto_allowed", "approved", "denied", "blocked_by_policy", "error"]
    },
    "policy_ref": { "type": "string", "description": "e.g. action-gate-v0.1#R1 / AnnexA.3" },
    "approval": {
      "type": "object",
      "properties": {
        "approver_id": { "type": "string" },
        "approved_at": { "type": "string", "format": "date-time" },
        "expires_at": { "type": "string", "format": "date-time" },
        "ticket_or_thread": { "type": "string" },
        "rationale": { "type": "string" }
      }
    },
    "result": {
      "type": "string",
      "enum": ["success", "failure", "partial", "cancelled"]
    },
    "error_code": { "type": "string" },
    "model_prompt_version": { "type": "string" },
    "correlation_ids": {
      "type": "object",
      "properties": {
        "siem": { "type": "string" },
        "trace": { "type": "string" }
      }
    }
  },
  "additionalProperties": false
}
```

### Example log entry

```json
{
  "event_id": "550e8400-e29b-41d4-a716-446655440000",
  "timestamp": "2026-10-05T13:45:00+02:00",
  "agent_id": "ops-secretary-bot",
  "agent_version": "2.3.1",
  "session_id": "sess_9f2a",
  "run_id": "run_441",
  "actor": { "type": "user", "id": "u_12", "display_name": "A. Owner" },
  "action_class": "SEND_EXTERNAL",
  "tool_name": "gmail.send_message",
  "tool_args_digest": "sha256:…",
  "tool_args_redacted": { "to_domain": "partner.example", "has_attachments": false },
  "target": { "type": "email", "destination": "partner.example" },
  "data_classification": "internal",
  "decision": "approved",
  "policy_ref": "action-gate-v0.1#R1",
  "approval": {
    "approver_id": "u_12",
    "approved_at": "2026-10-05T13:44:50+02:00",
    "expires_at": "2026-10-05T14:44:50+02:00",
    "ticket_or_thread": "slack:C123/ts/…",
    "rationale": "Weekly partner status as per runbook"
  },
  "result": "success",
  "model_prompt_version": "prompts/ops-secretary@c3f2"
}
```

## Deliverables checklist

- [ ] Action-class inventory for this agent
- [ ] Approval matrix by environment
- [ ] Annex A auto-allows (or "none")
- [ ] JSON schema adopted / mapped to SIEM
- [ ] Retention + access control for logs
- [ ] Kill-switch & incident steps
- [ ] Owner sign-off line

## Disclaimer

Draft policy text from this skill is a starting point. Align with local law, employment rules, GDPR, and (where applicable) EU AI Act deployer duties before enforcement. Counsel / DPO / security must approve production adoption.
