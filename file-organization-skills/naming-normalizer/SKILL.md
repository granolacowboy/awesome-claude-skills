---
name: naming-normalizer
description: Renames messy files into consistent, searchable patterns with previews, conflict checks, and reversible logs.
---

# Naming Normalizer

Enforce clear, predictable filenames so searches and sorts work every time.

## When to Use
- Files are full of “final_v2(1)” chaos
- Need consistent naming before handoff or archiving
- Want sortable patterns for receipts, reports, or media

## Outcomes
- Standardized naming pattern (e.g., `YYYY-MM-DD_topic_context.ext`)
- Preview of proposed renames with collision checks
- Undo-ready rename log

## Workflow
1. **Gather requirements**
   - Choose pattern elements: date, topic, owner, version
   - Pick delimiter (`-` or `_`) and casing style (kebab/snake/title)
   - Confirm scope and exclusions (skip exports, hidden files)

2. **Inventory targets**
   ```bash
   find [target] -maxdepth [depth] -type f \
     ! -path "*/.git/*" ! -path "*/node_modules/*" -print > /tmp/rename-targets
   ```

3. **Propose new names**
   - Derive dates from metadata when absent
   - Normalize whitespace, remove `(1)`/`copy`/`final` noise
   - Map to pattern and list as preview table (old → new)

4. **Validate**
   - Check for collisions and length limits
   - Flag ambiguous items for manual input (ask for topic/owner)
   - Create `rename-plan.tsv` (old, new, reason)

5. **Execute renames**
   ```bash
   while read -r old new; do
     mv -n "$old" "$new" || echo "$old" >> rename-conflicts.log
   done < rename-plan.tsv
   ```
   - Preserve extensions; ensure case sensitivity on target FS
   - Keep `rename-backup.tsv` for undo (new → old)

6. **Wrap-up**
   - Summary of renamed, skipped, conflicted files
   - Offer to propagate pattern to future captures (e.g., screenshot naming)

## Quick Prompts
- “Normalize receipts to YYYY-MM-DD_vendor_amount.pdf and skip anything already conforming.”
- “Rename design exports with kebab-case and drop all '(1)' suffixes.”
- “Preview renames only; don’t apply until I say go.”
