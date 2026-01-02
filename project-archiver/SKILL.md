---
name: project-archiver
description: Archives completed projects with consistent structure, metadata, and lightweight checksums so you can retrieve work quickly and reclaim space.
---

# Project Archiver

Convert finished projects into tidy, searchable archives.

## When to Use
- Wrapping up a client engagement or side project
- Preparing to hand off or share a project snapshot
- Need to free disk space while preserving retrievability

## Inputs to Gather
- Project root paths
- Completion date and status
- Must-keep artifacts (deliverables, contracts, assets)
- Exclusions (node_modules, build outputs, virtualenvs)
- Archive destination and naming convention

## What This Skill Does
1. Scans project directories for size, file types, and generated artifacts
2. Separates source, assets, and outputs
3. Applies consistent archive naming (e.g., `YYYY-MM-Project-Name.zip`)
4. Generates manifest with checksums and key metadata
5. Moves archives to long-term storage and frees workspace

## Instructions
1. Confirm project list, exclusions, and archive destination.
2. Collect stats: `du -sh`, file type counts, and largest items.
3. Build an archive plan highlighting what stays, what compresses, and what deletes.
4. Remove bulky generated folders (with consent), then package the rest.
5. Create `MANIFEST.md` including paths, sizes, mtimes, and checksum table.
6. Store archives in destination and leave a `ARCHIVED-AT` note in original location pointing to the new path.
7. Provide retrieval and verification commands.

## Safety
- Never archive credentials, secrets, or environment files without redaction.
- Keep original permissions and timestamps in the archive.
- Offer dry-run listing before compression.

## Example Prompt
"Archive the projects in ~/Projects/2024-Q2. Exclude node_modules and build directories, zip each project with a manifest, and move them to ~/Archives/Projects." 
