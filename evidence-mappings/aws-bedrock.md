Last verified: November 11, 2026

# AWS Bedrock — Evidence Mapping

## What the platform is

Amazon Bedrock is AWS's fully managed service for building and scaling generative AI applications with foundation models. The evidence here comes from three artifacts: the **CloudTrail record**, **model invocation logging**, and **Guardrails for Amazon Bedrock**. These are three separately switched-on settings with different defaults — none of them is a single "Bedrock logging" toggle.

## Evidence mapping

Status key: **In hand** — the artifact satisfies the control as evidence. **Wrapper** — the artifact counts once your process around it is documented.

| Platform artifact | ISO 42001 Annex A | SOC 2 CC | Status | Wrapper note |
|---|---|---|---|---|
| **CloudTrail management events.** Every Bedrock API call recorded: who made it, with which IAM identity, from which IP, and when — InvokeModel, Converse, and streaming variants included. | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | In hand | On by default, but Event History keeps management events for 90 days only. Longer retention needs a trail or event data store delivering to S3. CloudTrail records *that* a call happened — never the prompt or response bodies. |
| **Model invocation logging to S3 / CloudWatch Logs.** The full prompt sent, response returned, model ID, token counts, and caller ARN, for every invocation. | A.6.2.8 Recording of event logs; A.7.5 Data provenance | CC7.2 System operations; CC4.1 Monitoring activities | Wrapper | **Off by default — enable per Region**, document retention and review. Bodies over 100 KB need an S3 large-data location; the CloudWatch GenAI Observability per-request table is only populated if logs go to CloudWatch Logs. |
| **CloudTrail data events for agents and knowledge bases.** InvokeAgent, Retrieve, RetrieveAndGenerate, and ApplyGuardrail calls. | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | Wrapper | **Not logged by default** — needs advanced event selectors, and data events are charged separately. |
| **Guardrails — content filters, denied topics, and word filters.** Harmful categories, off-limits topics, and blocked terms screened on both the input prompt and the model response. | A.9.2 Processes for responsible use; A.6.2.4 Verification and validation | CC5.3 Control activities; CC7.2 System operations | Wrapper | Only where the guardrail ID and version are passed on the call. A guardrail that exists but is never attached to a call protects nothing. |
| **Guardrails — sensitive information filters.** PII in prompts and responses blocked or anonymised, with entity and action recorded in the guardrail trace. | A.7.2 Data for development; A.9.2 Processes for responsible use | CC6.1 Logical access; CC7.2 System operations | Wrapper | Only where the guardrail ID and version are passed on the call (corrected from "In hand" in the source — same condition as the content filters). See flags: the trace itself contains the original PII value, and the filter is text-only. |
| **Guardrails — contextual grounding checks and CloudWatch metrics.** Responses checked for grounding and relevance against your source; `InvocationsIntervened` published to CloudWatch (`AWS/Bedrock/Guardrails`). | A.6.2.4 Verification and validation; A.6.2.6 Operation and monitoring | CC4.1 Monitoring activities; CC4.2 Evaluation of deficiencies | Wrapper | Needs thresholds, alarms, and a response process. Contextual grounding requires a `grounding_source` on every request — without one the call errors. |

## What Bedrock does not give you — the gap band (the engagement)

No platform artifact covers these. They are the management system around the evidence — and they are the engagement.

- **Policy & scope** — A.2.2 AI policy, A.2.3 alignment with your other policies, and the Statement of Applicability deciding which of the 38 controls apply. SOC 2: CC1 governance.
- **Impact & risk** — A.5.2–A.5.5 impact assessments for individuals, groups, and society, plus the AI risk register behind them. SOC 2: CC3 risk assessment.
- **Accountability & response** — A.3.2 named roles, A.3.3 reporting of concerns, A.8.4 incident communication, A.9.4 intended use. SOC 2: CC1 / CC2 / CC7.4.

The point: AWS gives you the evidence. ISO 42001 makes it certifiable — the policy, risk, and accountability wrapper an auditor can test.

## Honest flags

- **Three logging settings, three defaults.** CloudTrail management events are on (90 days in Event History); CloudTrail data events are off; model invocation logging is off. Unless invocation logging was already on when something happened, there is no record of what was asked or answered, and it cannot be recovered later.
- **Guardrails do not apply themselves.** A guardrail only runs when its ID and version are passed on the call (or via `ApplyGuardrail`). Audit the call sites, not the guardrail's existence.
- **The guardrail trace leaks the PII it caught — by design.** The `match` field in the guardrail trace contains the original PII value, not the masked output, so your application can use the detection result. Treat trace output with the same care as the prompt data itself, and restrict who can read it.
- **Sensitive-information filters are text-only.** They do not evaluate tool arguments or tool results in function-calling workloads — PII in those fields is neither blocked nor masked. `ANONYMIZE` on input also needs its input-specific fields set explicitly; a top-level action alone can silently do nothing on the input side.
- **Contextual grounding errors without a source.** Enabling the contextual grounding policy breaks any request that does not carry an explicit `grounding_source` (a `ValidationException`), so do not enable it for general workloads such as code generation where there is no source material in context.
- **There is no `InvocationsBlocked` metric.** The CloudWatch metric is `InvocationsIntervened` (namespace `AWS/Bedrock/Guardrails`). Alarm on the intervention rate (`InvocationsIntervened` / `Invocations`), not a metric that does not exist.

## Sources

- AWS Documentation — CloudTrail logging for Amazon Bedrock; Model invocation logging (off by default, per Region, S3 / CloudWatch Logs)
- AWS Documentation — Guardrails for Amazon Bedrock
- AWS Documentation — Remove PII from conversations by using sensitive information filters: https://docs.aws.amazon.com/bedrock/latest/userguide/guardrails-sensitive-filters.html
- AWS Documentation — Monitor Amazon Bedrock Guardrails using CloudWatch metrics: https://docs.aws.amazon.com/bedrock/latest/userguide/monitoring-guardrails-cw-metrics.html
- AWS Machine Learning Blog — model invocation logging is off by default: https://aws.amazon.com/blogs/machine-learning/access-openai-gpt-models-on-amazon-bedrock-from-canada-with-cross-region-inference/
- ISO/IEC 42001:2023 Annex A (38 controls, A.2–A.10)
- AICPA SOC 2 Trust Services Criteria (CC criteria)

## Disclaimer

This is readiness guidance, not a certification guarantee. Applicability of each control is set in your Statement of Applicability and tested by your auditor. A vendor's own certification covers the vendor, not your deployment.
