---
name: media-librarian
description: Organizes photos and videos by date and quality, creates human-readable folders, and flags blurry or oversized media for review.
---

# Media Librarian

Bring order to sprawling photo and video collections with date-based folders, quality triage, and duplicate awareness.

## When to Use
- Camera roll exports are scattered across disks
- Mixed RAW/JPG/HEIC/MP4 files lack structure
- You need quick wins before syncing or backing up

## Outcomes
- `Photos/YYYY/MM` and `Videos/YYYY/MM` folders
- Optionally separate RAW vs. edited exports
- Report of potential duplicates and low-quality items

## Workflow
1. **Collect sources**
   - Targets: SD card mounts, `~/Pictures`, external drives
   - Exclude already-synced libraries if requested
   - Ask whether to keep RAW and edited files together or split

2. **Extract dates**
   - Prefer EXIF `DateTimeOriginal`; fall back to file mtime
   - Flag files missing date metadata for manual assignment

3. **Build structure**
   ```bash
   mkdir -p "Photos" "Videos"
   mkdir -p "Photos/2025/01" "Videos/2025/01"  # created per item
   ```

4. **Route files**
   - Images → `Photos/YYYY/MM/`
   - Videos → `Videos/YYYY/MM/`
   - RAW/large formats (`.CR3`, `.NEF`, `.ARW`) → `Photos/YYYY/MM/RAW/`
   - Edited exports (`-edit`, `_final`) → `Photos/YYYY/MM/Edited/`
   - Keep a move log with original paths

5. **Quality triage**
   - Identify blurry/low-res candidates using dimensions when available
   - Flag duplicates by hash before moving; stage uncertain ones in `_ToReview`
   - Skip files over user-defined size unless approved

6. **Summarize**
   - Counts by month, size moved, duplicates found
   - Suggested next actions (dedupe review, album curation)

## Quick Prompts
- “Sort all camera exports into Photos/YYYY/MM and flag duplicates.”
- “Keep RAW in a separate RAW folder, but place edits beside their originals.”
- “Skip files over 2GB and leave them in _ToReview.”
