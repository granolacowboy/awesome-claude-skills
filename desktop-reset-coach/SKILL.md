---
name: desktop-reset-coach
description: Cleans and stabilizes chaotic Desktops by triaging files into clear buckets, creating quick-access links, and leaving a maintenance routine to keep it tidy.
---

# Desktop Reset Coach

A fast, low-risk workflow to clear visual clutter from your Desktop while preserving quick access to the things you actually use.

## When to Use This Skill

- Desktop is overflowing with screenshots, zips, and temporary docs
- You need a clean Desktop before a presentation or recording
- You want a sustainable routine (weekly or daily) to keep it clear

## What This Skill Does

1. **Inventories Desktop items** and highlights large or old files
2. **Proposes triage buckets**: `Inbox/`, `To-File/`, `Current/`, `Archive/`, `Screenshots/`
3. **Creates shortcuts/aliases** to active projects instead of storing copies
4. **Moves files safely** after approval with an undo log
5. **Shares a maintenance checklist** and optional cron snippet

## How to Use

From your Desktop directory:
```bash
cd ~/Desktop
```
Then ask Claude Code:
```bash
Clear this Desktop with buckets and shortcuts—no deletions without asking.
```

## Instructions

1. Quick snapshot:
   ```bash
   ls -la
   du -sh * | sort -rh | head -20
   find . -maxdepth 1 -type f -mtime +14 -print
   ```
2. Present a plan with counts per bucket and any risky items (executables, very old files).
3. Create buckets:
   ```bash
   mkdir -p Inbox To-File Current Archive Screenshots
   ```
4. Moves after approval:
   - Screenshots → Screenshots/
   - Unknown items → Inbox/ for later review
   - In-use docs → Current/
   - Old items → Archive/
5. Replace heavy project copies with aliases/shortcuts (use `ln -s` on Unix) pointing to canonical locations.
6. Produce an undo log and a maintenance reminder:
   ```bash
   0 18 * * FRI /usr/bin/env bash -lc 'cd ~/Desktop && find . -maxdepth 1 -type f -mtime +7 -exec mv -t Archive {} +' 
   ```

## Safety and Defaults

- Never delete; archive first
- Preserve permissions and timestamps where possible
- Skip OS/system-created Desktop items (e.g., `.DS_Store`)
- Ask before moving application installers currently in use
