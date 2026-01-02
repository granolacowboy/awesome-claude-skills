---
name: shared-drive-curator
description: Cleans and standardizes shared drives by applying folder conventions, ownership labels, and access-friendly layouts while protecting critical team content.
---

# Shared Drive Curator

Make team drives understandable with consistent structure, labels, and access-aware organization.

## When to Use
- Team shares have ad-hoc folders and duplicates
- Onboarding new teammates requires clearer layout
- Need to prep a shared drive for audits or migration

## Inputs to Gather
- Target shared drive path or mount
- Critical folders that must stay untouched
- Role-based sections (e.g., Product, Eng, Marketing)
- Archiving rules and retention timelines

## What This Skill Does
1. Maps current structure and finds orphaned or duplicated folders
2. Designs a role-friendly top-level layout with clear naming
3. Moves or archives stale content into date-stamped buckets
4. Applies ownership/labels where supported and documents conventions
5. Produces a change log and a quick-start guide for teammates

## Instructions
1. Confirm scope, protected areas, and retention policies.
2. Inventory:
   - Tree depth and largest folders (du -sh)
   - Duplicate or near-duplicate folder names
   - Files with no clear owner (use path cues)
3. Propose target structure and naming rules in markdown.
4. Present a move/archive plan with risks and rollback steps.
5. Execute approved changes carefully, keeping permissions intact.
6. Deliver a short `README_SHARED_DRIVE.md` summarizing layout and maintenance cadence.

## Safety
- Never alter permissions without explicit approval.
- Skip legal/finance folders unless owner confirms.
- Preserve shared links by moving within the same drive when possible.

## Example Prompt
"Organize the team drive at /mnt/shared. Keep Legal and HR folders untouched, archive items untouched for 12+ months, and create a README for the new layout." 
