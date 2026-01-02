---
name: desktop-reset
description: Cleans and organizes a cluttered Desktop into structured folders, preserving active work while archiving old items for a clear workspace.
---

# Desktop Reset

Restore a calm, organized Desktop without losing ongoing work.

## When to Use
- Desktop is covered with files and screenshots
- Need a quick professional cleanup before screen sharing
- Want to separate active tasks from reference material

## Inputs to Gather
- What counts as "active" work to keep on Desktop
- Age threshold for archiving
- Destination root for organized files (e.g., Documents/Desktop-Sorted)
- Sensitive folders or file types to exclude

## What This Skill Does
1. Inventories Desktop contents by type and recency
2. Groups screenshots, documents, media, and archives
3. Leaves designated active items in place
4. Creates clean subfolders and moves items with clear naming
5. Archives stale items to a dated folder

## Instructions
1. Confirm active items and exclusions.
2. Generate quick stats: `find ~/Desktop -maxdepth 2 -type f -print` with counts by type and age buckets.
3. Propose structure: `Desktop-Sorted/{Active, Screenshots, Documents, Media, Archives, To-Review}`.
4. Present a move plan with counts and paths for approval.
5. Move files with collision-safe names; keep timestamps intact.
6. Provide before/after summary and shortcuts for maintaining cleanliness.

## Safety
- Never delete; only move/organize unless explicitly told.
- Avoid altering app shortcuts or system links unless approved.
- Ask before touching files changed today.

## Example Prompt
"Reset my Desktop. Keep anything modified in the last 7 days in Active, move screenshots to Screenshots/, and archive items older than 90 days." 
