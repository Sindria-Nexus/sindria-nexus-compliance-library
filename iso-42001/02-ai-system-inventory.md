# AI System Inventory

| | |
|---|---|
| **Company** | [Company Name] |
| **Owner** | [Name, Title — the AI governance owner] |
| **Review cadence** | Quarterly, and before any Tier 2 or Tier 3 deployment |
| **ISO 42001 mapping** | Annex A.3 (Internal organization), A.4 (Resources for AI systems), A.6 (AI system life cycle) |

## 1. Purpose

One register of every AI system the company builds, buys, or uses —
the single place a reviewer, a buyer, or a certification auditor can
look and see what AI the company runs, who owns it, what data it
touches, and how risky it is. If an AI system is not in this inventory,
it is not governed, and it should not be running.

This inventory is the working companion to the AI governance policy
(`01-ai-governance-policy.md`). Tiers are defined there (§4); this file
is where they are applied.

## 2. How to maintain it

- **Add before deployment.** A system enters the inventory before it
  goes live (Tier 2 and Tier 3), not after someone remembers it.
- **One row per system, one owner per row.** A row with no owner is
  an unowned system. A row with two owners is an argument waiting to
  happen.
- **Review quarterly.** The AI governance owner walks the inventory
  with system owners every quarter: still in use? tier still right?
  vendor terms changed? model changed? Retired systems move to the
  retired section with a date, not deleted — deletion destroys the
  audit trail.
- **Vendor features count.** When a vendor ships a new AI feature
  inside a tool you already use, that is a new row until the AI
  governance owner says otherwise.

## 3. The inventory

| Field | Meaning |
|---|---|
| System | Name of the system or feature, as staff know it |
| Purpose | What it does, in one sentence |
| Owner | One named person accountable for it |
| Built / Vendor + model | In-house, or vendor name and model/service |
| Data in | What data goes in (customer data? personal data? credentials? none?) |
| Data out | What comes back, and where it is stored |
| Tier | 1 / 2 / 3, per the AI governance policy |
| Human oversight | None / review before customer impact / review before effect + override logged |
| Impact assessment | Date completed, or "N/A (Tier 1/2)"; Tier 3 must have one |
| Vendor data terms | What the vendor does with inputs (trains? retains? unknown?) |
| Review date | Next scheduled review |
| Status | Active / Trial / Retired (with retirement date) |

### Example rows (replace with your own)

| System | Purpose | Owner | Built / Vendor + model | Data in | Tier | Oversight | Status |
|---|---|---|---|---|---|---|---|
| Support draft replies | Draft replies for support agents | [Name] | [Vendor, model] | Customer ticket text | 2 | Agent reviews before sending | Active |
| Code completion | Suggest code in the editor | [Name] | [Vendor, model] | Codebase (no customer data) | 1 | None | Active |
| Fraud scoring | Score transactions for review | [Name] | In-house model v[ ] | Transaction + account data | 3 | Analyst reviews before any account action; overrides logged | Active |

## 4. What "complete" looks like

A complete inventory has no blank owner, tier, or data-in fields; every
Tier 3 row has a dated impact assessment; every vendor row answers the
data-terms question or says "unknown" — and "unknown" rows carry no
customer data. An inventory with honest "unknowns" and no customer data
in them is stronger evidence than a polished inventory with blanks.

## 5. Evidence this inventory produces (Control AI-02)

| Evidence | Where it lives | Retention |
|---|---|---|
| Current inventory (every system owned, tiered, dated) | [inventory location] | Current + prior versions [3 years] |
| Quarterly review records (walked, updated, retired noted) | [review records] | [3 years] |
| Retired-system entries (kept, not deleted) | [inventory location] | [3 years] |

## 6. Where startups fail this control

1. **The inventory nobody updates.** Written once for a questionnaire,
   never touched again. A stale inventory is worse than none — it
   certifies, in writing, that the company does not know what AI it
   runs. The quarterly review is the control.
2. **Free tiers invisible.** The most common gap: staff using free AI
   tools that never went through any approval. If it is not in the
   inventory, it is not approved — and the fix starts with asking the
   team, not with a policy reminder.
3. **"Unknown" with customer data anyway.** Marking vendor data terms
   "unknown" while customer data flows into that system is the exact
   combination that produces breach notifications. Unknown means no
   customer data until the answer is in writing.

---

*What this template does not do: it does not discover your AI systems
for you. The inventory is only as complete as the asking is honest —
walk the team, walk the vendor list, and walk the expense report, and
the shadow systems will show up.*
