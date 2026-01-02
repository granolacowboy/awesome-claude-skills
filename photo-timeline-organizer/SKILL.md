---
name: photo-timeline-organizer
description: Sorts photos and videos into year/month/day timelines using EXIF data, file metadata, and sensible fallbacks while keeping originals safe.
---

# Photo Timeline Organizer

Bring order to photo libraries with consistent date-based folders and optional event groupings.

## When to Use
- Camera roll or imports are scattered across disks
- Need clean year/month folders for backups or sharing
- Mixed EXIF quality across devices causing messy ordering

## Inputs to Gather
- Source directories
- Destination root (e.g., `~/Photos/Chronological`)
- Whether to rename files with timestamps
- Handling rules for missing EXIF (use file mtime, prompt, or place in `Unsorted`)

## What This Skill Does
1. Reads EXIF capture times for images and videos
2. Normalizes timezones and handles missing metadata gracefully
3. Creates `YYYY/MM - Month` hierarchy (optionally day-level)
4. Renames files with `YYYYMMDD_HHMMSS` patterns if desired
5. Produces a summary of moved items and skipped edge cases

## Instructions
1. Confirm sources, destination, rename preference, and duplicate handling.
2. Audit sample EXIF data to detect timezone anomalies.
3. Draft target structure and collision rules.
4. Run organization in batches: move/copy to date folders, flag missing data to `Unsorted` with a report.
5. Offer optional de-duplication by checksum before finalizing.
6. Provide a final timeline summary and backup commands.

## Safety
- Default to copy instead of move for first run unless user approves moves.
- Preserve original metadata; avoid recompressing media.
- Avoid touching `.photoslibrary` or app-managed libraries unless explicitly allowed.

## Example Prompt
"Organize my camera roll in ~/Imports into ~/Photos/Chronological. Copy files, rename them with timestamps, and put anything missing EXIF into Unsorted for review." 
