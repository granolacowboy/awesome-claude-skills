---
name: photo-library-organizer
description: Normalizes scattered photo libraries by sorting into year/month folders, detecting duplicates, and preserving EXIF metadata while keeping an archive-first safety net.
---

# Photo Library Organizer

A reliable way to structure photos by date, remove duplicates, and keep originals safe.

## When to Use This Skill

- Photos live across Desktop, Downloads, phones, and external drives
- You want a clean year/month hierarchy without losing EXIF data
- You need duplicates surfaced before syncing to cloud storage
- You are migrating to a new photo library or NAS

## What This Skill Does

1. **Reads EXIF dates** (fallback to modification time) to sort into `YYYY/MM - Month` folders
2. **Detects duplicates** via hash + name patterns before moving
3. **Handles RAW + JPG pairs** intelligently (keeps both, pairs them)
4. **Creates an Archive/Unsorted area** for uncertain files
5. **Generates a migration report** (counts per year, dup sets, missing EXIF)

## How to Use

Choose a staging directory (recommended: external drive or dedicated Photos-Staging):
```bash
cd ~/Photos-Staging
```
Then ask Claude Code:
```bash
Organize all photos here into year/month folders, show duplicates, and keep an undo log.
```

## Instructions

1. Inventory before moving:
   ```bash
   find . -type f | wc -l
   du -sh .
   ```
2. Pull EXIF capture dates where possible:
   ```bash
   exiftool -d '%Y-%m' -DateTimeOriginal -FileModifyDate -FileName . | head
   ```
   - Use DateTimeOriginal first, fall back to FileModifyDate if missing
3. Propose target structure:
   ```
   Photos/
   ├── 2024/
   │   ├── 01-January/
   │   ├── 02-February/
   │   └── ...
   ├── 2023/
   └── Unsorted/
   ```
4. Detect duplicates before moves:
   ```bash
   find . -type f -iname '*.jpg' -o -iname '*.jpeg' -o -iname '*.png' -o -iname '*.heic' -o -iname '*.arw' | \
   while read f; do md5sum "$f"; done | sort > /tmp/photo-hashes.txt
   ```
   - Group identical hashes; present locations and keep recommendations
5. Move with safety:
   - Create destination directories with `mkdir -p`
   - Move with `mv` after approval; keep originals in Archive/ if unsure
   - Maintain a CSV log: `source, destination, action`
6. Post-run report:
   - Counts per year/month
   - Number of duplicates quarantined
   - Files missing EXIF (kept in Unsorted)

## Safety and Defaults

- Never strip EXIF; use `mv` not `cp` unless user requests copies
- Avoid touching cloud-synced originals until staging is validated
- Preserve RAW+JPG pairs together
- Keep a separate `Archive/Unsorted` for ambiguous files
