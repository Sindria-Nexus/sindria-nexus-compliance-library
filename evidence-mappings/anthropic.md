Last verified: November 11, 2026

# Anthropic (Claude API) — Evidence Mapping

## What the platform is

Claude via the Anthropic API is Anthropic's developer platform for building agents on Claude models. The evidence here comes from three places: the **Compliance API Activity Feed** and the **Admin API** (usage and cost reports, workspaces, API keys, roles), and your own **evaluation results** built using Anthropic's published method — define success criteria, then build evaluations to measure against them. Anthropic publishes a **system card** per model version with pre-deployment capability, safeguards, and agentic-safety evaluations.

There is no persistent Console eval/Workbench product to claim: Anthropic's evaluation guidance is a method (task-specific test sets, graded by code, humans, or an LLM judge against set criteria), and the evaluation evidence is yours — your datasets, rubrics, and retained results.

## Evidence mapping

Status key: **In hand** — the artifact satisfies the control as evidence. **Wrapper** — the artifact counts once your process around it is documented.

| Platform artifact | ISO 42001 Annex A | SOC 2 CC | Status | Wrapper note |
|---|---|---|---|---|
| **Compliance API Activity Feed.** Sign-ins, admin actions, config changes, API key and role changes — 6-year retention. | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | Wrapper | Enterprise only — enable first; **not retroactive**: recording starts the day the Compliance API is enabled, with no backfill. |
| **Usage & Cost Reports (Admin API).** Tokens and spend by key, workspace, model, and tier; Console exports CSV. | A.6.2.6 Operation and monitoring; A.4.5 System resources | CC4.1 Monitoring activities; CC7.2 System operations | In hand | Cost report is a daily roll-up lagging real-time usage by ~24 hours. Requires an admin-scoped API key and an organisation (not available for individual accounts). |
| **Workspaces, API keys, and member roles.** Keys scoped to a workspace, listed and revoked via the Admin API; invites and roles in one record. | A.4.5 System resources; A.6.2.8 Recording of event logs | CC6.1 Logical access; CC6.6 System boundaries | In hand | New API keys are created in the Console, not through the Admin API. |
| **Evaluation datasets and grading.** Task-specific test sets mirroring real use, graded by code, humans, or an LLM judge against set criteria. | A.6.2.4 Verification and validation; A.7.4 Quality of data; A.7.2 Data for development | CC4.1 Monitoring activities; CC7.2 System operations | Wrapper | Your datasets, rubrics, and retained results are the evidence. Anthropic supplies the method, not the evals. |
| **Per-response usage and prompt-cache records.** Every response returns the model, input/output tokens, and cache creation/read tokens. | A.7.5 Data provenance; A.6.2.8 Recording of event logs | CC7.2 System operations; CC4.1 Monitoring activities | Wrapper | Counts only if your app logs and retains them — Anthropic does not keep your prompts and responses for you. |
| **Claude system cards for your pinned model.** Anthropic-published pre-deployment capability, safeguards, and agentic-safety evals per model version. | A.10.3 Suppliers; A.6.2.7 Technical documentation | CC2.3 External communication; CC4.1 Monitoring activities | Wrapper | Needs your version pin and change log. A system card describes the model Anthropic tested, not your deployment of it. |

## What Anthropic does not give you — the gap band (the engagement)

No platform artifact covers these. They are the management system around the evidence — and they are the engagement.

- **Policy & scope** — A.2.2 AI policy, A.2.3 alignment with your other policies, and the Statement of Applicability deciding which of the 38 controls apply. SOC 2: CC1 governance.
- **Impact & risk** — A.5.2–A.5.5 impact assessments for individuals, groups, and society, plus the AI risk register behind them. SOC 2: CC3 risk assessment.
- **Accountability & response** — A.3.2 named roles, A.3.3 reporting of concerns, A.8.4 incident communication, A.9.4 intended use. SOC 2: CC1 / CC2 / CC7.4.

The point: Anthropic gives you the evidence. ISO 42001 makes it certifiable — the policy, risk, and accountability wrapper an auditor can test.

## Honest flags

- **The Activity Feed is metadata, not content.** It records who did what and when (actor, event type, timestamps, chat/project IDs). Prompt and response content is a separate matter: chat/file/project content follows your organisation's retention policy, and the Compliance API cannot return content your own policy has already deleted. Do not confuse the 6-year Activity Feed retention with 6 years of prompt history.
- **Do not cite the 180-day figure.** The 180-day number seen in many write-ups belongs to the Enterprise CSV audit export under Organisation settings — a capped lookback — not the Compliance API Activity Feed, which is retained for 6 years.
- **The Compliance API is Enterprise only** and must be explicitly enabled by the Primary Owner. Claude Team does not have it. If you are not on Enterprise, this row does not exist for you.
- **The Activity Feed is not retroactive.** Enable it late and there is nothing behind the enablement date. Switch it off and the gap is unrecoverable.
- **No prompt/response logging is built in.** The API returns token counts per response, but unless your own application logs and retains prompts, responses, and cache records, there is no record of what the model was asked or answered. Claude used through Bedrock, Vertex, or Foundry is outside the Compliance API's coverage.
- **System cards move with the model.** Each model version has its own card (e.g. Claude Opus 5, July 2026). Pin the model version, keep the card for that version, and log changes — an unpinned model silently changes the evidence underneath you.

## Sources

- Anthropic — Compliance API documentation (Activity Feed, 6-year retention), platform.claude.com
- Anthropic — Admin API documentation (Usage & Cost Reports, workspaces, API keys), platform.claude.com
- Anthropic — "Define success criteria and build evaluations" (Test & Evaluate), platform.claude.com
- Anthropic — Claude Opus 5 System Card: https://www.anthropic.com/claude-opus-5-system-card
- ISO/IEC 42001:2023 Annex A (38 controls, A.2–A.10)
- AICPA SOC 2 Trust Services Criteria (CC criteria)

## Disclaimer

This is readiness guidance, not a certification guarantee. Applicability of each control is set in your Statement of Applicability and tested by your auditor. A vendor's own certification covers the vendor, not your deployment.
