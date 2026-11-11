Last verified: November 11, 2026

# Salesforce Agentforce (Einstein Trust Layer) — Evidence Mapping

## What the platform is

Salesforce Agentforce is Salesforce's agent platform, built on the CRM and Data 360. Every Agentforce interaction passes through the **Einstein Trust Layer**, a secure AI architecture built into the Salesforce platform that sits between your users, your CRM data, and external LLMs. Its audit trail, toxicity scores, and feedback log are stored in Data 360 via the **Generative AI Audit and Feedback Trail**.

## Evidence mapping

Status key: **In hand** — the artifact satisfies the control as evidence. **Wrapper** — the artifact counts once your process around it is documented.

| Platform artifact | ISO 42001 Annex A | SOC 2 CC | Status | Wrapper note |
|---|---|---|---|---|
| **Generative AI Audit & Feedback Trail.** Prompt ID, original and PII-masked prompt, toxicity scores, and outputs, logged in Data 360. | A.6.2.8 Recording of event logs; A.6.2.6 Operation and monitoring | CC7.2 System operations; CC4.1 Monitoring activities | In hand | Audit and Feedback data collection must be turned on (on by default when Agentforce is turned on for orgs with a single dataspace); retention in your Data 360 instance is yours to set. |
| **Toxicity detection and prompt defense.** Prompts and responses scored in five categories (violence, sexual, profanity, hate, physical), each 0–1 with an overall score; prompt defense adds system instructions that reduce the chance the model follows injected instructions. | A.6.2.4 Verification and validation; A.9.2 Processes for responsible use | CC5.3 Control activities; CC7.2 System operations | Wrapper | Needs thresholds and a response process. Prompt defense reduces injection risk — it does not eliminate it, especially indirect injection via grounded data. |
| **Zero data retention via the secure gateway.** Model providers retain nothing and train on nothing; policies enforced on every call. | A.10.3 Suppliers; A.6.2.5 Deployment | CC6.1 Logical access; CC6.6 System boundaries | In hand | Applies to third-party LLM providers under Salesforce's zero-retention agreements. Salesforce notes that use of other features, including agents, may result in data storage elsewhere — the zero-retention promise is about the model provider, not your Salesforce org. |
| **Data masking and demasking.** PII replaced with placeholders before the prompt reaches the LLM; real values restored in the response. | A.7.2 Data for development and enhancement; A.7.6 Data preparation | CC6.1 Logical access; CC7.2 System operations | Wrapper — see flags | **Data masking for LLMs is disabled for Agentforce agents.** It is available for embedded features (e.g. Service Replies, Work Summaries, Prompt Builder). For Agentforce, PII is protected in transit and by zero retention, not masked before the LLM. Do not claim masking for an Agentforce deployment. |
| **Secure data retrieval and dynamic grounding.** The agent only pulls data the user may see, and answers are grounded in it. | A.7.3 Acquisition of data; A.7.5 Data provenance | CC6.1 Logical access; CC7.2 System operations | In hand | Grounding honours the executing user's sharing rules and field-level security. |
| **User feedback, captured per response.** Thumbs up/down with reasons, plus accept, regenerate, modify, and decline actions. | A.6.2.6 Operation and monitoring; A.9.2 Processes for responsible use | CC4.1 Monitoring activities; CC4.2 Evaluation of deficiencies | Wrapper | Needs a documented review cadence. |

## What Salesforce does not give you — the gap band (the engagement)

No platform artifact covers these. They are the management system around the evidence — and they are the engagement.

- **Policy & scope** — A.2.2 AI policy, A.2.3 alignment with your other policies, and the Statement of Applicability deciding which of the 38 controls apply. SOC 2: CC1 governance.
- **Impact & risk** — A.5.2–A.5.5 impact assessments for individuals, groups, and society, plus the AI risk register. SOC 2: CC3 risk assessment.
- **Accountability & response** — A.3.2 named roles, A.3.3 reporting of concerns, A.8.4 incident communication, A.9.4 intended use. SOC 2: CC1 / CC2 / CC7.4.

The point: Salesforce gives you the evidence. ISO 42001 makes it certifiable — the policy, risk, and accountability wrapper an auditor can test.

## Honest flags

- **Data masking is disabled for Agentforce agents.** This is stated in Salesforce Help and Trailhead ("Data masking for LLMs is disabled for agents"). The masking row above is therefore a wrapper, not in-hand evidence for an Agentforce deployment — and the audit trail's "PII-masked prompt" field only contains a masked prompt where masking is actually on. Verify per surface, not per platform.
- **Prompt defense is not a guarantee.** Salesforce's own framing is that prompt defense "decreases the likelihood" of unintended outputs. It does not make the model bulletproof against jailbreaks, and it does not cover indirect injection — a malicious instruction embedded in an email, case description, or Knowledge article that gets grounded into a prompt.
- **Audit-trail retention is two-layered.** Audit and feedback data are stored in your Data 360 instance with a retention period you control, and Salesforce also keeps them for 30 days for compliance purposes. Set and document your Data 360 retention; do not assume the 30-day Salesforce copy is your evidence store.
- **Toxicity scores are 0–1 per category, not a pass/fail.** The score accompanies the response and is logged; whether anything is blocked depends on the thresholds you configure. No threshold, no control.
- **Data 360 is a prerequisite.** The Trust Layer's audit trail depends on Data 360; without it, the audit trail cannot be enabled and some Trust Layer features are unavailable.

## Sources

- Salesforce Help — Einstein Trust Layer: https://help.salesforce.com/s/articleView?id=sf.generative_ai_trust_layer.htm
- Salesforce Help — Toxicity Detection: https://help.salesforce.com/s/articleView?id=ai.generative_ai_trust_toxicity_detection.htm&language=en_US&type=5
- Salesforce Help — About Generative AI Audit and Feedback Data: https://help.salesforce.com/s/articleView?id=generative_ai_feedback_about.htm&language=en_US&type=5
- Salesforce Help — Trust and Agentforce (zero retention; data masking limitations in Agentforce): https://help.salesforce.com/s/articleView?id=copilot_trust.htm&language=en_US&type=5
- Trailhead — Follow the Prompt Journey (Einstein Trust Layer): https://trailhead.salesforce.com/content/learn/modules/the-einstein-trust-layer/follow-the-prompt-journey
- Trailhead — Follow the Response Journey (Einstein Trust Layer): https://trailhead.salesforce.com/content/learn/modules/the-einstein-trust-layer/follow-the-response-journey
- ISO/IEC 42001:2023 Annex A (38 controls, A.2–A.10)
- AICPA SOC 2 Trust Services Criteria (CC criteria)

## Disclaimer

This is a mapping aid, not legal advice or a compliance guarantee. ISO 42001 or SOC 2 evidence does not equal legal compliance. Applicability of each control is set in your Statement of Applicability and tested by your auditor. A vendor's own certification covers the vendor, not your deployment.
