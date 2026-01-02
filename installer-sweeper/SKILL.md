---
name: installer-sweeper
description: Finds and handles leftover installers, disk images, and packages, freeing space while keeping a minimal stash for future reinstalls.
---

# Installer Sweeper

Clear out leftover installers and disk images without losing what you might still need.

## When to Use
- Downloads folder is full of `.dmg`, `.pkg`, `.exe`, `.zip` installers
- Preparing a machine for backup or handoff
- Running low on disk space due to cached installers

## Inputs to Gather
- Paths to scan (default: Downloads, Desktop, temp folders)
- Minimum age before removal
- Whether to keep the latest version per app
- Destination for a curated installer cache

## What This Skill Does
1. Detects installer file types and large archives
2. Groups by application/vendor name and version when possible
3. Recommends keeping the newest copy and archiving or deleting the rest
4. Optionally builds a small installer cache directory
5. Reports reclaimed space estimates

## Instructions
1. Confirm scan paths, age thresholds, and cache destination.
2. Identify installers: `find [paths] -type f \( -iname '*.dmg' -o -iname '*.pkg' -o -iname '*.exe' -o -iname '*.msi' -o -iname '*.zip' \)`.
3. Group results by app/version using filename tokens; surface duplicates.
4. Share a plan: keep list vs. archive vs. delete, with sizes.
5. Execute approved moves/deletions; keep a log for undo.
6. Provide follow-up commands to keep the cache tidy.

## Safety
- Default to moving installers to a cache instead of deleting.
- Ask before deleting anything modified in the last 30 days.
- Avoid touching compressed project backups mislabeled as installers unless confirmed.

## Example Prompt
"Sweep installers from Downloads and Desktop. Keep the latest version of each app in ~/Installer-Cache and delete anything older than 6 months after confirmation." 
