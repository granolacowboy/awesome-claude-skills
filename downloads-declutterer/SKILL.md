---
name: downloads-declutterer
description: Rapidly triages messy Downloads folders by grouping by type, date, and source, proposing a clean structure, and moving files safely with confirmations.
---

# Downloads Declutterer

A focused workflow for turning an overloaded Downloads folder into a clean staging area in minutes while preserving anything important.

## When to Use This Skill

- Downloads is full of installers, screenshots, and random attachments
- You need a quick cleanup before a meeting or travel
- You're preparing a new machine and want a fresh start
- You want an automated weekly routine to keep Downloads tidy

## What This Skill Does

1. **Scans and categorizes** common file types (archives, installers, docs, media, screenshots)
2. **Groups by recency** (today, last 7 days, older) to highlight what matters now
3. **Proposes a clean structure** (Active/, To-Review/, Installers/, Archives/, Temp/)
4. **Surfaces large or suspicious files** before any moves
5. **Moves safely with confirmation** and keeps an undo log
6. **Schedules recurring cleanups** with cron-ready commands

## How to Use

From your home directory:
```bash
cd ~/Downloads
```
Then ask Claude Code:
```bash
Declutter this Downloads folder, show me the plan, and only move files after I approve.
```

## Instructions

1. Get quick stats before proposing changes:
   ```bash
   du -sh . && find . -type f | wc -l
   du -sh * | sort -rh | head -20
   ```
2. Identify patterns and recency buckets:
   - Today, last 7 days, last 30 days, older
   - Installers (.dmg, .pkg, .exe), archives (.zip, .tar.*), media, docs, screenshots
3. Draft a plan first. Default structure:
   ```
   Downloads/
   ├── Active/
   ├── To-Review/
   ├── Installers/
   ├── Archives/
   ├── Screenshots/
   └── Temp/
   ```
4. Present moves in a checklist and request approval. Include largest files and anything older than 90 days as archive candidates.
5. Execute with logging:
   ```bash
   mkdir -p Active To-Review Installers Archives Screenshots Temp
   mv "${file}" Installers/  # example after approval
   ```
6. Keep an undo log (source → destination). If unsure about a file, leave it in To-Review/ and flag it.
7. Offer a recurring maintenance snippet:
   ```bash
   0 9 * * MON /usr/bin/env bash -lc 'cd ~/Downloads && find . -type f -mtime +14 -exec mv -t Archives {} +'  # adjust for OS
   ```

## Safety and Defaults

- Never delete anything; archive instead
- Preserve timestamps when possible (`cp -p` then remove originals if needed)
- Stop and ask if permissions or special files are detected
- Keep installers for 30 days before archiving
