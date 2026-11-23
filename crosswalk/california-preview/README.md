# California AI Controls Preview — Sindria Nexus Crosswalk

**Version:** v0.1-preview · **Last verified:** 21 November 2026

> **NOT YET ATTORNEY-REVIEWED.** This preview has not been reviewed by a
> California-licensed attorney. It is an educational starting point, not legal
> advice and not a substitute for advice tailored to your company. Do not rely
> on it as a compliance determination.

## What this is

A free sample of the Sindria Nexus crosswalk: California's AI laws mapped to
ISO/IEC 42001 controls, so a startup can see, law by law, which of its
governance controls help with each duty — and where the gaps are.

- **39 California requirements** across **7 laws**, mapped to ISO/IEC 42001
  controls in **123 mappings: 88 Partial, 35 None, 0 Full**. There are no Full
  mappings anywhere in this module: an ISO 42001 control can help with a
  California duty, but no control satisfies any duty on its own.
- **Confidence:** 2 High / 121 Medium (see `docs/source-verification.md`).
- **11 items are still UNVERIFIED** (U-01–U-11) — carried openly, not hidden.
  See `docs/source-verification.md` for the list and what would close each one.

### A correction to the count

An earlier version of this module listed **17** California requirements. That
count was wrong: a line-by-line audit found 9 blockers in those 17 rows,
including a wrong operative date for the CCPA risk-assessment duty, and
material duties with no row at all. The corrected module has **39
requirements** — this preview publishes the corrected 39, not the stale 17.

The preview also covers **7 laws, not 6**: SB 813 and AB 1405 (AI verification
bodies and the AI Auditor Registry) are included alongside AB 2013, SB 942,
the CCPA ADMT rules, FEHA, SB 947, and SB 53.

## Triage: does this apply to a typical startup?

"Typical startup" means a small US B2B SaaS/AI company, seed to Series B,
roughly 10–100 people, selling to enterprises, with no SOC 2 attestation yet.
It builds software (often AI features or a GenAI product), hires in California
or screens California applicants, and processes customer and employee data. It
does not train frontier-scale models and does not have $500M in revenue.

| Law | Who it covers | Does it apply to me? | Key dates | ISO 42001 controls that help | Verdict |
|---|---|---|---|---|---|
| **AB 2013** — AI Training Data Transparency Act (Civ. Code §§3110–3111) | Developers of generative AI systems made publicly available to Californians. **No size threshold** — a two-person startup is covered if it built the system. Systems and substantial modifications released on or after 1 Jan 2022. | Did you build a generative AI system Californians can use? If yes, you owe the training-data summary. | Effective **1 Jan 2025**. First §3111 postings due **1 Jan 2026**. Litigation: *X.AI v. Bonta* — preliminary injunction denied 4 Mar 2026; Ninth Circuit No. 26-1591 argued 18 Nov 2026, no decision as of 21 Nov 2026. The statute remains in force. | 10 controls — full list in `docs/triage.md` | **Applies** — if you built a GenAI system Californians can use |
| **SB 942** — California AI Transparency Act (Bus. & Prof. Code §§22757–22757.6, as amended by AB 853, SB 1000, AB 2713) | Covered providers: a person that creates, codes, or otherwise produces a GenAI system publicly accessible within California. The former 1,000,000-monthly-user threshold is gone — size no longer matters. | Did you create, code, or otherwise produce a generative AI system people in California can use? If yes: you owe a latent disclosure in AI-generated content and a free disclosure verification tool. | Chapter operative **2 Aug 2026**. Large online platform and hosting platform duties **1 Jan 2027**. Capture device duties **1 Jan 2028**. Penalties: $5,000 per violation, each day a discrete violation. | 3 controls — full list in `docs/triage.md` | **Applies** — if you create, code, or otherwise produce a GenAI system publicly accessible in California |
| **CCPA ADMT / risk-assessment / cybersecurity-audit regulations** (11 CCR §§7001, 7120–7124, 7150–7157, 7200, 7220–7222) | CCPA-covered businesses only, plus a trigger. A "business" meets at least one test: annual gross revenue above **$26,625,000**; annually buys, sells or shares personal information of **100,000+ consumers or households**; or derives **50%+ of annual revenue** from selling or sharing personal information. Then one of six §7150(b) triggers must apply (selling/sharing PI; processing sensitive PI; using ADMT for a significant decision; automated profiling of applicants, students, employees or contractors; inferences from presence in a sensitive location; processing PI to train ADMT for a significant decision or identity tech). | Is your revenue above $26,625,000 — or do you touch 100,000+ California consumers' data, or get half your revenue from selling/sharing personal information? If none, you are not a CCPA business yet. If yes, do you do any of the six trigger activities? If yes to any, a risk assessment is required **before you start** the processing. | Regulations effective **1 Jan 2026**. Risk assessment before initiating new §7150(b) processing from 1 Jan 2026; processing begun before 1 Jan 2026 and still running must be assessed by **31 Dec 2027**. Article 11 (pre-use notice, opt-out, access) from **1 Jan 2027**. First §7157 submission by **1 Apr 2028**. | 18 controls — full list in `docs/triage.md` | **Only if** you are a CCPA-covered business and do one of the six trigger activities |
| **FEHA employment ADS regulations** (2 CCR §§11008–11017.1) | California employers regularly employing **5 or more people**, counting part-time and out-of-state employees. An automated-decision system is a computational process (including AI/ML/algorithmic techniques) that makes a decision about an employment benefit or facilitates a human decision about one — resume screening, computer-based assessments, interview analysis, targeted job ads, third-party applicant/employee data analysis. | Do you regularly employ 5 or more people, with California employees or California applicants? Do you use an automated-decision system anywhere in hiring or employment? If yes to both, these regulations already apply to you. | In force **1 Oct 2025**. Personnel and employment records, expressly including selection criteria and ADS data, preserved at least **4 years**. | 4 controls — full list in `docs/triage.md` | **Applies** — if you employ 5+ people and use an ADS in hiring or employment in California |
| **SB 947** — No Robo Bosses Act (Lab. Code Part 5.5.5, §§1520–1526.7) | All employers using an automated decision system. **No size threshold and no small-employer exemption.** The duties bite only where an ADS is used for a **discipline or termination decision**. Three uses are banned for any ADS use: breaching labor, health-and-safety, employment or civil-rights law; inferring an employee's protected status; predicting and acting adversely against a worker for exercising legal rights. | Do you use an automated-decision system for discipline or termination decisions? If yes, the duties start 1 Jul 2027. If you only use AI in hiring, SB 947 is not your law — that is FEHA. | Operative **1 Jul 2027**. Civil penalty **$500 per violation**. "Primarily relies" is not defined in the statute and no Labor Commissioner guidance exists yet as of 21 Nov 2026. | 4 controls — full list in `docs/triage.md` | **Only if** you use an ADS for discipline or termination decisions — and not before 1 Jul 2027 |
| **SB 53** — Transparency in Frontier AI Act (Bus. & Prof. Code §22757.10 ff.; Lab. Code §§1107–1107.2) | **Frontier developers only.** A frontier model is a foundation model trained with more than 10^26 operations. A frontier developer is a person who trained or initiated training of one. A **large** frontier developer has collective annual gross revenue above **$500M** (with affiliates). **No duty falls on a deployer** — using someone else's frontier model does not make you a frontier developer. | Did you train (or start training) a foundation model using more than 10^26 operations? If no, SB 53 does not apply to you, however much AI you use. | In force **1 Jan 2026**. Critical safety incident reported to CalOES within **15 days** of discovery. AG civil penalty up to **$1M per violation** (large developers); no private right of action. | 31 controls — full list in `docs/triage.md` | **Probably not** — only if you trained a frontier model |
| **SB 813 / AB 1405** — AI verification bodies and auditors (Gov. Code §§8898–8898.4; §§11549.80–11549.86) | **Voluntary framework — no duty on an organisation unless it chooses to engage.** The Government Operations Agency designates independent verification organisations (SB 813) and runs an AI Auditor Registry (AB 1405). **No organisation is required to engage a designated organisation or undergo a covered AI audit.** From 1 Jan 2029, no person may offer, sell, or conduct a covered AI audit unless registered. | Do you offer or sell AI audit services in California? If yes, you must register from 1 Jan 2029. Do you want a designated independent verification organisation to assess your AI system? That is voluntary — nothing requires it. | Effective **1 Jan 2027**. IVO designation criteria published by **1 Jan 2028**. Auditor Registry established by **1 Jan 2029**; registration bar from 1 Jan 2029. | 1 control — full list in `docs/triage.md` | **Probably not** — only if you sell AI audit services or choose to engage a designated verifier |

The full triage — the complete control lists, per-law notes, the verdict
summary, and the UNVERIFIED items — is in `docs/triage.md`.

**Federal preemption:** no federal statute preempts any California AI law as
of 21 November 2026. Executive Order 14365 (11 Dec 2025) directs federal
agencies to challenge state AI laws and asks Congress to pass a preemptive
federal law, but it repeals nothing by itself. Congress has passed no such
law. Preemption is a watch item, not a current qualification on any duty
above.

## What's in this folder

| File | What it is |
|---|---|
| `README.md` | This file — the triage table, the correction note, and what is not covered. |
| `LICENSE` | Creative Commons Attribution 4.0 International (CC BY 4.0) for the material in this folder. |
| `data/ca_requirements.csv` | 39 California requirements: citation, plain-language summary, theme, effective date, who it applies to, status. |
| `data/ca_mappings.csv` | 123 mappings from ISO/IEC 42001 controls to those requirements: match strength, gap, evidence examples, rationale, source, confidence. |
| `data/data-dictionary.md` | Column-by-column definitions for both CSVs. |
| `docs/triage.md` | The full triage: complete control lists, per-law notes, verdict summary, UNVERIFIED items. |
| `docs/methodology.md` | How this was built: evidence-first method, official sources first, what "Partial" and "None" mean, and the maintenance schedule. |
| `docs/source-verification.md` | What was verified on 21 Nov 2026, what is still UNVERIFIED (U-01–U-11), and what would close each item. |

## How to use it

1. Start with the triage table above. Find the laws that apply to you.
2. Open `data/ca_requirements.csv` and filter to those laws. Each row is one
   duty, in plain language, with its citation and effective date.
3. Open `data/ca_mappings.csv` and filter to the same requirements. Each
   Partial mapping names the ISO 42001 control that helps, the gap (what the
   control does *not* cover), and the evidence that would prove the control
   operates. A None mapping is also information: that control does not help
   with that duty.
4. Treat the gaps as your to-do list. The crosswalk tells you where your
   governance already reaches and where it stops — it does not do the work.

## What this preview does NOT cover

- **No Full mappings.** Nothing here says an ISO 42001 control satisfies a
  California duty. Every Partial mapping has a gap, and the gap is the work.
- **Five FEHA requirements have no ISO control mapped at all** —
  CA-FEHA-11016, CA-FEHA-11016-1, CA-FEHA-11016-2, CA-FEHA-11017-1, and
  CA-FEHA-11072 (pre-employment practices, adverse impact, criminal history,
  and individualized assessment). The module does not yet say which controls
  help with those duties.
- **11 items are still UNVERIFIED** (U-01–U-11). The codified text of five
  laws has not yet been read directly from leginfo, two submission portals
  have not been confirmed live, and two re-checks are date-dependent. See
  `docs/source-verification.md`.
- **California only.** The full crosswalk also maps ISO/IEC 42001 to the EU AI
  Act, the NIST AI Risk Management Framework, and Colorado SB 26-189. None of
  those modules are in this preview.
- **Not attorney-reviewed, not legal advice.** See the notice at the top of
  this file.

## The full crosswalk

This preview is a free sample. The full Sindria Nexus crosswalk — all four
frameworks, the complete requirement and mapping sets, and quarterly updates —
plus the other state modules as they are published, are available from
Sindria Nexus at [sindrianexus.com](https://sindrianexus.com). The full set is
maintained as a living product with a quarterly check (next run 18 Feb 2027);
this preview is updated when the underlying data changes.

## License

The material in this folder — the CSVs, the triage, and the methodology and
verification notes — is licensed under the **Creative Commons Attribution 4.0
International Public License (CC BY 4.0)**: share and adapt it, even
commercially, as long as you give appropriate credit to Sindria Nexus, link to
the license, and indicate if changes were made. See `LICENSE` in this folder.
The rest of this repository is licensed under the MIT License — see the
repository root `LICENSE`.

## Changelog

- **v0.1-preview (21 Nov 2026):** first public preview. 39 requirements, 123
  mappings (88 Partial / 35 None / 0 Full), 7 laws. Corrected from the
  workbook's 17 requirements (see "A correction to the count" above). 5 of 16
  verification items closed in Fix Pass 2; 11 remain UNVERIFIED (U-01–U-11).
  CalOES portal URL corrected from the Fix Pass 2 record to the URL the
  CalOES page itself links (see `docs/source-verification.md`).

---

*Built by Sindria Nexus. These materials are educational starting points, not
legal advice and not a substitute for advice tailored to your company.*
