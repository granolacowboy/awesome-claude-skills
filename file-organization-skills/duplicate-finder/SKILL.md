---
name: duplicate-finder
description: Finds duplicate files safely using hashes and metadata, then guides decisions on what to keep, consolidate, or archive.
---

# Duplicate Finder

Surface duplicate files with transparent evidence and safe remediation steps.

## When to Use
- Storage is ballooning because of copy-pasted files
- You inherited a drive with overlapping folders
- Need a pre-backup cleanup to reduce size
- Want a clear keep/delete/merge recommendation

## Capabilities
- Exact duplicate detection via hashing
- Name and size-based similarity triage
- Side-by-side evidence with dates and sizes
- Conservative, confirmation-first deletion

## Workflow
1. **Define search scope**
   - Target directories (e.g., `~/Documents`, external drives)
   - Exclusions (e.g., node_modules, .git, photo libraries)
   - Size thresholds (skip >4GB unless approved)

2. **Collect candidates**
   ```bash
   find [scope] -type f \
     ! -path "*/.git/*" \
     ! -path "*/node_modules/*" \
     -size -4G -print0 > /tmp/dup-list
   ```

3. **Hash and group**
   ```bash
   xargs -0 md5sum < /tmp/dup-list | sort > /tmp/dup-hashes
   awk 'prev==$1 {print prev, $2, line} {line=$0; prev=$1}' /tmp/dup-hashes
   ```
   - Present sets with path, size, modified date
   - Highlight safer keep options (newest, canonical location)

4. **User decisions**
   - Options: keep newest, keep in chosen root, archive extras, or ignore
   - Offer dry-run move to `Duplicates_To_Delete/` before permanent removal
   - Never delete without explicit approval

5. **Execute safely**
   - Create `duplicate-actions.tsv` log (hash, action, from, to)
   - Use `mv -n` to avoid overwrites; preserve metadata when copying
   - For huge files, confirm via checksum match before acting

6. **Report & follow-up**
   - Show total reclaimed space and remaining uncertain sets
   - Offer recurring checks and exclusion lists

## Quick Prompts
- “Scan Documents and Desktop for duplicates, but ignore Git repos.”
- “Keep files in /Projects as canonical; stage older copies for deletion.”
- “Find exact duplicates over 200MB and ask before touching them.”
