---
name: backup-ready-bundler
description: Prepares folders for backup by flattening clutter, excluding noise, and producing manifest files so backups are lean, verifiable, and organized.
---

# Backup-Ready Bundler

Get directories backup-ready with clear manifests and excluded noise.

## When to Use
- Before running cloud or external-drive backups
- Cleaning up sync targets (iCloud/Dropbox/Drive) to save quota
- Need manifests to verify backup integrity later

## Inputs to Gather
- Source directories and backup destination
- Exclusion patterns (build outputs, caches, node_modules, .DS_Store)
- Desired manifest format (markdown, JSON, CSV)
- Compression preference and split size if needed

## What This Skill Does
1. Scans sources and highlights bulky noise to exclude
2. Creates standardized `backup-manifest` with sizes, counts, and checksums
3. Optionally compresses cleaned directories into chunks for transport
4. Provides verification commands for restore testing

## Instructions
1. Confirm sources, exclusions, and destination.
2. Run inventory: `du -sh`, file type counts, and largest offenders.
3. Draft exclusion list and manifest template; seek approval.
4. Apply exclusions, then generate manifest with checksums for key assets.
5. Package content if requested; place manifest alongside archives.
6. Share backup + restore verification commands and schedule tips.

## Safety
- Never delete originals; only exclude from backup packaging.
- Handle sparse disk images and VMs cautiously—ask before including or skipping.
- Stop if encountering encrypted vaults; require explicit direction.

## Example Prompt
"Prep ~/Work for backup. Exclude node_modules and .cache folders, create a markdown manifest with sizes and sha256 hashes, then tar.gz the cleaned folder to ~/Backups/Work-Backup." 
