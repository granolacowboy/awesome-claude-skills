---
name: temporary-file-sweeper
description: Cleans caches, temp files, and build artifacts safely by scoping paths, previewing deletions, and leaving a reset script for repeat use.
---

# Temporary File Sweeper

A cautious cleanup routine for reclaiming space from temp files without breaking active work.

## When to Use This Skill

- Storage is being eaten by caches or build artifacts
- You want to clean working directories before archiving
- CI artifacts or IDE caches clutter repositories
- You need a reusable, parameterized cleanup script

## What This Skill Does

1. **Scopes cleanup** to safe directories (tmp, cache, build outputs)
2. **Previews deletions** with size summaries before removal
3. **Targets common clutter**: `.DS_Store`, `node_modules`, `.pytest_cache`, `dist/`, `*.tmp`, `*.log` (configurable)
4. **Creates a reusable script** (`cleanup.sh`) with toggles for dry-run vs delete
5. **Logs what was removed** for accountability

## How to Use

Navigate to the workspace root:
```bash
cd ~/Projects/my-app
```
Then ask Claude Code:
```bash
Identify temp/build clutter here, show me the space I can save, and generate a cleanup script.
```

## Instructions

1. Discover size hotspots:
   ```bash
   du -sh .
   du -sh node_modules dist build .pytest_cache .venv 2>/dev/null | sort -rh
   find . -maxdepth 3 -type f -name '*.log' -o -name '*.tmp' | head
   ```
2. Present a cleanup plan with categories: caches, build outputs, logs, temp files. Mark anything risky (e.g., production uploads) as exclude-by-default.
3. Build `cleanup.sh` with flags:
   ```bash
   #!/usr/bin/env bash
   set -euo pipefail
   DRY_RUN=${DRY_RUN:-1}
   delete() { if [ "$DRY_RUN" -eq 1 ]; then echo "DRY: rm -rf $1"; else rm -rf "$1"; fi }
   delete node_modules
   delete dist
   delete .pytest_cache
   ```
4. Keep a deletion log:
   ```bash
   echo "$(date -Iseconds),removed,$path" >> cleanup-log.csv
   ```
5. Run dry-run first; only perform deletions after user confirms. Skip `.git/`, `.env`, secrets, and anything explicitly excluded.
6. Suggest adding the script to CI or a cron job with DRY_RUN=1 for visibility before enabling deletions.

## Safety and Defaults

- Default to dry-run; never delete without consent
- Exclude VCS, environment files, and user-specified paths
- Warn before removing large directories (>1 GB)
- Preserve permissions and ownership on remaining files
