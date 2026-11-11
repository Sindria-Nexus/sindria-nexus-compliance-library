Last verified: November 11, 2026

# AWS Bedrock — Evidence Mapping

## What the platform is

Amazon Bedrock is AWS's fully managed service for building and scaling generative AI applications with foundation models. The evidence here comes from three artifacts: the **CloudTrail record**, **model invocation logging**, and **Guardrails for Amazon Bedrock**. These are three separately switched-on settings with different defaults — none of them is a single "Bedrock logging" toggle.

## Evidence mapping

Status key: **In hand** — the artifact satisfies the control as evidence. **Wrapper** — the artifact counts once your process around it is documented.

| Platform artifact | ISO 42001 Annex A | SOC 2 CC | Status | Wrapper note |
|---|---|---|---|---|
| **CloudTrail management events.** Every Bedrock API call recorded: who made it, with which IAM identity, from which IP, and when — InvokeModel, Converse, and streaming variants included. | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | Wrapper | On by default, but Event History keeps management events for 90 days only. Longer retention needs a trail or event data store delivering to S3. CloudTrail records *that* a call happened — never the prompt or response bodies. |
| **Model invocation logging to S3 / CloudWatch Logs.** The full prompt sent, response returned, model ID, token counts, and caller ARN, for every invocation on the `bedrock-runtime` endpoint. | A.6.2.8 Recording of event logs; A.7.5 Provenance of data | CC7.2 System operations; CC4.1 Monitoring activities | Wrapper | **Off by default — enable per Region**, document retention and review. Covers `bedrock-runtime` calls only — calls on other endpoints (e.g. `bedrock-mantle`) are not captured. Bodies over 100 KB need an S3 large-data location; the CloudWatch GenAI Observability per-request table is only populated if logs go to CloudWatch Logs. |
| **CloudTrail data events for agents and knowledge bases.** InvokeAgent, Retrieve, RetrieveAndGenerate, and ApplyGuardrail calls. | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | Wrapper | **Not logged by default** — needs advanced event selectors, and data events are charged separately. |
| **Guardrails — content filters, denied topics, and word filters.** Harmful categories, off-limits topics, and blocked terms screened on both the input prompt and the model response. | A.9.2 Processes for responsible use; A.6.2.4 Verification and validation | CC5.3 Control activities; CC7.2 System operations | Wrapper | Only where the guardrail ID and version are passed on the call. A guardrail that exists but is never attached to a call protects nothing. |
| **Guardrails — sensitive information filters.** PII in prompts and responses blocked or anonymised, with entity and action recorded in the guardrail trace. | A.7.2 Data for development; A.9.2 Processes for responsible use | CC6.1 Logical access; CC7.2 System operations | Wrapper | Only where the guardrail ID and version are passed on the call — same condition as the content filters. See flags: the trace itself contains the original PII value, and the filter is text-only. |
| **Guardrails — contextual grounding checks and CloudWatch metrics.** Responses checked for grounding and relevance against your source; `InvocationsIntervened` published to CloudWatch (`AWS/Bedrock/Guardrails`). | A.6.2.4 Verification and validation; A.6.2.6 Operation and monitoring | CC4.1 Monitoring activities; CC4.2 Evaluation of deficiencies | Wrapper | Needs thresholds, alarms, and a response process. Contextual grounding requires a `grounding_source` on every request — without one the check cannot run, so do not enable it for general workloads such as code generation where there is no source material in context. |

## What Bedrock does not give you — the gap band (the engagement)

No platform artifact covers these. They are the management system around the evidence — and they are the engagement.

- **Policy & scope** — A.2.2 AI policy, A.2.3 alignment with your other policies, and the Statement of Applicability deciding which of the 38 controls apply. SOC 2: CC1 governance.
- **Impact & risk** — A.5.2–A.5.5 impact assessments for individuals, groups, and society, plus the AI risk register behind them. SOC 2: CC3 risk assessment.
- **Accountability & response** — A.3.2 named roles, A.3.3 reporting of concerns, A.8.4 incident communication, A.9.4 intended use. SOC 2: CC1 / CC2 / CC7.4.

The point: AWS gives you the evidence. ISO 42001 makes it certifiable — the policy, risk, and accountability wrapper an auditor can test.

## Honest flags

- **Three logging settings, three defaults.** CloudTrail management events are on (90 days in Event History); CloudTrail data events are off; model invocation logging is off. Unless invocation logging was already on when something happened, there is no record of what was asked or answered, and it cannot be recovered later. Invocation logging also covers only `bedrock-runtime` calls — traffic on `bedrock-mantle` (e.g. the native Anthropic Messages API path) is not captured, so confirm which endpoint your traffic uses.
- **Guardrails do not apply themselves.** A guardrail only runs when its ID and version are passed on the call (or via `ApplyGuardrail`). Audit the call sites, not the guardrail's existence.
- **The guardrail trace leaks the PII it caught — by design.** The `match` field in the guardrail trace contains the original PII value, not the masked output, so your application can use the detection result. Treat trace output with the same care as the prompt data itself, and restrict who can read it. Model invocation logs are the same: the `input` field in CloudWatch Logs always contains the original, unmodified request regardless of guardrail intervention.
- **Sensitive-information filters are text-only.** They do not evaluate tool arguments or tool results in function-calling workloads — PII in those fields is neither blocked nor masked. Confirm input and output actions are set for each direction in your guardrail configuration; do not assume a single top-level setting covers both.
- **Contextual grounding needs a source.** Enabling the contextual grounding policy means every request must carry an explicit `grounding_source` (plus the query and the content to guard), so do not enable it for general workloads such as code generation where there is no source material in context.
- **There is no `InvocationsBlocked` metric.** The CloudWatch metric is `InvocationsIntervened` (namespace `AWS/Bedrock/Guardrails`). Alarm on the intervention rate (`InvocationsIntervened` / `Invocations`), not a metric that does not exist.

## Sources

- AWS Documentation — CloudTrail logging for Amazon Bedrock: https://docs.aws.amazon.com/bedrock/latest/userguide/logging-using-cloudtrail.html
- AWS Documentation — Model invocation logging (off by default, per Region, S3 / CloudWatch Logs; `bedrock-runtime` only): https://docs.aws.amazon.com/bedrock/latest/userguide/model-invocation-logging.html
- AWS Documentation — Guardrails for Amazon Bedrock: https://docs.aws.amazon.com/bedrock/latest/userguide/guardrails.html
- AWS Documentation — Remove PII from conversations by using sensitive information filters: https://docs.aws.amazon.com/bedrock/latest/userguide/guardrails-sensitive-filters.html
- AWS Documentation — Use contextual grounding check to filter hallucinations in responses: https://docs.aws.amazon.com/bedrock/latest/userguide/guardrails-contextual-grounding-check.html
- AWS Documentation — Monitor Amazon Bedrock Guardrails using CloudWatch metrics: https://docs.aws.amazon.com/bedrock/latest/userguide/monitoring-guardrails-cw-metrics.html
- AWS Documentation — CloudWatch Generative AI observability, Model Invocations (per-request table needs CloudWatch Logs destination): https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/model-invocations.html
- ISO/IEC 42001:2023, Annex A (38 controls, A.2–A.10): https://www.iso.org/standard/81230.html
- AICPA — 2017 Trust Services Criteria (with revised Points of Focus, 2022): https://www.aicpa-cima.com/resources/download/2017-trust-services-criteria-with-revised-points-of-focus-2022

## Disclaimer

This is a mapping aid, not legal advice or a compliance guarantee. ISO 42001 or SOC 2 evidence does not equal legal compliance. Applicability of each control is set in your Statement of Applicability and tested by your auditor. A vendor's own certification covers the vendor, not your deployment.
