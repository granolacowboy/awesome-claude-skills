---
name: project-archivist
description: Archives inactive projects into dated, well-labeled bundles with dependency notes, readme stubs, and storage-friendly compression.
---

# Project Archivist

Reduce clutter by moving inactive projects into structured archives while keeping them understandable and restorable.

## When to Use
- Projects are piling up in a single workspace
- You need space before backups or laptop swaps
- Old work needs clear status and restore instructions

## Outcomes
- `Archive/YYYY/ProjectName/` folders with README notes
- Optional compressed bundles for cold storage
- Clear separation of active vs. archived work

## Workflow
1. **Select candidates**
   - Identify projects untouched since a chosen date
   - Exclude active/experimental repos per user input
   - Detect heavy folders (e.g., `node_modules`, `.venv`, `build/`) for cleanup

2. **Prepare archive home**
   ```bash
   ARCHIVE_ROOT="[archive_root]/Archive/$(date +%Y)"
   mkdir -p "$ARCHIVE_ROOT"
   ```

3. **Document context**
   - For each project, create `ARCHIVE_ROOT/ProjectName/README-ARCHIVE.md` with:
     - Purpose, status, last commit/tag
     - How to restore/run, required tools, env vars
     - Why it was archived and known gaps

4. **Slim dependencies (optional)**
   - Remove `node_modules`, `.venv`, `build`, `.DS_Store` with consent
   - Capture lockfiles and `requirements.txt/package-lock.json` before removal

5. **Move & compress**
   ```bash
   rsync -a --exclude "node_modules" --exclude "*.log" \
     "[project_path]" "$ARCHIVE_ROOT/"
   tar -czf "${ARCHIVE_ROOT}/ProjectName.tgz" -C "$ARCHIVE_ROOT" "ProjectName"  # optional
   ```
   - Keep checksums and size notes in `archive-log.tsv`

6. **Update active area**
   - Remove/move original project folder after verification
   - Leave a shortcut or text stub indicating archive location

7. **Report**
   - Space reclaimed, projects archived, compression savings
   - Suggest quarterly archive sweeps

## Quick Prompts
- “Archive projects untouched since Jan 1 into ~/Archives/2025 and strip node_modules.”
- “Bundle inactive client projects with README-ARCHIVE context and tar them.”
- “Move archived repos off the main drive; leave stubs in ~/Projects.”
