---
name: project-archive-architect
description: Converts messy project directories into clear Active/Archive layouts with consistent naming, retention rules, and lightweight inventories for future retrieval.
---

# Project Archive Architect

A repeatable pattern for separating active work from historical projects while keeping everything discoverable.

## When to Use This Skill

- You have old projects mixed with current work
- You need to hand off projects with clear structure
- Storage quotas require archiving inactive work safely
- You want standardized naming and retention windows

## What This Skill Does

1. **Assesses recency** (last modified) to suggest Active vs Archive placement
2. **Creates a consistent scaffold** (`Active/`, `Archive/YYYY/`, `Templates/`)
3. **Renames folders** to a standard format (e.g., `yyyy-mm-client-name-project`)
4. **Generates a manifest** (project, path, last activity, notes)
5. **Compresses or moves** cold projects to Archive after approval

## How to Use

Navigate to your projects root:
```bash
cd ~/Projects
```
Then ask Claude Code:
```bash
Restructure this projects directory into Active and Archive, propose names, and create a manifest.
```

## Instructions

1. Inventory and recency:
   ```bash
   find . -maxdepth 2 -type d -mtime -1 | head
   find . -maxdepth 2 -type d -mtime +180
   ```
2. Propose scaffold (customize per user):
   ```
   Projects/
   ├── Active/
   ├── Archive/
   │   ├── 2024/
   │   └── 2023/
   └── Templates/
   ```
3. Build rename suggestions using the pattern `YYYY-MM-owner-project` or similar approved format. Show before/after table and request confirmation.
4. Generate manifest CSV:
   ```bash
   printf "name,last_modified,path,status\n" > manifest.csv
   find Active Archive -maxdepth 1 -mindepth 1 -type d -print0 | while IFS= read -r -d '' dir; do
     printf "%s,%s,%s,%s\n" "$(basename "$dir")" "$(stat -c '%y' "$dir" | cut -d' ' -f1)" "$dir" "$(dirname "$dir" | xargs basename)" >> manifest.csv
   done
   ```
5. Move/zip cold projects after approval:
   ```bash
   mkdir -p Archive/2023
   mv "OldProject" Archive/2023/
   # Or compress
   tar -czf Archive/2023/OldProject.tar.gz OldProject
   ```
6. Summarize changes and remind about retention rules (e.g., archive after 90 days idle).

## Safety and Defaults

- Never delete; archive to dated folders
- Skip VCS metadata changes; avoid altering `.git` contents unless asked
- Keep manifest and rename plan versioned for traceability
- Ask before compressing very large directories
