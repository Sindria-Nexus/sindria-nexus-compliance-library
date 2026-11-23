# Data dictionary — California preview CSVs

Two files, one row per record. Both are UTF-8, comma-separated, with a header
row. IDs are stable across versions: a requirement keeps its `Req_ID` and a
mapping keeps its (`Control_ID`, `Req_ID`) pair unless the underlying law
changes.

## `data/ca_requirements.csv` — 39 rows

One row per California duty (or per distinct duty-bearing provision).

| Column | Meaning |
|---|---|
| `Req_ID` | Stable ID. Format `CA-<LAW>-<CITATION>`, e.g. `CA-SB53-1107.1`, `CA-ADMT-7221`, `CA-FEHA-11072`. |
| `Framework` | Always `California` in this preview. |
| `Citation` | The law and section, e.g. `SB 53, Lab. Code §1107.1`. |
| `Plain_Summary` | The duty in plain language. This is a summary, not the statutory text — read the cited section for the operative wording. |
| `Theme` | Short topic label, e.g. `Whistleblower protections`, `Risk assessment`. |
| `Effective_Date` | Date the duty takes effect, `YYYY-MM-DD`. For phased duties this is the date the first obligation bites; see `Notes` for the phase-in schedule. |
| `Applies_To` | Who the duty falls on — the threshold, trigger, or class of person/organisation. |
| `Status` | `In effect` (duty already operative), `Phased` (operative with a phase-in schedule — see `Notes`), or `Amended` (the cited section was amended after chaptering — see `Notes`). |
| `Notes` | Verification detail: which official source the row was read from, what is still UNVERIFIED (U-01–U-11), cross-references, and attorney flags. |

## `data/ca_mappings.csv` — 123 rows

One row per (ISO/IEC 42001 control, California requirement) pair that was
assessed. Pairs not listed were not assessed — absence from this file is not a
rating.

| Column | Meaning |
|---|---|
| `Control_ID` | ISO/IEC 42001 control ID, e.g. `6.1.2`, `A.7.5`. Clauses 4–10 use plain numbers; Annex A controls use the `A.` prefix. |
| `Req_ID` | The California requirement this row assesses (joins to `ca_requirements.csv`). |
| `Match_Strength` | `Partial` — the control helps with the duty but does not satisfy it; the gap is in `Gap`. `None` — the control does not help with this duty. There are no `Full` mappings in this module. |
| `Gap` | For Partial mappings: what the control does *not* cover — the work that remains. For None mappings: why the control does not help. |
| `Evidence_Examples` | The artifacts that would prove the control operates for this duty (e.g. published framework, assessment record, notification log). Examples, not an exhaustive evidence list. |
| `Rationale` | Why this rating, tied to the cited text. |
| `Source_URL` | The source the rating rests on — an official text (leginfo bill text, CPPA approved text, CRD Final Text) or a named mirror where the official text could not be read directly. |
| `Date_Accessed` | Date the source was read, `YYYY-MM-DD`. All rows in v0.1-preview were last accessed 21 Nov 2026 or earlier. |
| `Confidence` | `High` — the rating rests on a direct read of the official text with no open codified-text leg. `Medium` — the rating is sound on the chaptered or approved text, but a codified-text or portal check is still open. 2 High / 121 Medium in v0.1-preview. |
| `Reviewer` | Blank by design. Filled only by the expert reviewer of a later pass — never by the builders of this preview. |
| `Last_Reviewed` | Blank by design, for the same reason. |

## Counts (v0.1-preview)

- Requirements: 39 — SB 53: 7, AB 2013: 1, CCPA ADMT (ADMT + cybersecurity-audit rows): 10, SB 942: 6, FEHA: 10, SB 947: 3, SB 813: 1, AB 1405: 1.
- Mappings: 123 — 88 Partial, 35 None, 0 Full.
- Five FEHA requirements have no mapping row at all: CA-FEHA-11016,
  CA-FEHA-11016-1, CA-FEHA-11016-2, CA-FEHA-11017-1, CA-FEHA-11072.
