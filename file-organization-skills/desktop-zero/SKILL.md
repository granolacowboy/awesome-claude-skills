---
name: desktop-zero
description: Resets a cluttered desktop to zero files by staging items, routing them into the right home folders, and leaving a clean workspace.
---

# Desktop Zero

Turn a chaotic desktop into a clear workspace while preserving important files and providing an undo-friendly trail.

## When to Use
- Desktop is overloaded with screenshots, shortcuts, and random files
- You want a tidy desktop without losing track of items
- You need a repeatable routine before presentations or screen shares

## Outcomes
- Empty, screenshot-ready desktop
- Staged folders for items needing decisions
- Clear routing of work vs. personal files into permanent homes

## Workflow
1. **Clarify expectations**
   - Default target: `~/Desktop`
   - Ask which file types should stay (e.g., active docs, shortcuts)
   - Confirm destinations for work vs. personal files

2. **Create staging**
   ```bash
   cd "[desktop_path]"
   mkdir -p _ToReview _Work _Personal Screenshots Shortcuts
   ```

3. **Route by type**
   - Screenshots (`*.png`, timestamped filenames) → `Screenshots/`
   - Shortcuts/aliases (`*.lnk`, `.desktop`) → `Shortcuts/`
   - Documents for work vs. personal → `_Work/` or `_Personal/`
   - Unknown or mixed → `_ToReview/`
   - Keep count and log moves in `desktop-zero-log.tsv`

4. **Move to destinations**
   - Ask for destination roots (e.g., `~/Documents/Work`, `~/Documents/Personal`)
   - Move staged `_Work` and `_Personal` items into final homes
   - Leave `_ToReview` for explicit confirmation

5. **Safety rules**
   - Never delete by default; only move
   - Skip app bundles or packages unless approved
   - Keep icon arrangement intact by emptying root after staging

6. **Wrap-up**
   - Report what was moved where and remaining `_ToReview`
   - Offer to compress old screenshots or archive dated items
   - Suggest a weekly reminder cadence for Desktop Zero

## Quick Prompts
- “Clear my desktop now; send work files to Documents/Work and leave anything unclear in _ToReview.”
- “Archive screenshots older than 90 days and leave the rest organized.”
- “Move everything except .webloc shortcuts; keep a log for undo.”
