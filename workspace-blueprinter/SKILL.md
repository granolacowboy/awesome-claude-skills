---
name: workspace-blueprinter
description: Designs and scaffolds clean folder layouts for new or existing workspaces with reusable templates, README guides, and automation hooks for consistent organization.
---

# Workspace Blueprinter

A starter kit for defining and enforcing a clear directory blueprint for any team or project.

## When to Use This Skill

- Kicking off a new team workspace or repository mirror
- Standardizing how new projects are structured
- Migrating from ad-hoc folders to a consistent hierarchy
- Preparing a sandbox with scripts and READMEs baked in

## What This Skill Does

1. **Interviews for requirements** (team, data types, compliance needs)
2. **Proposes a tailored blueprint** with directories, ownership notes, and README stubs
3. **Generates scaffolding** with `mkdir -p` and placeholder files
4. **Adds automation hooks** (scripts for cleanup, backups, linting) when relevant
5. **Produces a quickstart guide** explaining what goes where

## How to Use

Pick a target path:
```bash
cd ~/Workspace
```
Then ask Claude Code:
```bash
Create a standardized workspace skeleton with READMEs and scripts for this team.
```

## Instructions

1. Gather essentials: team size, data sensitivity, programming languages, retention rules.
2. Draft a blueprint similar to:
   ```
   Workspace/
   ├── docs/
   ├── data/
   ├── projects/
   ├── sandbox/
   ├── archive/
   └── scripts/
   ```
3. Create directories and README placeholders describing purpose and rules for each.
4. Add helpful boilerplate:
   - `.gitkeep` where empty folders are needed
   - `scripts/cleanup.sh` skeleton for routine tidying
   - `docs/conventions.md` summarizing naming and storage rules
5. Present commands for review before execution, then apply with logging.
6. Deliver a quickstart summary and optional cron/automation snippets.

## Safety and Defaults

- Avoid overwriting existing files; propose merges instead
- Keep automation opt-in; never enable destructive scripts by default
- Respect permissions—flag restricted paths for admin review
