---
name: duplicate-file-hunter
description: Finds duplicate and near-duplicate files safely by hashing, size clustering, and metadata review, then guides you through keeping the best copy with clear evidence and undo logs.
---

# Duplicate File Hunter

A cautious workflow for eliminating redundant files without accidental loss.

## When to Use This Skill

- Storage is tight and you suspect duplicates across drives
- Photos, PDFs, or installers appear multiple times in different folders
- You need an auditable, reversible deduplication process
- You want to standardize a "keep the best copy" rule

## What This Skill Does

1. **Discovers duplicates** with a tiered approach: name matches → size matches → hash matches
2. **Surfaces near-duplicates** (same size ±1%, same name with copies) for manual review
3. **Shows evidence** (paths, sizes, modified dates) before any action
4. **Suggests keep rules** (newest, highest-quality path, canonical folder) with rationale
5. **Executes moves or deletions** only after explicit approval, keeping a restore log

## How to Use

Pick a root directory:
```bash
cd ~/Documents
```
Then ask Claude Code:
```bash
Find duplicates here, recommend which to keep, and prepare commands I can review before running.
```

## Instructions

1. Build evidence sets:
   ```bash
   find . -type f -printf '%s %p\n' | sort -n > /tmp/size-list.txt
   # Exact duplicates
   awk '{print $1}' /tmp/size-list.txt | uniq -d | while read size; do grep "^${size} " /tmp/size-list.txt; done > /tmp/same-size.txt
   # Hash the candidates
   awk '{print $2}' /tmp/same-size.txt | xargs -I{} sh -c 'md5sum "$1"' _ {} | sort > /tmp/hash-list.txt
   ```
2. Group by hash and present sets with:
   - File paths
   - Size and modified time (`stat -c "%y %s"`)
   - Suggested keeper and reason
3. Ask for per-set confirmation: delete extras, move to Archive/Duplicates/, or skip.
4. Apply decisions with reversible steps:
   ```bash
   mkdir -p Archive/Duplicates
   mv "${file}" Archive/Duplicates/
   # Only `rm` after user confirms archive review
   ```
5. Produce an undo/decision log (`source → action → destination`).

## Safety and Defaults

- Never delete without explicit approval; prefer moving to Archive/Duplicates first
- Avoid hashing enormous files until user confirms; show size summary first
- Skip system/hidden folders unless user opts in
- Preserve one copy in the canonical location the user approves
