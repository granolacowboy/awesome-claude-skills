---
name: paperwork-filer
description: Files bills, receipts, statements, and PDFs into labeled folders with consistent naming for fast retrieval and finance workflows.
---

# Paperwork Filer

Give your digital paperwork a predictable home so taxes, reimbursements, and audits are painless.

## When to Use
- Receipts and statements pile up in Downloads or email saves
- You need month/quarter folders and consistent naming
- Preparing for taxes, reimbursements, or bookkeeping handoff

## Outcomes
- `Paperwork/{Taxes,Receipts,Bills,Statements}` with year/month subfolders
- Canonical filename format (e.g., `YYYY-MM-DD_vendor_amount.pdf`)
- Checklists for missing documents

## Workflow
1. **Define taxonomy**
   - Confirm categories: Receipts, Bills, Statements, Taxes, Warranties
   - Choose year/month structure depth (`YYYY/MM` vs `YYYY/Q#`)

2. **Prepare folders**
   ```bash
   BASE="[root]/Paperwork"
   mkdir -p "$BASE"/{Receipts,Bills,Statements,Taxes,Warranties}
   ```

3. **Classify**
   - Detect vendors and document type from filename text
   - Use metadata (text/ocr when available) to infer date and amount
   - Ambiguous items go to `_ToReview`

4. **Normalize filenames**
   - Pattern: `YYYY-MM-DD_vendor_type_amount.ext`
   - Remove clutter like `(1)`, `final`, `scan`
   - Log old/new names to `paperwork-renames.tsv`

5. **Move with context**
   - Route into `Category/YYYY/MM/`
   - Keep `paperwork-log.tsv` with `from`, `to`, `date`, `amount`
   - Skip encrypted PDFs unless user approves handling

6. **Reconciliation pass (optional)**
   - Generate checklist by month/category for missing statements
   - Flag duplicates and near-duplicates (same date/amount)

7. **Report**
   - Items filed, items needing review, any suspicious gaps
   - Offer monthly reminder cadence and backup guidance

## Quick Prompts
- “File all receipts into Receipts/YYYY/MM and rename with vendor + amount.”
- “Sort statements vs. bills; leave any unreadable PDFs in _ToReview.”
- “Create a missing-statements checklist for the last quarter.”
