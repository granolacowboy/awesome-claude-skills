---
name: downloads-declutterer
description: Rapidly cleans and organizes a messy Downloads folder by categorizing files, archiving old items, and separating installers from documents without losing anything important.
---

# Downloads Declutterer

Keep your Downloads folder tidy with fast triage, smart categorization, and safe archiving so you never hunt for a file again.

## When to Use
- Downloads folder is overflowing or unsorted
- Need a clean slate before backing up or sharing the machine
- Want to separate installers, media, docs, and archives automatically
- Preparing a new workstation and want a tidy baseline

## Inputs to Gather
- Target directory (default: ~/Downloads)
- Cutoff dates for archiving (e.g., older than 90 days)
- File types to preserve in place (e.g., work-in-progress)
- Aggressiveness level: conservative, standard, aggressive

## What This Skill Does
1. Surveys the Downloads folder for volume, types, and recency
2. Groups files by type (docs, images, videos, audio, archives, installers)
3. Separates installers and disk images to their own stash
4. Archives stale files by age while preserving recent items
5. Flags suspicious or sensitive items for manual review

## Instructions
1. Confirm scope and preferences (age thresholds, exclusions, aggressiveness).
2. Collect stats:
   - `du -sh ~/Downloads/* | sort -rh | head -50`
   - `find ~/Downloads -type f -maxdepth 2 | sed 's/.*\.//' | sort | uniq -c | sort -rn`
   - `find ~/Downloads -type f -mtime +[days]`
3. Propose a tidy layout:
   - `Documents/`, `Images/`, `Audio/`, `Video/`, `Archives/`, `Installers/`, `To-Review/`, `Recent/`
4. Present a plan including moves, archives, and items needing confirmation.
5. After approval, run moves with logging and collision-safe renaming (preserve timestamps, never delete without consent).
6. Summarize results with counts, total space reclaimed, and quick follow-up commands for future upkeep.

## Safety
- Never delete by default—archive instead.
- Ask before moving anything newer than the chosen recency window.
- Stop and re-confirm if encryption/keys/passwords are detected.

## Example Prompt
"Declutter my Downloads folder. Archive anything older than 60 days, keep installers separate, and put documents in Documents/Downloads-Sorted/Docs."
