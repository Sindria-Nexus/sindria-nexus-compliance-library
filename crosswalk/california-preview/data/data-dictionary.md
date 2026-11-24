# Data dictionary

> **NOT YET ATTORNEY-REVIEWED.** This is a public preview, not legal advice.
> **Last verified:** 21 November 2026. **Next check:** 18 February 2027.

## The files

- `ca_requirements.csv` — 40 requirements from seven California laws.
- `ca_mappings.csv` — 123 mappings of those requirements to ISO/IEC 42001
  controls: 88 Partial, 35 None, 0 Full. Confidence: 89 High, 34 Medium.
- 6 open items (U-05, U-06, U-08–U-11) are listed in
  [triage.md](../docs/triage.md#open-items) and
  [source-verification.md](../docs/source-verification.md).

## `ca_requirements.csv`

| Column | What it means |
|---|---|
| Req_ID | Stable ID for the requirement, e.g. `CA-SB53-22757-12`. IDs never change. |
| Framework | Always `California` in this preview. |
| Citation | The exact section the requirement comes from, e.g. `Bus. & Prof. Code §22757.12`. |
| Plain_Summary | The duty in plain language, written from the section text. |
| Theme | A short label for the duty (e.g. "Frontier AI framework", "Pre-use notice"). |
| Effective_Date | The date the duty takes effect, YYYY-MM-DD. For phased duties this is the date the duty in the row takes effect; the Notes field gives the other dates. |
| Applies_To | Who the duty binds. |
| Status | `In effect` (20), `Phased` (18 — the duty has later phase-in dates, given in Notes), or `Amended` (1). |
| Notes | Context: related rows, litigation, verification notes, and open-item IDs where a source is a mirror, secondary, or unconfirmed. |
| Snapshot_Date | 2026-11-21 on every row — the date the data was snapshotted. See below. |

This file has no Reviewer column. Review of a requirement is recorded in
the open-items list, not on the row.

## `ca_mappings.csv`

| Column | What it means |
|---|---|
| Control_ID | The ISO/IEC 42001 clause or Annex A control, e.g. `A.6.2.3` or `7.5.1`. |
| Req_ID | The requirement this mapping is about (matches `ca_requirements.csv`). |
| Match_Strength | `Partial` — the control helps with part of the requirement; the Gap field says what is left. `None` — the control does not help at all. There are no Full matches in this preview. |
| Gap | What the control leaves uncovered. This is the most important column: it is why a Partial is not a pass. |
| Evidence_Examples | Records an auditor would look for. |
| Rationale | Why the control maps to the requirement the way it does. |
| Source_URL | The source the mapping's requirement text rests on. |
| Source_Type | How that source was read. See below. |
| Date_Accessed | The date the source was actually read, where one is established (YYYY-MM-DD). Blank where no real access date is established — a blank is not a missing value to be filled in from the snapshot date. |
| Snapshot_Date | 2026-11-21 on every row — the date the data was snapshotted. See below. |
| Confidence | `High` or `Medium`. See below. |
| Reviewer | Blank by design. Filled only by the expert reviewer of a later pass. |
| Last_Reviewed | Blank by design. Filled only by the expert reviewer of a later pass. |

## Source_Type

| Value | What it means | Rows |
|---|---|---|
| Official text read | The text was read directly in an official source. | 123 |
| Official URL cited; direct read not confirmed | The URL is the official location of the text, but no direct read of the official page is established. The text behind the row was checked another way (a mirror or a cross-check). Each such source group has an open item. | 0 |
| Mirror | The text was read through a mirror of the official text (e.g. Justia, public.law). | 0 |
| Secondary (law firm) | The text was read through a law-firm document (Orrick PDF). | 0 |

## Confidence

- **High** — the requirement's text was read directly in an official
  source, the ISO control's scope was confirmed from a public description,
  and no open item bears on that requirement. 89 rows: 28 resting on the
  official CPPA approved text, 5 resting on the official CRD Final
  Text, 46 resting on the SB 53 chaptered text read directly on
  leginfo 24 November 2026, and 10 resting on the SB 942 codified sections
  and chaptered texts read directly on leginfo 24 November 2026. The 28 CPPA rows were held at Medium pending a spot-check; the
  spot-check was confirmed 24 November 2026 and they upgraded to High.
- **Medium** — everything else. Medium explicitly covers four cases: a
  text read through a mirror, a text read through a secondary document,
  an official source whose direct read is not confirmed, and an official
  read where an open item bears on the requirement. The last case covers
  four rows: the two mappings of CA-ADMT-7157 and the two of
  CA-CCPA-CYBER-7124, where the submission portals (U-06) are part of the
  requirement and could not be found. Medium does not mean the mapping is
  wrong; it means the underlying text was not read directly in the
  official source, or an open item still bears on it, so the mapping
  should be checked against the official text before it is relied on.
  34 rows.

This definition is the same in the README, the methodology, and this file.

## Snapshot_Date and Date_Accessed

- **Snapshot_Date (2026-11-21)** is the date this data was frozen. It is
  the same on every row of both files.
- **Date_Accessed** is the date a source was actually read, where one is
  established. It is filled on 123 mapping rows and blank
  on 0. A blank Date_Accessed means the real access date is unknown — it
  must not be filled in from the snapshot date.
