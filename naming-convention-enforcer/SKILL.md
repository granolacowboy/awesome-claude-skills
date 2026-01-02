---
name: naming-convention-enforcer
description: Renames files and folders to consistent, human-readable conventions with preview and rollback support to eliminate chaotic naming.
---

# Naming Convention Enforcer

Normalize file names so everything is searchable and consistent.

## When to Use
- Mix of `final_v2 (1).pdf` and other messy names
- Migrating to a shared drive that needs consistent patterns
- Preparing assets for delivery or ingestion into a system

## Inputs to Gather
- Target directories
- Preferred naming template (e.g., `YYYY-MM-DD-topic.ext`)
- Words to strip (copy, final, draft, v2)
- Casing style (kebab-case, snake_case, Title Case)
- Dry-run vs. apply

## What This Skill Does
1. Inventories existing names and detects common patterns
2. Builds normalized names using chosen template and casing
3. Removes noise suffixes and collapses whitespace
4. Shows a before/after preview table for approval
5. Applies renames atomically with collision handling and rollback notes

## Instructions
1. Confirm template, casing, and excluded folders.
2. Analyze filenames and propose replacements; surface conflicts early.
3. Present markdown preview with diffs and ask for confirmation.
4. Apply renames using safe moves; record a `rename-log.txt` with old→new mappings.
5. Verify references (e.g., paired files .md/.png) stay aligned.
6. Share quick scripts to undo or propagate changes (e.g., git mv, symlinks).

## Safety
- Skip hidden/system files unless explicitly included.
- Avoid renaming within app bundles or package directories without consent.
- Abort if target names collide beyond safe resolution rules.

## Example Prompt
"Rename everything in ~/Documents/Proposals to kebab-case with dates, removing `(1)` and `final` suffixes. Show a preview before applying." 
