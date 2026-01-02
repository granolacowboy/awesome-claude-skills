---
name: archive-rotation-scheduler
description: Implements a retention playbook that auto-archives stale files on a schedule, keeping active areas lean while maintaining dated, searchable archives.
---

# Archive Rotation Scheduler

Keep active folders light by automatically moving stale files into dated archives with audit trails.

## When to Use This Skill

- You want rolling retention (e.g., archive after 90 days idle)
- Active folders slow down sync due to size
- Compliance or client contracts require dated archives
- You need predictable archive naming (year/month) and reports

## What This Skill Does

1. **Defines retention windows** per folder type (active, reference, temp)
2. **Creates archive destinations** by year/month with storage-friendly naming
3. **Builds scheduled jobs** (cron/Task Scheduler) for moves with logs
4. **Produces reports** of what was archived each run
5. **Supports dry-runs** before enabling automation

## How to Use

Select the active directory to keep lean:
```bash
cd ~/Projects/Active
```
Then ask Claude Code:
```bash
Set up a 90-day archive rotation here with cron commands and a dry-run first.
```

## Instructions

1. Confirm retention windows and exclusions (e.g., `.git`, `node_modules`, encrypted files).
2. Draft archive structure:
   ```
   Active/
   Archive/
     ├── 2024-01/
     ├── 2024-02/
     └── ...
   ```
3. Dry-run candidates:
   ```bash
   find . -maxdepth 2 -type f -mtime +90 -print > /tmp/archive-candidates.txt
   ```
4. Present move plan and get approval. Then implement with logging:
   ```bash
   mkdir -p Archive/$(date +%Y-%m)
   while IFS= read -r file; do
     mv "$file" "Archive/$(date +%Y-%m)/" && echo "$file,Archive/$(date +%Y-%m)/" >> archive-log.csv
   done < /tmp/archive-candidates.txt
   ```
5. Set up a cron entry (example):
   ```bash
   0 3 * * SUN /usr/bin/env bash -lc 'cd ~/Projects/Active && find . -maxdepth 2 -type f -mtime +90 -print0 | xargs -0 -I{} mv {} Archive/$(date +%Y-%m)/'
   ```
   - Include `-print` only mode for dry-runs on first execution.
6. Share a rollback note: move from Archive/* back to Active/ if needed.

## Safety and Defaults

- Never delete; only move to Archive
- Keep archive-log.csv for each run
- Skip files currently modified in last 24 hours (optional flag with `-mtime +90 ! -mtime -1`)
- Respect permissions and encrypted/secret files—ask before moving them
