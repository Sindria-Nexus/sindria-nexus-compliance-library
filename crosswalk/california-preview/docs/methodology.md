# Methodology — California preview

> **NOT YET ATTORNEY-REVIEWED.** This preview has not been reviewed by a
> California-licensed attorney. It is an educational starting point, not legal
> advice and not a substitute for advice tailored to your company.

## Evidence first

This crosswalk is built around the question an auditor or an enterprise buyer
actually asks — never "do you have a policy?" but "show me it working." Every
mapping names the evidence that would prove the control operates for the duty.
A control with no evidence is a claim, not a control.

## Official sources first

Every requirement starts from the official text: the chaptered bill text on
leginfo, the OAL-approved regulation text, or the filed Final Text from the
issuing agency. Secondary sources (law-firm alerts, committee analyses,
mirrors such as Justia or public.law) are used only to cross-check, never as
the sole basis for a duty — and where the official text could not be read
directly, the item is marked **UNVERIFIED** and listed in
`docs/source-verification.md` rather than filled in from a secondary source.

Sources used for v0.1-preview, in order of preference:

1. **leginfo.legislature.ca.gov** — chaptered bill texts (SB 53, SB 942 as
   amended by AB 853 / SB 1000 / AB 2713, SB 947, SB 813, AB 1405, AB 2013).
2. **cppa.ca.gov** — the approved CCPA regulation text (11 CCR §§7001,
   7120–7124, 7150–7157, 7200, 7220–7222).
3. **calcivilrights.ca.gov** — the CRD Final Text of the FEHA automated-decision
   system regulations (2 CCR §§11008–11017.1), filed 27 Jun 2025, effective
   1 Oct 2025; OAL Register 2025, No. 28-Z (11 Jul 2025), pp. 886–887.
4. **govops.ca.gov** — the Government Operations Agency report "AI Safety in
   2026 and Beyond" (SB 813 / AB 1405 context — a proposal, not law).
5. **oag.ca.gov** — Attorney General pages (SB 53 context; the §22757.3(c)
   report mechanism was searched and not found — see U-08).
6. Named mirrors only where the official text was unreachable: Justia (Lab.
   Code §1107.2 substance; Civ. Code §3111), public.law (Lab. Code §1107.1),
   CourtListener (the *X.AI v. Bonta* stipulation). Each mirror use is flagged
   in the row's Notes.

## How a mapping is rated

Each (control, requirement) pair gets one of two ratings. There is no third
rating in this module, deliberately: no ISO 42001 control satisfies a
California duty on its own.

- **Partial** — the control helps with the duty. The `Gap` column states what
  the control does *not* cover. The gap is the work.
- **None** — the control does not help with this duty. A None rating is
  information, not a failure: it stops a team from claiming coverage it does
  not have.

**Confidence** is separate from the rating:

- **High** — the rating rests on a direct read of the official text with no
  open codified-text leg. (2 rows in v0.1-preview.)
- **Medium** — the rating is sound on the chaptered or approved text, but a
  codified-text or portal check is still open. (121 rows.)

A rating is never upgraded on the strength of a secondary source alone.

## What "last verified" means

"Last verified 21 November 2026" means: the sources named in
`docs/source-verification.md` were read on or before that date, and the data
reflects the law as it stood then. It does not mean the law has not changed
since, and it does not mean every item was verified — 11 items were not (see
U-01–U-11). Dates in the CSVs are the dates each source was accessed.

## What was corrected before publication

The module this preview is drawn from was audited line by line before
publication. The audit found 9 blockers in the original 17 requirement rows —
including a wrong operative date for the CCPA risk-assessment duty (the duty
applies from the regulations' 1 Jan 2026 effective date, not 1 Jan 2027) — and
material duties with no row at all. The corrected module has 39 requirements
and 123 mappings. This preview publishes the corrected data. The full
correction history is in the preview README's changelog note.

## Maintenance

The crosswalk is checked quarterly. The next scheduled run is **18 Feb 2027**
(then roughly every three months). A run is brought forward if a checked item
resolves — a Ninth Circuit decision in *X.AI v. Bonta* (No. 26-1591), Labor
Commissioner guidance on SB 947, the SB 813 / AB 1405 chapters taking effect
on 1 Jan 2027, or a §7157 / §7124 portal going live — or if a law is amended.
Between runs, corrections are recorded in the README changelog with their
dates.

## Limits

- This is a **screening** tool, not a compliance determination. A Partial
  mapping does not mean "compliant," and a None mapping does not mean "in
  breach" — it means the control does not help with that duty.
- **No federal preemption** applies to any California AI law as of
  21 November 2026. That is a watch item: an executive order alone does not
  preempt state law, and Congress has passed no preemptive federal AI law.
- Thresholds are stated as they stood on 21 Nov 2026. The CCPA revenue
  threshold ($26,625,000) is inflation-adjusted, next adjustment 1 Jan 2027.
- Five FEHA requirements (CA-FEHA-11016, CA-FEHA-11016-1, CA-FEHA-11016-2,
  CA-FEHA-11017-1, CA-FEHA-11072) have no ISO control mapped. The module does
  not yet say which controls help with those duties.
