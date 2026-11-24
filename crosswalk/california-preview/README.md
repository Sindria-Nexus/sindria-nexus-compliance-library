# California AI Laws x ISO/IEC 42001 Controls — Preview

> **NOT YET ATTORNEY-REVIEWED.** This is a public preview, not legal advice.
> It maps seven California AI laws against ISO/IEC 42001 controls so you can
> see where the controls help and where they don't. It is not a compliance
> opinion, and it is not a substitute for advice from a California-licensed
> attorney.

**Version:** v0.1-preview
**Last verified:** 21 November 2026
**Next check:** 18 February 2027
**License:** CC BY 4.0 (see [LICENSE](LICENSE))

## Does this apply to you?

| Law | Screening result | Who it covers | Key date |
|---|---|---|---|
| AB 2013 — AI training-data transparency | Likely applies if you built a generative AI system Californians can use | Anyone who designs, codes, produces, or substantially modifies a generative AI system for public use | In force; first postings due 1 Jan 2026 |
| SB 942 — AI Transparency Act | Likely applies if you create, code, or otherwise produce a generative AI system publicly accessible in California | Covered providers, large online platforms, GenAI hosting platforms, capture-device makers | Operative 2 Aug 2026; platform duties 1 Jan 2027 |
| CCPA ADMT / risk-assessment / cybersecurity-audit regulations | Applies only if you are a CCPA-covered business and do at least one of six trigger activities | CCPA-covered businesses doing significant-risk processing | In force 1 Jan 2026; first submissions 1 Apr 2028 |
| FEHA employment ADS regulations | Likely applies if you regularly employ 5+ people and use an automated-decision system in hiring or employment decisions in California | Employers regularly employing five or more people | In force 1 Oct 2025 |
| SB 947 — No Robo Bosses Act | Applies only if you use an automated-decision system for discipline or termination decisions, and not before 1 Jul 2027 | Employers using an ADS for discipline or termination decisions | Operative 1 Jul 2027 |
| SB 53 — Transparency in Frontier AI Act | Probably not: applies to developers who trained a frontier model | Frontier developers; large frontier developers for the framework duties | In force 1 Jan 2026 |
| SB 813 / AB 1405 — AI verification bodies and auditors | Probably not: voluntary for most organisations; mandatory registration only for AI auditors from 1 Jan 2029 | Government Operations Agency and AI auditors; organisations are not required to engage an auditor | Effective 1 Jan 2027; registry and registration bar 1 Jan 2029 |

The screening result is a starting point, not a verdict. [Read the full
triage](docs/triage.md) for who each law covers, the questions to ask
yourself, key dates, and which ISO controls help.

## What this preview is

- **40 requirements** from seven California laws, mapped to ISO/IEC 42001
  controls in **123 mappings**: 88 Partial, 35 None, 0 Full. No control fully
  satisfies a California requirement on its own — the laws and the standard
  do different jobs.
- **89 High / 34 Medium confidence.** High means the requirement's text
  was read directly in an official source, the ISO control's scope was
  confirmed from a public description, and no open item bears on that
  requirement. Medium covers everything else: reads through a mirror or a
  secondary document, official sources whose direct read is not confirmed,
  and official reads where an open item bears on the requirement (four
  rows). The 28 rows resting on the official CPPA approved text were held
  at Medium pending a spot-check; the spot-check was confirmed 24 November
  2026 and they are now High. See [methodology](docs/methodology.md).
- **6 open items.** Six things are still unverified — mostly direct
  reads of official texts that could not be opened, and two submission
  portals we could not find live. They are listed openly in
  [triage](docs/triage.md#open-items) and
  [source verification](docs/source-verification.md). Ten items (U-01, U-02, U-03, U-04, U-07, U-12,
  U-13, U-14, U-15, U-16) are closed: see [triage](docs/triage.md#closed). Nothing is hidden
  behind a confidence score.

## Federal preemption

As of 21 November 2026, we could not find a federal statute that preempts
a California AI law, and we could not find a court decision holding one
preempted. An executive order (EO 14365, 11 December 2025) directs a
Justice Department task force and a Commerce Department evaluation, but an
executive order does not preempt state law by itself. On 5 November 2026
DOJ announced the Super Intelligence Task Force, which folds in the AI
Litigation Task Force and coordinates DOJ's AI-related enforcement; it has
announced no new case against any state AI law. This is a watch item, not
a current qualification on any duty. The full position, with dates and
sources, is in [triage](docs/triage.md#federal-preemption).

## How to use it

1. **Start with the triage** ([docs/triage.md](docs/triage.md)) — it tells
   you which laws are likely to apply to you and what to ask yourself.
2. **Check the data** ([data/ca_requirements.csv](data/ca_requirements.csv),
   [data/ca_mappings.csv](data/ca_mappings.csv)) — the 40 requirements and
   their 123 mappings, with the gap each mapping leaves and the evidence
   examples an auditor would look for.
3. **Check the sources** ([docs/sources.md](docs/sources.md)) — every
   official source used, with the date it was checked and what could not be
   confirmed.
4. **Read the method** ([docs/methodology.md](docs/methodology.md)) —
   how the mappings were built, what the confidence ratings mean, and what
   this preview does not do.

## Limits

- **Seven laws, not every California AI-related law.** This preview covers
  AB 2013, SB 942, the CCPA ADMT / risk-assessment / cybersecurity-audit
  regulations, the FEHA employment ADS regulations, SB 947, SB 53, and
  SB 813 / AB 1405. It does not cover any other California AI-related law.
- **Not attorney-reviewed.** The contents have not been reviewed by a
  California-licensed attorney.
- **Five FEHA requirements have no ISO mapping yet** (CA-FEHA-11016,
  CA-FEHA-11016-1, CA-FEHA-11016-2, CA-FEHA-11017-1, CA-FEHA-11072) —
  they are requirements without a control row, not requirements that were
  missed.
- **The ISO/IEC 42001 control scope was confirmed from public descriptions
  of the controls, not from the paid standard.** No text from the standard
  is reproduced here — only clause numbers, control titles, and original
  summaries.
- **Dates are a snapshot.** Sources were verified on 21 November 2026
  (see `Snapshot_Date` in the data files). Laws change; the next check is
  18 February 2027.

## How to cite this preview

> California AI Laws x ISO/IEC 42001 Controls Preview, Sindria Nexus,
> CC BY 4.0 — sindrianexus.com

## Found an error?

Open an issue at
[github.com/Sindria-Nexus/sindria-nexus-compliance-library/issues](https://github.com/Sindria-Nexus/sindria-nexus-compliance-library/issues)
with the law, the section, an official link, and the date you checked it.
See [CONTRIBUTING.md](CONTRIBUTING.md) for what a correction needs.

## Disclaimer

This preview is provided for general information only. It is not legal
advice, and it does not create any attorney–client relationship. California
AI law is changing quickly; check the official sources linked in
[docs/sources.md](docs/sources.md) and get advice from a California-licensed
attorney before acting on anything here. Sindria Nexus is not affiliated
with ISO, IEC, or any government body.

## What's in this folder

| File | What it is |
|---|---|
| [README.md](README.md) | This file |
| [LICENSE](LICENSE) | CC BY 4.0 license for this folder |
| [NOTICE.md](NOTICE.md) | Attorney-review status, not legal advice, preview status |
| [CONTRIBUTING.md](CONTRIBUTING.md) | How to report an error or propose a correction |
| [CHANGELOG.md](CHANGELOG.md) | Version history for this preview |
| [data/ca_requirements.csv](data/ca_requirements.csv) | The 40 California requirements |
| [data/ca_mappings.csv](data/ca_mappings.csv) | The 123 mappings to ISO/IEC 42001 controls |
| [data/data-dictionary.md](data/data-dictionary.md) | What every column in the CSVs means |
| [docs/triage.md](docs/triage.md) | Per-law screening, key dates, ISO controls that help, open items |
| [docs/methodology.md](docs/methodology.md) | How the mappings were built and what the ratings mean |
| [docs/source-verification.md](docs/source-verification.md) | What was verified, what was not, and what to check |
| [docs/sources.md](docs/sources.md) | Every official source used, with links and dates checked |

## The full crosswalk

This preview is the California module of a larger crosswalk (ISO/IEC 42001
against the EU AI Act, the NIST AI Risk Management Framework, Colorado
SB 26-189, and California). The full crosswalk is not published yet. The
full crosswalk is in development; details at sindrianexus.com. The
California module is published first as a standalone preview so it can be
corrected in public before the full release.

## Changelog

See [CHANGELOG.md](CHANGELOG.md).
