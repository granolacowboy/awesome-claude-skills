---
name: backup-prep
description: Prepares folders for backup by cleaning clutter, excluding noise, and producing a predictable manifest for verification.
---

# Backup Prep

Prepare clean, lightweight folders before backups so transfers are faster and restores are predictable.

## When to Use
- Before cloud syncs, Time Machine runs, or rsync jobs
- Need to slim large directories to fit storage limits
- Want a manifest for post-backup verification

## Outcomes
- Exclusion list for caches, build artifacts, and temp files
- Trimmed folder ready for backup
- Manifest with sizes and checksums for spot checks

## Workflow
1. **Define scope & exclusions**
   - Defaults: skip `node_modules`, `.venv`, `build/`, `dist/`, `.git`, caches
   - Ask about large binaries/datasets to keep or relocate

2. **Estimate size**
   ```bash
   du -sh [target]
   du -sh [target]/* | sort -rh | head -20
   ```

3. **Clean noise**
   - With approval, remove or move to `_BackupExcludes`
   - For repos, keep lockfiles and configs, drop build outputs
   - Keep log of removed paths in `backup-prep-log.tsv`

4. **Create manifest**
   ```bash
   find [target] -type f -size -2G -print0 | xargs -0 sha256sum > backup-manifest.sha
   ```
   - For huge files, record size + mtime instead of hashing

5. **Prepare backup command**
   - Provide ready-to-run `rsync` or `tar` command with exclusions
   - Include dry-run flag for validation

6. **Verify post-backup (optional)**
   - Spot-check manifest hashes at destination
   - Report mismatches and skipped files

## Quick Prompts
- “Prep ~/Projects for backup—exclude node_modules and build folders, generate manifest.”
- “Trim this directory under 50GB by moving big artifacts to _BackupExcludes.”
- “Give me an rsync command with --dry-run first.”
