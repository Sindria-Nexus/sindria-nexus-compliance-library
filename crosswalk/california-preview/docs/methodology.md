# Methodology

> **NOT YET ATTORNEY-REVIEWED.** This is a public preview, not legal advice.
> **Last verified:** 21 November 2026. **Next check:** 18 February 2027.

## What this preview does

It maps seven California AI laws against ISO/IEC 42001 controls: 39
requirements, 123 mappings (88 Partial, 35 None, 0 Full). A Partial means
the control helps with part of the requirement and leaves a gap, stated in
the mapping's Gap field. A None means the control does not help at all. No
control fully satisfies a California requirement on its own — the laws and
the standard do different jobs, and the preview says so rather than
forcing a fit.

## Sources — official first

Official sources come first: the California Legislative Information
system (leginfo) for chaptered bill text and codified sections, the
California Privacy Protection Agency for the CCPA regulations, the Civil
Rights Department for the FEHA regulations, the Office of Administrative
Law for the register entry, the Governor's office and the Government
Operations Agency for executive orders and reports, and the Attorney
General's office for SB 53.

One claim still rests on a secondary document as its sole source,
because the official page could not be read directly:

- **AB 1405 §11549.83.5 advertising claim** — Orrick law-firm PDF (not yet read from the official source).

The claim is flagged in the Notes on its row. It is not presented as if the official text had been read.
Every other row's source route is recorded the same way: `Source_Type` is
"Official text read", "Official URL cited; direct read not confirmed",
"Mirror", or "Secondary (law firm)". See [sources.md](sources.md) for the
full source table and [source-verification.md](source-verification.md) for
what is still open.

## Confidence

- **High** — the requirement's text was read directly in an official
  source, the ISO control's scope was confirmed from a public description,
  and no open item bears on that requirement. 89 of the 123 mappings are
  High: 28 rows resting on the official CPPA approved text, 5 rows
  resting on the official CRD Final Text, 46 rows resting on the SB 53
  chaptered text read directly on leginfo 24 November 2026, and 10 rows
  resting on the SB 942 codified sections and chaptered texts read
  directly on leginfo 24 November 2026. The 28 CPPA rows were held at
  Medium pending a spot-check; the spot-check was confirmed 24 November
  2026 and they upgraded to High.
- **Medium** — everything else. Medium explicitly covers four cases: a
  text read through a mirror, a text read through a secondary document
  (such as a law-firm PDF), an official source whose direct read is not
  confirmed, and an official read where an open item bears on the
  requirement. The last case covers four rows: the two mappings of
  CA-ADMT-7157 and the two of CA-CCPA-CYBER-7124, where the submission
  portals (U-06) are part of the requirement and could not be found.
  Medium does not mean the mapping is wrong; it means the underlying text
  was not read directly in the official source, or an open item still
  bears on it, so the mapping should be checked against the official text
  before it is relied on. 34 of the 123 mappings are Medium.

## How a requirement was built

Each requirement states the duty in plain language, cites the exact
section, and records its effective or operative date. Each mapping states
the control, the match (Partial or None), the gap the control leaves, and
evidence examples — the records an auditor would look for. The ISO/IEC
42001 control scope was confirmed from public descriptions of the
controls, not from the paid standard. No text from the standard is
reproduced here — only clause numbers, control titles, and original
summaries.

## California scope

The preview covers seven laws: AB 2013, SB 942, the CCPA ADMT /
risk-assessment / cybersecurity-audit regulations, the FEHA employment ADS
regulations (2 CCR §§11008–11017.1, plus conforming amendment §11038 —
§11038 repeats the §11009(f) formula and creates no separate duty row),
SB 947, SB 53, and SB 813 / AB 1405. It does not cover any other
California AI-related law. Five FEHA requirements have no ISO mapping yet
(CA-FEHA-11016, CA-FEHA-11016-1, CA-FEHA-11016-2, CA-FEHA-11017-1,
CA-FEHA-11072) — they are requirements without a control row.

## What "last verified" means

"Last verified: 21 November 2026" is the date the sources in
[sources.md](sources.md) were checked. The data files carry a
`Snapshot_Date` of 2026-11-21 on every row. `Date_Accessed` in the
mappings file is the date a source was actually read, where one is
established; it is blank where no real access date is established — a blank
is not a missing value to be filled in from the snapshot date.

## Maintenance

This preview is re-checked quarterly, next on 18 February 2027, and sooner
if any of these happen:

- **A dated re-check comes due:** U-05 (Ninth Circuit decision in
  No. 26-1591) and U-10 (Labor Commissioner guidance on SB 947).
- **The SB 813 / AB 1405 chapters take effect** (1 January 2027) — the
  codified display (U-11) is best checked on or after that date.
- **The §7157 / §7124 portals go live** (U-06) — the first submission
  deadline is 1 April 2028.
- **Any California amendment** to one of the seven laws, or a new
  regulation or guidance under one of them.
- **A court decision** affecting one of the seven laws — including any
  decision in X.AI v. Bonta (AB 2013) or any federal preemption ruling.

## Limits

- This preview is not attorney-reviewed and is not legal advice.
- It does not assess whether any organisation is compliant.
- It does not cover federal law except for the preemption position in
  [triage.md](triage.md#federal-preemption), which is a watch item, not a
  legal conclusion.
- The ISO/IEC 42001 control descriptions are original summaries, not
  quotations from the standard.
