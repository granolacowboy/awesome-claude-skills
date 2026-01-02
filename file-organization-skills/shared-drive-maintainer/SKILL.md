---
name: shared-drive-maintainer
description: Cleans and standardizes team shared drives with clear folder rules, ownership notes, and safe handling of active collaboration areas.
---

# Shared Drive Maintainer

Restore sanity to team drives with clear structure, safe staging, and minimal disruption to collaborators.

## When to Use
- Shared drives have duplicate folders, misc uploads, or unclear ownership
- Need a non-destructive cleanup with communication built-in
- Want consistent rules for future file drops

## Outcomes
- Approved folder taxonomy for the team
- `_Staging` and `_ToReview` areas to avoid breaking links
- Ownership notes and change log for transparency

## Workflow
1. **Align on rules**
   - Confirm canonical roots (e.g., `Projects`, `Assets`, `Admin`)
   - Define do-not-touch areas (active sprints, legal, finance)
   - Decide on naming and versioning norms

2. **Map current state**
   ```bash
   find [drive_root] -maxdepth 3 -type d | sort > structure-before.txt
   ```
   - Identify duplicates by similar names
   - Spot orphan files at root and large loose assets

3. **Create staging**
   - `mkdir -p [drive_root]/_Staging/_ToReview`
   - Move ambiguous or duplicate copies into `_ToReview` (never delete)
   - Leave breadcrumbs (README) where moves occur

4. **Standardize folders**
   - Apply template: `Projects/<Client>/<Project>/{Briefs,Assets,Deliverables,Archive}`
   - `Admin/{Finance,HR,Legal}`, `Assets/{Brand,Stock,Templates}`
   - Normalize names to kebab-case or Title Case per team preference

5. **Handle duplicates safely**
   - Hash large files before moving
   - Keep the most complete folder as canonical; move extras into `_Staging`
   - Record rationale in `shared-drive-log.tsv`

6. **Communicate changes**
   - Produce summary with moved paths and new standards
   - Flag files needing owner confirmation
   - Suggest guardrails (upload checklist, new folder request form)

## Quick Prompts
- “Clean the shared drive but keep sprint folders untouched; stage duplicates.”
- “Apply the Projects/Client/Project template and move loose files to correct spots.”
- “Create a change log and owner questions list for the team.”
