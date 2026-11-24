# Triage — which California AI laws apply to you?

> **NOT YET ATTORNEY-REVIEWED.** This is a public preview, not legal advice.
> **Last verified:** 21 November 2026. **Next check:** 18 February 2027.

Start here. Each law below gives a screening result, who it covers, the
questions to ask yourself, key dates, and the ISO/IEC 42001 controls that
partly help. The data behind every line is in
[data/ca_requirements.csv](../data/ca_requirements.csv) and
[data/ca_mappings.csv](../data/ca_mappings.csv).

A "Partial" control helps with part of a requirement and leaves a gap; a
"None" control does not help at all. No control fully satisfies a California
requirement on its own.

---

## AB 2013 — California AI Training Data Transparency Act

**Screening result:** Likely applies if you built a generative AI system
Californians can use.

**Who it covers:** Anyone who designs, codes, produces, or substantially
modifies a generative AI system or service for use by members of the
public. There is no size, revenue, or compute threshold anywhere in the
statute.

**Questions to ask yourself:**
- Did we build, or substantially modify, a generative AI system that
  Californians can use, released on or after 1 January 2022?
- Is the high-level summary of the datasets we used posted on our own
  website, covering at least the 12 items the statute lists?
- Do we re-post before each substantial modification is made publicly
  available?

**Key dates:** Statute effective 1 January 2025. First §3111 postings due
on or before 1 January 2026. Re-posting before each substantial
modification. The statute names no enforcer and no penalty.

**Litigation:** X.AI LLC v. Bonta — preliminary injunction denied
4 March 2026; appeal (9th Cir. No. 26-1591) argued 18 November 2026; we
could not find a decision as of 21 November 2026. The statute remains in
force.

**ISO controls that help (10):** 7.5.1, A.4.3, A.6.2.3, A.6.2.7, A.7.2,
A.7.3, A.7.4, A.7.5, A.7.6, A.8.5. They help with documenting what data
was used and how it was handled; none of them produces the public posting
the statute requires.

---

## SB 942 — California AI Transparency Act

**Screening result:** Likely applies if you create, code, or otherwise
produce a generative AI system publicly accessible in California.

**Who it covers:** Covered providers (anyone who creates, codes, or
otherwise produces a generative AI system publicly accessible in
California — the former 1,000,000-monthly-user threshold is gone);
large online platforms (2,000,000+ unique monthly users); GenAI hosting
platforms; capture-device manufacturers.

**Questions to ask yourself:**
- Do we create, code, or produce a generative AI system Californians can
  reach?
- Can a user verify whether our content was AI-generated — a free tool,
  and a latent disclosure in the content itself?
- If we license a system to someone else, do we tell them their duties,
  and do we know where to report them if they don't comply?
- Are we a large online platform, a hosting platform, or a capture-device
  maker? Those duties start later.

**Key dates:** Chapter operative 2 August 2026. Platform and hosting
duties 1 January 2027. Capture-device duties 1 January 2028.
Assistive-technology dates 1 January 2029. Penalty: $5,000 per violation,
each day a discrete violation for covered providers, platforms, and
capture-device makers. The Attorney General must establish a mechanism to
receive provider reports — whether it exists is unverified (U-08).

**ISO controls that help (3):** A.7.5, A.8.2, A.8.3. They help with
provenance information and incident reporting; none of them builds the
verification tool or the latent disclosure the chapter requires.

---

## CCPA ADMT / risk-assessment / cybersecurity-audit regulations

**Screening result:** Applies only if you are a CCPA-covered business and
do at least one of six trigger activities.

**Who it covers:** A CCPA "business" — a for-profit entity doing business
in California that determines the purposes and means of processing personal
information and meets at least one of the Civil Code §1798.140(d) tests
(annual gross revenue above the inflation-adjusted $26,625,000 threshold;
buying, selling, or sharing personal information of 100,000+ consumers or
households a year; or deriving 50%+ of annual revenue from selling or
sharing personal information) — whose processing presents significant risk
under one of six triggers: selling or sharing personal information;
processing sensitive personal information; using an automated-decisionmaking
technology (ADMT) for a significant decision; automated inference about
applicants, students, employees, or contractors; the same based on presence
in a sensitive location; or processing personal information intended to
train an ADMT for a significant decision or for facial, emotion, or
identity-verification technology.

**Questions to ask yourself:**
- Are we a CCPA-covered business?
- Do we do any of the six trigger activities — and if we use an ADMT for a
  significant decision, do we give pre-use notice, an opt-out, and access?
- Did we assess the risk before starting the processing, or are we relying
  on the backfill deadline?
- Do we meet the cybersecurity-audit test, and when is our first audit
  report due?

**Key dates:** Regulations in force 1 January 2026. Risk assessment before
initiating new significant-risk processing from 1 January 2026; processing
begun before 1 January 2026 and continuing after it must be assessed by
31 December 2027. ADMT duties (pre-use notice, opt-out, access) from
1 January 2027. First risk-assessment submissions 1 April 2028. First
cybersecurity-audit reports 1 April 2028 (revenue over $100M), 1 April 2029
($50M–$100M), 1 April 2030 (under $50M). We could not find the §7157
risk-assessment and §7124 audit-certification submission portals live
(U-06).

**ISO controls that help (18):** 4.1, 6.1.2, 6.1.4, 7.4, 8.1, 8.2, 8.4,
9.1, 9.3.2, A.2.3, A.5.2, A.5.3, A.5.4, A.5.5, A.6.2.6, A.7.2, A.8.2,
A.9.2. They help with risk assessment, records, and the audit programme;
none of them files the submission the regulations require.

---

## FEHA employment ADS regulations

**Screening result:** Likely applies if you regularly employ 5+ people and
use an automated-decision system in hiring or employment decisions in
California.

**Who it covers:** Employers regularly employing five or more people (plus
the State and political subdivisions regardless of size; non-profit
religious organisations excluded). Citation range: 2 CCR §§11008–11017.1,
plus conforming amendment §11038. Section 11038 repeats the §11009(f)
formula for pregnancy and creates no separate duty row.

**Questions to ask yourself:**
- Do we regularly employ five or more people in California?
- Do we use an automated-decision system anywhere in hiring or employment
  decisions — screening, assessments, ads, interviews, testing?
- Does the system restrict, exclude, or classify on a protected basis, or
  make inquiries that identify a person on a protected basis?
- Are we keeping the records — including ADS data — for four years?

**Key dates:** In force 1 October 2025. No phase-in. The regulations
impose no standalone duty to tell an applicant or employee that an ADS is
in use.

**Five requirements have no ISO mapping yet:** CA-FEHA-11016,
CA-FEHA-11016-1, CA-FEHA-11016-2, CA-FEHA-11017-1, and CA-FEHA-11072
are requirements without a control row, not requirements that were missed.

**ISO controls that help (4):** 4.3, 7.5.3, A.10.2, A.5.4. They help with
understanding the organisation's context, records, responsibilities, and
non-discrimination in AI; none of them is the discrimination analysis the
regulations turn on.

---

## SB 947 — No Robo Bosses Act

**Screening result:** Applies only if you use an automated-decision system
for discipline or termination decisions, and not before 1 July 2027.

**Who it covers:** Employers using an automated-decision system for
discipline or termination decisions. No small-employer exemption, no size
threshold. The statute imposes no duty on the ADS vendor or provider.

**Questions to ask yourself:**
- Do we use an ADS for discipline or termination decisions — or will we
  by 1 July 2027?
- Is a human corroborating the output with the data behind it (or other
  supporting information) before we act on it?
- Are we giving the affected employee a written post-use notice, in plain
  language, as a stand-alone communication, when we tell them the
  decision?
- Does a collective bargaining agreement waive the part, or does the
  federal aircraft / national-security carve-out apply?

**Key dates:** Operative 1 July 2027. Civil penalty $500 per violation.
"Primarily relies" is undefined, and we could not find Labor Commissioner
guidance as of 21 November 2026 (U-10). One drafting quirk to flag for an
attorney:
§1526.1(c) says "deactivation" where the rest of the part says
"termination".

**ISO controls that help (4):** 5.3, A.4.6, A.8.2, A.9.4. They help with
human oversight, roles, and incident handling; none of them is the
corroboration and notice regime the statute requires.

---

## SB 53 — Transparency in Frontier Artificial Intelligence Act

**Screening result:** Probably not: applies to developers who trained a
frontier model.

**Who it covers:** Frontier developers — anyone who trained, or initiated
the training of, a foundation model trained with more than 10^26
operations. Large frontier developers (collective annual gross revenues
with affiliates above $500M in the preceding calendar year) carry the
framework duties; all frontier developers carry the transparency-report
and incident-reporting duties.

**Questions to ask yourself:**
- Did we train a frontier model — more than 10^26 operations, counting
  the original run plus fine-tuning and reinforcement learning?
- If we are a large frontier developer, do we have a published frontier
  AI framework, reviewed at least yearly, with material modifications
  published with justification within 30 days?
- Do we publish a transparency report before or at the same time as
  deploying a new or substantially modified frontier model?
- Do we report critical safety incidents to CalOES within 15 days?

**Key dates:** In force 1 January 2026. 1 January 2027 milestones: CalOES
first annual anonymised incident report; Department of Technology first
definition-review recommendations; Attorney General first annual
covered-employee report. Civil penalty up to $1M per violation, large
developers only, recoverable only in an Attorney General civil action; no
private right of action. The CalOES reporting portal was opened 24 Nov 2026 and is live, with a
submission form for TFAIA filings; the submission-type dropdown was
expanded the same day and lists both submission paths by name (U-03
closed).

**ISO controls that help (31):** 10.1, 10.2, 4.4, 5.1, 5.2, 6.1.1, 6.1.2,
6.1.3, 7.3, 8.1, 8.2, 8.3, 9.1, 9.3.1, A.2.2, A.2.4, A.3.2, A.3.3, A.4.2,
A.5.5, A.6.1.2, A.6.2.2, A.6.2.3, A.6.2.4, A.6.2.5, A.6.2.7, A.6.2.8,
A.8.3, A.8.4, A.8.5, A.9.3. The framework, transparency report, and
incident-reporting duties map widely across the standard — but the
framework is a catastrophic-risk document for frontier models, not a
general AI policy, and no control produces the CalOES filings.

---

## SB 813 / AB 1405 — AI verification bodies and auditors

**Screening result:** Probably not: voluntary for most organisations;
mandatory registration only for AI auditors from 1 January 2029.

**Who it covers:** The Government Operations Agency (which designates
independent verification organisations and runs the AI Auditor Registry)
and AI auditors (who must register to offer, sell, or conduct a covered AI
audit from 1 January 2029). Organisations are not required to engage a
verification organisation or undergo a covered AI audit.

**Questions to ask yourself:**
- Do we conduct covered AI audits for third parties? If so, registration
  is coming.
- If we engage an auditor for a covered AI audit, is the auditor
  registered — from 1 January 2029?
- Are we treating a verification-organisation report or an auditor's
  registration as a substitute for our own supplier assessment? It is not.

**Key dates:** Both chapters effective 1 January 2027. IVO designation
criteria due 1 January 2028 (Executive Order N-9-26 targets 1 May 2027).
Registry and registration bar 1 January 2029 (Executive Order targets
1 December 2027). The November 2026 Government Operations Agency report
recommending mandatory verification oversight is a proposal, not law.

**ISO controls that help:** SB 813 — A.10.3. AB 1405 — A.10.3. A
designated verification organisation or registered auditor gives a
state-recognised route to check a supplier AI system, but use is voluntary
and registration governs who may conduct a covered AI audit, not whether
you must assess a supplier.

---

## Federal preemption

As of 21 November 2026, we could not find a federal statute that preempts
a California AI law, and we could not find a court decision holding one
preempted.

- **Executive Order 14365** (11 December 2025, 90 FR 58499) directs the
  Attorney General to stand up a DOJ AI Litigation Task Force and directs
  the Commerce Department to evaluate state AI laws. An executive order
  does not preempt state law by itself.
- **The DOJ AI Litigation Task Force** was set up by memo on 9 January
  2026. The only DOJ court action we found is its intervention on
  24 April 2026 in X.AI v. Weiser, a suit against Colorado's AI Act — not
  a California law.
- **The Commerce evaluation** was due 11 March 2026. We could not find a
  published copy.
- **The Super Intelligence Task Force** was announced 5 November 2026.
  Created by an Attorney General memorandum dated 13 October 2026, it
  folds in the AI Litigation Task Force (the memorandum merges the
  Artificial Intelligence Task Force, announced 9 January 2026, into the
  DOJ-SITF) and coordinates DOJ's AI-related criminal and civil
  enforcement. It has announced no new case against any state AI law.
- **No preemption statute has been enacted.** The Senate voted 99–1 on
  1 July 2025 to strip the ten-year moratorium on state AI laws from the
  reconciliation bill (S.Amdt. 2814 to H.R. 1, Record Vote No. 363;
  congress.gov). The enacted FY2026 defense authorization (P.L. 119-60,
  18 December 2025): we found no provision preempting state AI laws. The
  method was a full-text search of the enacted text for 'preempt,'
  'preemption,' and 'supersede'.

Preemption is a watch item for every law in this preview, not a current
qualification on any duty. Re-check at each quarterly review.

---

## Open items

Six things are still unverified. They are listed here so the preview
can be corrected in public. "What to check" is the exact step that would
close the item.

| ID | What is unverified | What to check |
|---|---|---|
| U-05 | Ninth Circuit decision, No. 26-1591 — argued 18 Nov 2026; we could not find a decision as of 21 Nov 2026 | Check the Ninth Circuit opinions page before attorney review |
| U-06 | §7157 / §7124 submission portals live — searched cppa.ca.gov 24 Nov 2026, no live portal URLs found; CPPA's Aug 2026 Audits Update says portal buildout is ongoing, with first §7157 submissions and phased §7124 certifications from 1 Apr 2028 | Re-check the CPPA website for the submission and certification portals before 1 Apr 2028 |
| U-08 | Whether the AG §22757.3(c) report-receipt mechanism exists — we could not find one on oag.ca.gov, 21 Nov 2026 | Search oag.ca.gov and leginfo for the mechanism |
| U-09 | Codified Lab. Code §§1520–1526.7 display — we could not find a codified mirror as of 21 Nov 2026; on 24 Nov 2026 the §1520, §1522, §1524, §1526 and §1526.7 code pages were opened in a browser but the body text did not render (blank), so no direct codified read; substance matches via the SB 947 chaptered text (U-13 closed). Re-check on/after 1 Jul 2027, when the sections become operative. | Open the leginfo code-section pages in a browser |
| U-10 | Labor Commissioner guidance on SB 947 — we could not find any; re-checked 21 Nov 2026 | Check dir.ca.gov / Labor Commissioner publications before publication and before 1 Jul 2027 |
| U-11 | Codified Gov. Code §§8898–8898.4 and §§11549.80–11549.86 — GOV §8898 and GOV §11549.82 code pages opened 24 Nov 2026, but body text truncated in the shared context; chapters take effect 1 Jan 2027 and are not yet codified as active law | Re-check the leginfo code-section pages on or after 1 Jan 2027 and read the remaining sections |

## Closed

| ID | What was verified | Closed |
|---|---|---|
| U-01 | Lab. Code §1107.2 confirmed by the SEC. 4 chaptered-text read on leginfo: a single interpretive sentence — loss of equity value does not count as damage to or loss of property; no standalone affirmative developer duty in §1107.2. No requirement row. | 24 Nov 2026 |
| U-02 | Lab. Code §§1107–1107.1 read via SEC. 4 of the SB 53 chaptered text on leginfo; substance matches the mirror reading (disclosure protections, anti-retaliation, notice, anonymous internal process, burden-shifting, injunctive relief, attorney's fees). | 24 Nov 2026 |
| U-03 | CalOES TFAIA Portal submission flow — portal opened 24 Nov 2026 and live; submission-type dropdown expanded the same day and lists three options: 'Submit a critical safety incident report', 'Submit a summary of any assessments of potential for catastrophic risk resulting from internal use of a frontier model', and 'File an amendment to a previously submitted incident report'. Both submission paths confirmed by name. No test submission executed. | 24 Nov 2026 |
| U-04 | Codified Civ. Code §3111 read directly on leginfo; matches the Justia mirror reading. §3110 was not opened (scope context only; no requirement row). | 24 Nov 2026 |
| U-07 | Codified BPC §§22757.1–22757.6 read directly on leginfo; substance matches the text checked (definitions, verification tool, latent disclosure, penalties, exemptions, operative date 2 Aug 2026). The four §22757.3 rows stay Medium under U-08. | 24 Nov 2026 |
| U-12 | SB 53 chaptered text (BPC §§22757.10–22757.16) read directly on leginfo; substance matches the text checked (definitions and thresholds, frontier AI framework, transparency reports, internal-use summaries, false-statement ban and redactions, incident reporting, enforcement). 46 mapping rows now 'Official text read'; 39 upgraded to High. | 24 Nov 2026 |
| U-13 | SB 947 chaptered text (Ch. 859) read directly on leginfo; substance matches the text checked (ADS definition and exclusions §1520(c), prohibited uses §1522(a), no-sole-reliance and human corroboration §1522(b)–(c), data-description right §1522(d)–(e), post-use notice §1524, anti-retaliation §1526, $500/violation penalty §1526.1(e), CBA waiver §1526.5, federal aviation/defense/space carve-out §1526.6). Codified LAB §1520, §1522, §1524, §1526 and §1526.7 pages opened 24 Nov 2026; body text blank, not directly read (U-09 still open). | 24 Nov 2026 |
| U-14 | SB 942 amendment chaptered texts (SB 1000, AB 853, AB 2713) read directly on leginfo; substance matches the text checked. One correction: §22757.3 was not amended by AB 853 — citation and Notes fixed. §22757.3 codified page also opened 24 Nov 2026 (U-07 still open). | 24 Nov 2026 |
| U-15 | SB 813 chaptered text (§§8898–8898.4) read directly on leginfo; substance matches the text checked (§8898.3 annual IVO report; §8898.4 non-mandate/non-endorsement and §8898.4(b) relevance rule). The two CA-SB813-8898 rows now 'Official text read'; confidence stays Medium under U-11. | 24 Nov 2026 |
| U-16 | AB 1405 chaptered text (§§11549.80–11549.86) read directly on leginfo; substance matches the text checked (§11549.84 investigations/removal; §11549.85 APA rulemaking; §11549.86(a)–(b) preservation and non-endorsement). The two CA-AB1405-11549-82 rows now 'Official text read'; confidence stays Medium under U-11. The §11549.83.5 advertising claim still rests on the Orrick PDF. | 24 Nov 2026 |

---

## Notes on the verification behind this triage

- **AB 2013, preliminary-injunction date:** 4 March 2026. The filed order
  (X.AI LLC v. Bonta, C.D. Cal. No. 2:25-cv-12295-JGB-SSC, Dkt. 35) was
  read in full via a mirror copy, corroborated by the
  CourtListener-hosted Dkt. 36 stipulation. A direct PACER pull has not
  been made.
- **FEHA, OAL register:** the entry is in Register 2025, No. 28-Z
  (11 July 2025), pp. 886–887 — File #2025–0515–01, filed 27 June 2025,
  effective 1 October 2025.
- **FEHA, §11072:** the individualized-assessment sentence sits in
  §11072(b)(5), item (F), read in the official CRD Final Text.
- **SB 813 / AB 1405, GovOps report:** the November 2026 Government
  Operations Agency report ("AI Safety in 2026 and Beyond") recommending
  mandatory verification oversight was read in full from the official
  GovOps PDF. It is a proposal, not law.
- **SB 947, "primarily relies":** undefined in the statute; we could not
  find Labor Commissioner guidance, FAQ, or rulemaking as of 21 November
  2026.
- **SB 942, AG mechanism:** we could not find evidence that the
  §22757.3(c) mechanism exists as of 21 November 2026. A provider's report
  under §22757.3(b)(4) still has no confirmed destination.
- **SB 53, CalOES portal:** the portal was opened 24 Nov 2026 and is live;
  the submission-type dropdown was expanded the same day and lists both
  submission paths by name (U-03 closed).
