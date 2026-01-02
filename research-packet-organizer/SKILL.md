---
name: research-packet-organizer
description: Consolidates scattered research files into tidy packets with sources, notes, and citations aligned for fast review or sharing.
---

# Research Packet Organizer

Bundle research materials into coherent, labeled packets.

## When to Use
- Notes, PDFs, and screenshots are spread across folders
- Need to prepare a research handoff or briefing package
- Want consistent citation and source tracking for documents

## Inputs to Gather
- Target research topic or project name
- Source directories containing notes, PDFs, images
- Preferred packet structure (e.g., `Sources/`, `Notes/`, `Summaries/`, `Assets/`)
- Citation or metadata format (APA, MLA, link list)

## What This Skill Does
1. Collects all relevant files into a unified packet folder
2. Normalizes names and adds topic/date prefixes
3. Generates a `SOURCES.md` with links, metadata, and citation-ready snippets
4. Creates a `SUMMARY.md` skeleton for the user to fill or for Claude to draft
5. Produces a change log and next-step checklist

## Instructions
1. Confirm topic, scope, and desired structure.
2. Locate candidate files via keyword searches (filenames and optionally contents if allowed).
3. Propose a packet layout and naming scheme in markdown for approval.
4. Move/copy files into the structure, keeping originals safe unless asked to move.
5. Generate `SOURCES.md` and `SUMMARY.md` placeholders, linking to each asset.
6. Summarize what was consolidated and what remains to be gathered.

## Safety
- Default to copying, not moving, when consolidating across devices.
- Avoid altering source content; only organize references.
- Respect privacy-sensitive folders; require explicit consent before scanning.

## Example Prompt
"Create a research packet for 'battery recycling market'. Pull PDFs and notes from ~/Downloads and ~/Notes, copy them into ~/Research/Battery-Recycling, add SOURCES.md with links, and draft a SUMMARY.md outline." 
