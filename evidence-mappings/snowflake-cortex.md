Last verified: November 11, 2026

# Snowflake Cortex — Evidence Mapping

## What the platform is

Snowflake Cortex is the AI layer inside Snowflake: LLM functions callable in SQL, Cortex Agents, Cortex Analyst (natural-language-to-SQL over a governed semantic layer), and Cortex Search — all running on data that never leaves Snowflake's governed environment, under Horizon Catalog controls. A deployment already generates Account Usage audit views, AI Observability traces, and Cortex Analyst evaluation records.

## Mapping table

Status: **In hand** — the artifact satisfies the control as evidence. **Wrapper** — the artifact counts once the process around it is documented.

| Platform artifact | ISO 42001 Annex A | SOC 2 CC | Status | Wrapper note |
|---|---|---|---|---|
| Account Usage Cortex views — `CORTEX_AI_FUNCTIONS_USAGE_HISTORY` (the canonical AI-functions view) records Cortex AI function calls with user, role, model, tokens and credits; `CORTEX_AGENT_USAGE_HISTORY` covers agent requests; plus `ACCESS_HISTORY` for tables accessed. | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | In hand | Account Usage views retain **1 year (365 days)** of history. Rows are per function call but aggregated into **one-hour windows** — a long-running query can appear as several rows. Usage data in `CORTEX_AI_FUNCTIONS_USAGE_HISTORY` starts January 5, 2026; user, role, and query-tag fields are present for data from February 16, 2026. **Do not use the legacy `CORTEX_FUNCTIONS_USAGE_HISTORY` / `CORTEX_FUNCTIONS_QUERY_USAGE_HISTORY` views — they are no longer updated (data ends November 21, 2025; slated for deprecation November 22, 2026); `CORTEX_AISQL_USAGE_HISTORY` is slated for deprecation January 15, 2027. `CORTEX_ANALYST_USAGE_HISTORY` is hourly-aggregated only (request counts, credits, username) — it does **not** record per-query generated SQL, model, or role; Analyst-generated SQL lives in `SNOWFLAKE.LOCAL.CORTEX_ANALYST_REQUESTS_RAW` (see below). |
| AI Observability events & traces — agent and Analyst steps in `SNOWFLAKE.LOCAL.AI_OBSERVABILITY_EVENTS`, with inputs, outputs, and request IDs, reviewable in Snowsight; guardrail scans in Account Usage. | A.6.2.8 Recording of event logs; A.6.2.7 Technical documentation | CC7.2 System operations; CC4.1 Monitoring activities | Wrapper | Needs a review cadence and retention rule. Read via the `GET_AI_OBSERVABILITY_EVENTS` table functions (recommended); direct table access is for limited admin use and needs the `SNOWFLAKE.AI_OBSERVABILITY_READER` role. Rows can only be deleted by the `SNOWFLAKE.AI_OBSERVABILITY_ADMIN` application role, for retention management. Guardrail scans are recorded in `CORTEX_AI_GUARDRAILS_USAGE_HISTORY` (data from April 8, 2026). |
| Horizon Catalog controls, enforced before the model — RBAC resolved first, then masking and row-access policies apply before data reaches a model; classification and lineage in the same catalog. | A.9.2 Processes for responsible use; A.7.5 Data provenance | CC6.1 Logical access; CC7.2 System operations | In hand | Cortex is enabled for every user in a new account by default (`SNOWFLAKE.CORTEX_USER` is granted to PUBLIC, as is the `USE AI FUNCTIONS` account privilege) — restrict it deliberately. The narrower `AI_FUNCTIONS_USER` role grants scalar AI functions only (it excludes aggregate functions `AI_AGG` and `AI_SUMMARIZE_AGG`, and grants no access to Cortex Agent, Analyst, Fine-tuning, or Search) and is **not** granted to PUBLIC by default. |
| Semantic view / model — the governed definition — tables, dimensions, metrics, synonyms, and joins defined once in a versioned semantic layer; Analyst answers only through those definitions. | A.6.2.7 Technical documentation; A.6.2.5 Deployment | CC8.1 Change management; CC2.3 Communication of changes | Wrapper | Needs a named owner and change approval. |
| Verified queries — vetted question-and-SQL pairs in the semantic model; Analyst uses them to guide SQL generation — what "active" means — from them. | A.6.2.4 Verification and validation; A.7.4 Quality of data | CC4.1 Monitoring activities; CC8.1 Change management | In hand | When a question matches a verified query, Analyst is guided by the vetted SQL instead of generating unaided. A verified query can guide Analyst at runtime or serve as evaluation ground truth, but not both at the same time. |
| Cortex Analyst evaluations — batch evaluations run verified queries as ground truth, execute Analyst's SQL, compare results, and track accuracy and latency regressions over time. | A.6.2.4 Verification and validation; A.9.2 Processes for responsible use | CC4.1 Monitoring activities; CC4.2 Evaluation of deficiencies | Wrapper | Needs pass thresholds and a regression response. During an evaluation run, selected verified queries are removed from a temporary copy of the semantic view so the test is honest; unselected ones still guide Analyst. Evaluation runs execute as Snowflake tasks and need the associated task privileges under a single primary role. |

## The gap is the engagement

No platform artifact covers these. They are the management system around the evidence — and they are the engagement.

- **Policy & scope** — A.2.2 AI policy, A.2.3 alignment with your other policies, and the Statement of Applicability deciding which of the 38 controls apply. SOC 2: CC1 governance.
- **Impact & risk** — A.5.2–A.5.5 impact assessments for individuals, groups, and society, plus the AI risk register behind them. SOC 2: CC3 risk assessment.
- **Accountability & response** — A.3.2 named roles, A.3.3 reporting of concerns, A.8.4 incident communication, A.9.4 intended use. SOC 2: CC1 / CC2 / CC7.4.

The point: Snowflake gives you the evidence. ISO 42001 makes it certifiable — the wrapper an auditor can test.

## Honest flags and footnotes

- **Direct Analyst logs live in a different table.** Direct Cortex Analyst request/response telemetry sits in `SNOWFLAKE.LOCAL.CORTEX_ANALYST_REQUESTS_RAW`, separate from `AI_OBSERVABILITY_EVENTS` — collect both for a complete trail. (Analyst invoked as a tool by a Cortex Agent does appear in `AI_OBSERVABILITY_EVENTS` as part of the agent trace.)
- **The observability table is best-effort, not complete.** Snowflake states telemetry is delivered on a best-effort basis — a span can occasionally be dropped or arrive late. Do not present it as a lossless audit log. Base spend reporting on the usage views, not the event table.
- **Not everything writes to the observability table.** Built-in AI SQL functions (`AI_COMPLETE`, `AI_CLASSIFY`, etc.) and the Cortex REST API do **not** write traces to `AI_OBSERVABILITY_EVENTS` — monitor those through the Account Usage views (`CORTEX_AI_FUNCTIONS_USAGE_HISTORY` and `CORTEX_REST_API_USAGE_HISTORY`, data from November 1, 2025). Cortex Search writes only when `REQUEST_LOGGING` is enabled on the service.
- **Cortex is on by default for everyone.** A new account grants Cortex access to all users via the PUBLIC role. If your audit story is "only approved roles can call the models," that restriction is a configuration step you must take and evidence. Note the exception: **Cortex Analyst is opt-in** — it is not accessible by default and is enabled with the `ENABLE_CORTEX_ANALYST` account parameter.
- **Analyst is increasingly surfaced through Agents.** Snowflake now recommends moving Analyst use into Cortex Agents / CoWork; the semantic view and verified queries remain the governed layer either way.
- **Evaluation scores move between runs.** SQL generation is non-deterministic, so repeated runs of the same evaluation set can produce different SQL and different scores even with a pinned metric version (`v1`/`v2`/`v3`). Run the set several times to learn its normal range before gating a pipeline on a threshold.

## Sources

- **Snowflake Documentation — AI cost management and governance (usage-view lineage):** https://docs.snowflake.com/en/user-guide/snowflake-cortex/governance-and-availability/ai-cost-management-and-governance
- Snowflake Documentation — CORTEX_AI_FUNCTIONS_USAGE_HISTORY view: https://docs.snowflake.com/en/sql-reference/account-usage/cortex_ai_functions_usage_history
- Snowflake Documentation — AI Observability with Snowflake Cortex: https://docs.snowflake.com/en/user-guide/snowflake-cortex/ai-observability
- Snowflake Documentation — AI_OBSERVABILITY_EVENTS table: https://docs.snowflake.com/en/sql-reference/local/ai_observability_events
- Snowflake Documentation — Account Usage: https://docs.snowflake.com/en/sql-reference/account-usage
- Snowflake Documentation — Cortex Analyst evaluations: https://docs.snowflake.com/en/user-guide/snowflake-cortex/cortex-analyst-evaluations
- Snowflake Documentation — Opt out of Snowflake AI features (default access): https://docs.snowflake.com/en/user-guide/snowflake-cortex/opting-out
- Snowflake Documentation — Privileges and model access for Cortex AI Functions: https://docs.snowflake.com/en/user-guide/snowflake-cortex/aisql-privileges-and-access

## Disclaimer

This is a mapping aid, not legal advice or a compliance guarantee. ISO 42001 or SOC 2 evidence does not equal legal compliance. Applicability of each control is set in your Statement of Applicability and tested by your auditor. A vendor's own certification covers the vendor, not your deployment.
