---
name: naming-convention-enforcer
description: Audits and normalizes file and folder names to approved patterns, providing previews and safe rename scripts with rollback before applying changes.
---

# Naming Convention Enforcer

Standardize filenames so search, sorting, and automation work reliably.

## When to Use This Skill

- Files use inconsistent patterns (`final_v2`, spaces, mixed cases)
- You need timestamps and semantics embedded in names
- Teams struggle to understand what files mean at a glance
- You want a reversible rename script before touching anything

## What This Skill Does

1. **Audits current names** and highlights violations (spaces, uppercase, missing dates)
2. **Defines canonical patterns** per type (docs, images, invoices, projects)
3. **Generates preview tables** (current → proposed) before any rename
4. **Creates shell-safe rename scripts** with undo logs
5. **Adds README of conventions** for the directory root

## How to Use

Set the target directory:
```bash
cd ~/Documents/client-work
```
Then ask Claude Code:
```bash
Audit names here, propose standardized formats, and prepare a reversible rename script.
```

## Instructions

1. Collect names and spot issues:
   ```bash
   find . -type f -maxdepth 3 -printf '%P\n' | head -100
   ```
2. Work with the user to pick patterns, e.g.:
   - Documents: `YYYY-MM-DD - Title - Status.ext`
   - Images: `YYYYMMDD_HHMMSS_Camera.ext`
   - Projects: `client-project-scope`
3. Prepare a preview CSV:
   ```bash
   printf "current,proposed\n" > rename-preview.csv
   # Fill rows with proposed names
   ```
4. Generate a safe script using `mv` with backup and undo:
   ```bash
   mv "${old}" "${new}" && echo "${new},${old}" >> undo.log
   ```
   - Include safeguards for collisions and immutable files
5. Ask for confirmation, then run renames batch-by-batch. Skip anything uncertain and list it in a TODO.
6. Drop a `NAMING-RULES.md` in the directory documenting patterns and examples.

## Safety and Defaults

- Never overwrite existing files; handle collisions by appending suffixes after approval
- Keep undo.log to reverse renames easily
- Avoid touching VCS internals (`.git`, `.svn`)
- Ask before lowercasing names on case-sensitive file systems
