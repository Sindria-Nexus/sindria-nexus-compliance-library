Last verified: November 11, 2026

# Snowflake Cortex — Evidence Mapping

## What the platform is

Snowflake Cortex is the AI layer inside Snowflake: LLM functions callable in SQL, Cortex Agents, Cortex Analyst (natural-language-to-SQL over a governed semantic layer), and Cortex Search — all running on data that never leaves Snowflake's governed environment, under Horizon Catalog controls. A deployment already generates Account Usage audit views, AI Observability traces, and Cortex Analyst evaluation records.

## Mapping table

Status: **In hand** — the artifact satisfies the control as evidence. **Wrapper** — the artifact counts once the process around it is documented.

| Platform artifact | ISO 42001 Annex A | SOC 2 CC | Status | Wrapper note |
|---|---|---|---|---|
| Account Usage Cortex views — `CORTEX_FUNCTIONS_USAGE_HISTORY` and `CORTEX_ANALYST_USAGE_HISTORY` record every Cortex call and Analyst-generated SQL query, with user, role, model, and tables accessed, plus `ACCESS_HISTORY`. | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | In hand | Account Usage views retain **1 year (365 days)** of history. The AI-functions view is also published as `CORTEX_AI_FUNCTIONS_USAGE_HISTORY` (GA March 2026); per-query token detail lives in `CORTEX_FUNCTIONS_QUERY_USAGE_HISTORY`. |
| AI Observability events & traces — agent and Analyst steps in `SNOWFLAKE.LOCAL.AI_OBSERVABILITY_EVENTS`, with inputs, outputs, and request IDs, reviewable in Snowsight; guardrail scans in Account Usage. | A.6.2.8 Recording of event logs; A.6.2.7 Technical documentation | CC7.2 System operations; CC4.1 Monitoring activities | Wrapper | Needs a review cadence and retention rule. Read via the `GET_AI_OBSERVABILITY_EVENTS` table functions (recommended); direct table access is for limited admin use. Rows are immutable — only the `SNOWFLAKE.AI_OBSERVABILITY_ADMIN` application role can delete them for retention management. |
| Horizon Catalog controls, enforced before the model — RBAC resolved first, then masking and row-access policies apply before data reaches a model; classification and lineage in the same catalog. | A.9.2 Processes for responsible use; A.7.5 Data provenance | CC6.1 Logical access; CC7.2 System operations | In hand | Cortex is enabled for every user in a new account by default (`SNOWFLAKE.CORTEX_USER` is granted to PUBLIC) — restrict it deliberately; the narrower `AI_FUNCTIONS_USER` role (GA April 2026) grants scalar AI functions only. |
| Semantic view / model — the governed definition — tables, dimensions, metrics, synonyms, and joins defined once in a versioned semantic layer; Analyst answers only through those definitions. | A.6.2.7 Technical documentation; A.6.2.5 Deployment | CC8.1 Change management; CC2.3 Communication of changes | Wrapper | Needs a named owner and change approval. |
| Verified queries — vetted question-and-SQL pairs in the semantic model; Analyst reuses the trusted SQL and learns your definitions — what "active" means — from them. | A.6.2.4 Verification and validation; A.7.4 Quality of data | CC4.1 Monitoring activities; CC8.1 Change management | In hand | When a question matches a verified query, Analyst can reuse the vetted SQL directly instead of generating new SQL. |
| Cortex Analyst evaluations — batch evaluations run verified queries as ground truth, execute Analyst's SQL, compare results, and track accuracy and latency regressions over time. | A.6.2.4 Verification and validation; A.9.2 Processes for responsible use | CC4.1 Monitoring activities; CC4.2 Evaluation of deficiencies | Wrapper | Needs pass thresholds and a regression response. During an evaluation run, selected verified queries are removed from a temporary copy of the semantic view so the test is honest; unselected ones still guide Analyst. |

## The gap is the engagement

No platform artifact covers these. They are the management system around the evidence — and they are the engagement.

- **Policy & scope** — A.2.2 AI policy, A.2.3 alignment with your other policies, and the Statement of Applicability deciding which of the 38 controls apply. SOC 2: CC1 governance.
- **Impact & risk** — A.5.2–A.5.5 impact assessments for individuals, groups, and society, plus the AI risk register behind them. SOC 2: CC3 risk assessment.
- **Accountability & response** — A.3.2 named roles, A.3.3 reporting of concerns, A.8.4 incident communication, A.9.4 intended use. SOC 2: CC1 / CC2 / CC7.4.

The point: Snowflake gives you the evidence. ISO 42001 makes it certifiable — the wrapper an auditor can test.

## Honest flags and footnotes

- **Direct Analyst logs live in a different table.** Direct Cortex Analyst request/response telemetry sits in `SNOWFLAKE.LOCAL.CORTEX_ANALYST_REQUESTS_RAW`, separate from `AI_OBSERVABILITY_EVENTS` — collect both for a complete trail. (Analyst invoked as a tool by a Cortex Agent does appear in `AI_OBSERVABILITY_EVENTS` as part of the agent trace.)
- **The observability table is best-effort, not complete.** Snowflake states telemetry is delivered on a best-effort basis — a span can occasionally be dropped or arrive late. Do not present it as a lossless audit log.
- **Not everything writes to the observability table.** Built-in AI SQL functions (`AI_COMPLETE`, `AI_CLASSIFY`, etc.) and the Cortex REST API do **not** write traces to `AI_OBSERVABILITY_EVENTS` — monitor those through the Account Usage views. Cortex Search writes only when `REQUEST_LOGGING` is enabled on the service.
- **Cortex is on by default for everyone.** A new account grants Cortex access to all users via the PUBLIC role. If your audit story is "only approved roles can call the models," that restriction is a configuration step you must take and evidence.
- **Analyst is increasingly surfaced through Agents.** Snowflake now recommends moving Analyst use into Cortex Agents / CoWork; the semantic view and verified queries remain the governed layer either way.

## Sources

- Snowflake Documentation — AI Observability with Snowflake Cortex: https://docs.Snowflake.com/en/user-guide/snowflake-cortex/ai-observability
- Snowflake Documentation — AI_OBSERVABILITY_EVENTS table: https://docs.snowflake.com/en/sql-reference/local/ai_observability_events
- Snowflake Documentation — Account Usage: https://docs.snowflake.com/en/sql-reference/account-usage
- Snowflake Documentation — Cortex Analyst evaluations: https://docs.snowflake.com/en/user-guide/snowflake-cortex/cortex-analyst-evaluations
- ISO/IEC 42001:2023 Annex A (38 controls, A.2–A.10)
- AICPA SOC 2 CC criteria

## Disclaimer

This is readiness guidance, not a certification guarantee. Applicability is set in your Statement of Applicability and tested by your auditor. Snowflake's own certifications cover Snowflake's service — not your account, your roles and masking policies, your semantic views, or your use of Cortex.
