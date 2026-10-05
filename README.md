# Aigov AI Governance (Grok Build plugin)

Governance tooling for organisations building or deploying AI systems. Ships four skills that help classify EU AI Act risk, draft GDPR DPIAs, scout public funding and regulatory sandboxes, and review contracts for governance risks.

**Author:** [Aigov.consulting](https://aigov.consulting)  
**Maintainer:** [@herboloid](https://github.com/herboloid)  
**License:** MIT

## Skills

| Skill | When to use it |
|---|---|
| `ai-act-assessment` | Classify an AI system under the EU AI Act (prohibited practices, high-risk, transparency, GPAI, minimal risk) and list role-specific obligations. |
| `dpia-draft` | Draft a GDPR data protection impact assessment for a project or AI system. |
| `funding-sandboxes` | Find and evaluate grants, regulator sandboxes, consortia, and other opportunity windows with deadlines. |
| `contract-review` | Review a contract, MoU, NDA, or offer for risk clauses and proposed redlines (governance / procurement angle). |

## What this plugin does **not** do

- No MCP servers, hooks, or network calls — skills only.
- No credentials required.
- Outputs are preliminary working drafts, not legal advice. Final decisions stay with counsel / DPO / compliance owners.

## Install

In Grok Build, open `/plugin`, search for **aigov-ai-governance**, and install. Or install from this repository once listed in the [xAI plugin marketplace](https://github.com/xai-org/plugin-marketplace).

## Security

This plugin contains only markdown skill instructions. It does not execute shell, fetch remote code, or read secrets. Declare nothing to network endpoints.

## Attribution

Built and maintained by Aigov.consulting for public use under MIT.
