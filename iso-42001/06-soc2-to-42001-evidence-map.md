# SOC 2 to ISO 42001 Evidence Map

| | |
|---|---|
| **Company** | [Company Name] |
| **Owner** | [Name, Title — the AI governance owner] |
| **Purpose** | Show what a working SOC 2 program already proves for ISO 42001 — and exactly where the gaps are |
| **ISO 42001 mapping** | Annex A (A.2–A.10), mapped from this library's SOC 2 controls |

## 1. The insight in one paragraph

If you already run SOC 2 controls, you are closer to ISO 42001 than
you think — and further than a vendor will tell you. Roughly half the
work transfers: your risk process, vendor process, change process, and
incident process all have 42001 counterparts, and their evidence
counts twice. What does not transfer is the AI-specific core: an AI
policy, an inventory of AI systems, impact assessments, and
transparency to affected people. SOC 2 never asked you for those, so
no SOC 2 evidence answers them. The table below is the honest map:
reuse what transfers, extend what partially covers, and build what is
new — in that order.

## 2. The map

Verdicts: **Reuse** = SOC 2 evidence already answers the 42001
control, with minor relabeling. **Extend** = the SOC 2 control is the
right skeleton, but AI-specific evidence must be added. **New** = SOC 2
has no counterpart; build it from the 42001 templates.

| SOC 2 control (this library) | What it already proves | ISO 42001 Annex A | Verdict | The gap to close |
|---|---|---|---|---|
| IS-01 Security program governance | Governance exists, roles exist, reviews happen | A.2, A.3 | Extend | Add an AI policy and named AI roles — governance of the company is not governance of its AI |
| AC-01 Logical access | Who can touch systems and data | A.9 (partial) | Extend | Access control covers people reaching systems; 42001 also needs oversight of what AI systems do once running |
| AU-01 Acceptable use | Staff rules for company systems | A.9 (partial) | Extend | The AI-tools rule is a start; add the full AI acceptable-use position (approved tools, customer-data ban, concern channel) |
| IR-01 Incident response | Detect, contain, recover, learn | A.6, A.9 | Extend | Add AI incidents as a category: wrong outputs with consequences, data leaked into a model, vendor model behavior shifts |
| VM-01 Vendor management | Vendors chosen, reviewed, offboarded | A.10 | Extend | Add vendor AI terms: what vendors train on, retain, and change without notice — the standard vendor review never asked |
| CM-01 Change management | Software changes reviewed, deployed, rolled back | A.6 | Extend | Add model, prompt, and dataset changes to change control — the change type SOC 2 never saw, and the one that silently alters behavior |
| DC-01 Data classification & retention | Data classes, handling, retention | A.7 | Extend | Add training-data provenance, quality checks, and rights — classification says how data is handled; 42001 asks where training data came from and whether you may use it |
| RA-01 Risk assessment | Risks found, scored, treated, owned | A.5 | Extend | Add AI-specific impacts: bias, safety, privacy, transparency, societal effects — the risk register's categories were never built for those |
| — (no SOC 2 counterpart) | — | A.2 AI policy | **New** | Build from `01-ai-governance-policy.md` |
| — (no SOC 2 counterpart) | — | A.4 Resources / inventory | **New** | Build from `02-ai-system-inventory.md` |
| — (no SOC 2 counterpart) | — | A.5 Impact assessments | **New** | Build from `03-ai-impact-assessment-template.md` |
| — (no SOC 2 counterpart) | — | A.8 Information for interested parties | **New** | Transparency to affected people: what the system does, how to challenge an outcome — no SOC 2 control ever required this |

## 3. Read it as a sequence, not just a table

1. **Reuse first.** Point your SOC 2 evidence at the 42001 controls
   it already satisfies, and say so in your Statement of
   Applicability. Auditors accept reused evidence; they do not accept
   pretending it covers more than it does.
2. **Extend second.** The eight "Extend" rows are where most of the
   work actually is — each is a small addition to a process that
   already runs, not a new program. Do these before building anything
   new, because they are cheap and they compound.
3. **Build the four "New" rows last, in this order:** policy, then
   inventory, then impact assessments, then transparency. The order
   matters: you cannot assess impacts for systems you have not
   inventoried, and you cannot write honest transparency copy for
   systems you have not assessed.

## 4. What SOC 2 does not give you (say it plainly)

- No SOC 2 report, however clean, is an ISO 42001 certificate, and no
  auditor will treat it as one. The programs overlap; they do not
  substitute.
- SOC 2 evidence is organized around criteria (CC-series); 42001
  evidence is organized around the AI system life cycle. Reuse
  requires re-framing, not just re-filing — the same incident record
  answers both, but the story you tell with it differs.
- The four "New" rows are the certification-critical path. A company
  with perfect SOC 2 controls and no AI inventory, no impact
  assessments, and no AI policy will fail a 42001 audit on scope
  alone.

## 5. Evidence this map produces (Control AI-06)

| Evidence | Where it lives | Retention |
|---|---|---|
| Completed map (verdicts + gaps, dated) | [program location] | Current + prior versions [3 years] |
| Reuse claims tied to SOC 2 evidence locations | [program location] | [3 years] |
| Gap closure records (each "Extend" and "New" row closed with evidence) | [program location] | [3 years] |

---

*What this template does not do: it does not certify the mapping —
your certification body decides what reused evidence it accepts, and
its view governs. What it does is stop the two expensive errors teams
make here: rebuilding from scratch when half the evidence already
exists, and assuming a SOC 2 report covers AI governance when it
never asked a single AI question.*
