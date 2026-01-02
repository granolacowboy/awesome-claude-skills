---
name: duplicate-hunter
description: Detects and resolves duplicate files safely using hashes, metadata, and context-based recommendations with user-approved cleanup actions.
---

# Duplicate Hunter

Find and clean duplicate files without risking important data.

## When to Use
- Storage space is tight
- Multiple copies of the same documents or media exist
- Sync conflicts created filename suffixes ("(1)", "copy", etc.)
- Migrating between machines and want a single source of truth

## Inputs to Gather
- Target directories to scan
- Preferred keep rules (newest, highest-quality, canonical path)
- Folders to ignore (backups, archives)
- Action policy: delete duplicates, move to quarantine, or just report

## What This Skill Does
1. Computes hashes for exact matches and sizes for near-duplicates
2. Groups candidates by filename patterns and modification time
3. Detects derivative suffixes (copy, final, v2, (1))
4. Produces a reviewable report with recommendations
5. Executes user-approved cleanup (delete/move/quarantine)

## Instructions
1. Clarify scope, keep rules, and handling of archives.
2. Run discovery:
   - `find [paths] -type f -exec md5sum {} \; | sort`
   - `find [paths] -type f -printf '%s %p\n' | sort -n`
   - Flag names with patterns: `(1)`, `copy`, `final`, `backup`.
3. Build a markdown report listing each duplicate set with size, mtime, and recommended keeper.
4. Ask for confirmation per set or batch.
5. Execute chosen actions with logging; never delete without explicit consent.
6. Provide undo guidance (move duplicates to a quarantine folder before deletion if unsure).

## Safety
- Skip system and hidden directories unless explicitly allowed.
- Avoid deleting items inside time-machine/backup snapshots.
- Stop if large binary blobs appear critical (VMs, DBs) and ask before touching.

## Example Prompt
"Find duplicates in ~/Documents and ~/Desktop. Keep the newest version, move duplicates to ~/Quarantine/Duplicates, and show a summary before doing anything." 
