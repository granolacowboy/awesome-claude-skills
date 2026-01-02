---
name: shared-drive-tidier
description: Brings order to shared network/cloud drives with clear ownership, access-safe moves, and playbooks for permissions, naming, and team-wide folder standards.
---

# Shared Drive Tidier

A collaboration-safe approach to cleaning shared drives without breaking links or permissions.

## When to Use This Skill

- Team shares a chaotic Google Drive, OneDrive, or SMB share
- Ownership is unclear and links frequently break
- You need a migration plan that keeps stakeholders informed
- You want standard folder conventions enforced consistently

## What This Skill Does

1. **Inventories shared content** with size, owner (if available), and last-modified signals
2. **Builds a taxonomy** (Team/Projects/Archive/Reference/Intake) with agreed naming rules
3. **Identifies risky items** (linked docs, shared folders, unknown owners) for manual review
4. **Stages moves** with a dry-run plan and communication template
5. **Creates onboarding docs** (README in each major folder + naming rules)

## How to Use

Define the mount or sync location first:
```bash
cd /mnt/shared-drive  # or synced path
```
Then ask Claude Code:
```bash
Create a safe cleanup and migration plan for this shared drive, including dry-run move commands and a comms note.
```

## Instructions

1. Inventory and hotspots:
   ```bash
   du -sh * | sort -rh | head -30
   find . -maxdepth 3 -type f -printf '%TY-%Tm-%Td %p\n' | sort | head -5  # oldest
   ```
2. Draft taxonomy and naming rules (get stakeholder approval):
   ```
   Shared/
   ├── Team/
   ├── Projects/
   ├── Reference/
   ├── Archive/
   └── Intake/
   ```
   - Names: `YYYY-Project-Name`, `Client - Project - Artifact`
3. Produce a dry-run move plan (`mv` commands commented out) and a CSV log with `source,target,owner,last_modified`.
4. Share a communication template for the team describing what will move and when.
5. Execute moves in phases after approval; avoid deleting, prefer Archive/ for stale content.
6. Drop README and RULES.md files in top-level folders summarizing conventions and support contacts.

## Safety and Defaults

- Never change permissions without explicit direction
- Avoid moving files actively edited (recently modified within 48 hours)
- Keep linkable documents' paths stable or provide redirect files/shortcuts
- Maintain a full audit log for reversibility
