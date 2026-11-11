# Evidence Mappings — What Your AI Stack Already Proves

Each page maps one platform's own audit trail and evaluation artifacts to
ISO/IEC 42001:2023 Annex A controls and SOC 2 Trust Services Criteria. The
point is the opposite of a vendor's compliance page: this is what **your**
deployment already evidences, what still needs a wrapper (a named owner, a
retention rule, a documented threshold), and what the platform never gives
you — policy and scope, impact and risk, accountability and response. That
gap is the engagement.

**How to use these:** find a platform you already run on, read its page,
and check the two status columns. **In hand** means the artifact satisfies
the control as the platform produces it, with no extra process needed.
**Wrapper** means it only counts as evidence once your own process wraps
it — a documented review cadence, a retention rule, a named approver, a
pass threshold, or configuration such as enabling a log. Every page ends
with that gap, stated plainly.

**Staying current:** platforms change tiers, retention windows, and feature
names constantly. Every page carries a `Last verified` date as its first
line — the date its claims were last checked against the vendor's own
documentation. Treat anything older than a few months as a prompt to
re-check, not as a fact. Pin a version when you rely on a page.

| Platform | File | What it covers | Last verified |
|---|---|---|---|
| Anthropic (Claude API) | [anthropic.md](anthropic.md) | Six-year Activity Feed plus Admin API usage/cost reporting and your own evaluation results | November 11, 2026 |
| AWS Bedrock | [aws-bedrock.md](aws-bedrock.md) | CloudTrail API record, full prompt/response invocation logs, and Guardrails as the runtime control layer | November 11, 2026 |
| Azure OpenAI | [azure-openai.md](azure-openai.md) | Off-by-default diagnostic logs (metadata only), built-in and custom content-safety controls, and Foundry quality/safety evaluations | November 11, 2026 |
| Braintrust | [braintrust.md](braintrust.md) | Production traces with online scoring plus versioned datasets, experiments, scorers, and prompt versions | November 11, 2026 |
| Cloudflare AI Gateway | [cloudflare-ai-gateway.md](cloudflare-ai-gateway.md) | Per-request logs, analytics/metadata, BYOK + audit logs, caching, rate/spend limits, and Guardrails/DLP | November 11, 2026 |
| Cohere | [cohere.md](cohere.md) | North + Compass audit trails, RBAC/SSO/human gates, versioned datasets, fine-tuning metrics, and cited/grounded output | November 11, 2026 |
| Databricks (Mosaic AI) | [databricks.md](databricks.md) | LLM-judge evals plus human review, MLflow traces, and Unity Catalog audit logs with full payload logging | November 11, 2026 |
| Galileo | [galileo.md](galileo.md) | End-to-end traces, Luna-2 production scoring, Agent Control guardrail verdicts, and the dataset/experiment record | November 11, 2026 |
| Google Vertex AI | [google-vertex-ai.md](google-vertex-ai.md) | Cloud Audit Logs, sampled BigQuery request–response logging, Gen AI eval runs, and Agent Engine traces | November 11, 2026 |
| Helicone | [helicone.md](helicone.md) | Per-request logs, sessions/users, edge caching, eval scores, datasets-from-logs, and LLM Security | November 11, 2026 |
| Hugging Face | [hugging-face.md](hugging-face.md) | The Hub's org audit log, Git-versioned repos with pinned endpoints, and model/dataset cards plus Evaluate/Lighteval results | November 11, 2026 |
| Langfuse | [langfuse.md](langfuse.md) | Traces, scores, annotation queues, versioned datasets/experiments, and label-pinned prompts | November 11, 2026 |
| LangSmith | [langsmith.md](langsmith.md) | Full run tracing, online and offline evaluation, human feedback queues, and versioned prompts in Prompt Hub | November 11, 2026 |
| Mistral | [mistral.md](mistral.md) | Enterprise audit logs, workspaces/roles/SAML, guardrails + ZDR, OTel tracing, and offline/online evals | November 11, 2026 |
| NVIDIA | [nvidia.md](nvidia.md) | NeMo evals, guardrail decision records, and Curator/Customizer provenance plus NIM runtime logs/metrics and OpenShell/Sentry agent boundaries | November 11, 2026 |
| Pinecone | [pinecone.md](pinecone.md) | Control-plane audit logs to your own bucket plus RBAC/SSO/scoped keys | November 11, 2026 |
| Salesforce Agentforce | [salesforce-agentforce.md](salesforce-agentforce.md) | Trust Layer audit trail, toxicity scoring, and feedback log — with data masking unavailable for Agentforce agents | November 11, 2026 |
| Scale GenAI | [scale-genai.md](scale-genai.md) | Production audit trail plus a representative evaluation dataset and per-version in-workflow testing | November 11, 2026 |
| ServiceNow Now Assist | [servicenow-now-assist.md](servicenow-now-assist.md) | Execution plans, usage logs, AI Guardian guardrails, and the Control Tower inventory/lifecycle record | November 11, 2026 |
| Snowflake Cortex | [snowflake-cortex.md](snowflake-cortex.md) | Account Usage views, AI Observability traces, Horizon pre-model access controls, and Cortex Analyst's governed semantic layer with verified-query evaluations | November 11, 2026 |
| Surge | [surge.md](surge.md) | Delivered expert-built eval datasets, rubrics/verifiers, human evaluation results, RLHF/SFT training records, and red-teaming findings | November 11, 2026 |
| Vercel AI Gateway | [vercel-ai-gateway.md](vercel-ai-gateway.md) | Per-request metadata logs, OTel Trace Drains, budgets and routing/ZDR controls | November 11, 2026 |
| Weights & Biases Weave | [weights-biases-weave.md](weights-biases-weave.md) | Trace trees, versioned datasets/evals/scorers, and production scoring | November 11, 2026 |

## Status notes — read before you rely on a page

- **Helicone** is in maintenance mode (acquired by Mintlify, March 2026;
  hosted feature development stopped, new signups disabled). Its page is
  for existing users and self-hosted deployments, not a new-vendor
  recommendation.
- **Surge** is a managed expert-data service, not a self-serve platform.
  Its page maps delivered artifacts (datasets, rubrics, evaluation
  reports), not a live audit trail the buyer controls.
- **ServiceNow:** the full Generative AI log (`sys_generative_ai_log`) is
  ServiceNow Support staff only — even administrators cannot access it.
  The usable customer records are the usage log and Generative AI Metrics.
- **NVIDIA Sentry** is a reference design (announced September 2026,
  planned availability early 2027), not a shipped product.
- **OpenAI is deliberately not here.** Its legacy Evals platform is being
  shut down (read-only October 31, 2026, shutdown November 30, 2026) and
  the mapping would be a moving target.

## What these are not

Readiness guidance, not a certification guarantee. A vendor's own SOC 2
or ISO 42001 certification covers the vendor, not your deployment of it.
An auditor still needs your policies, your risk register, your impact
assessments, and your own processes — the platform's logs are evidence
inside that system, not a substitute for it.

## Disclaimer

This is a mapping aid, not legal advice or a compliance guarantee. ISO 42001 or SOC 2 evidence does not equal legal compliance. Applicability of each control is set in your Statement of Applicability and tested by your auditor. A vendor's own certification covers the vendor, not your deployment.
