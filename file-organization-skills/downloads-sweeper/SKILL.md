---
name: downloads-sweeper
description: Quickly declutters a messy Downloads folder by sorting files into staged buckets, archiving installers, and leaving a clean inbox for new items.
---

# Downloads Sweeper

Keep your Downloads folder lean by sweeping bulk files into sensible buckets, archiving installers, and leaving a clear inbox for new items.

## When to Use
- Downloads contains months of mixed files and installers
- You want a fast reset without touching other folders
- You need staging before deciding long-term destinations
- You want predictable buckets for routine sweeps

## What This Skill Delivers
- Clean “_Inbox” for the newest items
- Buckets for documents, images, media, archives, and installers
- Optional age-based archive (e.g., older than 60 days)
- A summary report with undo-friendly move logs

## Workflow
1. **Confirm scope**
   - Default target: `~/Downloads`
   - Ask for exclusions (VM images, large datasets, work-in-progress files)
   - Ask how aggressive to be (light, standard, deep)

2. **Prepare structure**
   ```bash
   cd "[downloads_path]"
   mkdir -p _Inbox _ToReview Documents Images Media Archives Installers
   ```

3. **Classify & move**
   - Documents: `pdf docx xlsx txt md` → `Documents/`
   - Images: `png jpg jpeg gif svg heic` → `Images/`
   - Media: `mp4 mov mkv mp3 wav` → `Media/`
   - Archives: `zip tar.gz rar 7z` → `Archives/`
   - Installers: `dmg pkg exe msi deb rpm` → `Installers/`
   - Unknown or recent (<48h): keep in `_Inbox`
   - Unclear items: `_ToReview/`
   - Log every move in `sweep-log.tsv` (`from<TAB>to`)

4. **Age-based archive (optional)**
   ```bash
   find . -maxdepth 1 -type f -mtime +60 -print0 | xargs -0 -I{} mv "{}" Archives/
   ```

5. **Safety checks**
   - Never delete by default; only move
   - Preserve timestamps (`mv -n` or `cp -p` then `rm`) if user requests
   - Skip files >2GB unless user approves

6. **Summarize & next steps**
   - Report counts per bucket and total size moved
   - Surface `_ToReview` items for user decisions
   - Suggest renaming or long-term destinations if asked

## Quick Prompts
- “Sweep my Downloads lightly—just bucket common types.”
- “Deep clean Downloads, archive installers older than 30 days, and leave a list of questionable files.”
- “Move anything bigger than 1GB into _ToReview and don’t touch it.”
