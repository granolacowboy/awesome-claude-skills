---
name: folder-template-builder
description: Builds reusable folder templates for recurring work, complete with README guidance, checklists, and default subfolders.
---

# Folder Template Builder

Standardize recurring projects with reusable folder blueprints that keep every engagement organized from day one.

## When to Use
- Every new project starts from scratch with inconsistent structure
- Teams need a consistent home for briefs, assets, and deliverables
- Want to reduce setup time and onboarding questions

## Outcomes
- Template directories stored centrally (e.g., `~/Templates/Project`) 
- README with usage instructions and naming rules
- Optional setup script to instantiate a new project quickly

## Workflow
1. **Gather requirements**
   - Project types (client, internal, research, content)
   - Must-have folders (Briefs, Assets, Working, Archive, Hand-off)
   - Naming convention for new instances

2. **Design the template**
   - Sketch target tree in Markdown for approval
   - Include `_DoNotCommit`, `_ToReview`, or `_Intake` as needed

3. **Create template structure**
   ```bash
   TEMPLATE_ROOT="[root]/Templates/Project"
   mkdir -p "$TEMPLATE_ROOT"/{Briefs,Assets,Working,Deliverables,Archive}
   printf "# How to use this template\n\n- Place raw assets in Assets/\n- Keep WIP in Working/\n- Final outputs go to Deliverables/\n" > "$TEMPLATE_ROOT/README.md"
   ```

4. **Optional automation**
   - Provide a shell snippet to instantiate: `cp -R "$TEMPLATE_ROOT" "Projects/<Name>"`
   - Add token placeholders (e.g., `{{PROJECT_NAME}}`, `{{CLIENT}}`) for quick replace

5. **Publish rules**
   - Document naming pattern for new projects
   - Add a checklist for first-setup tasks and hand-off steps
   - Version the template with a CHANGELOG entry

6. **Rollout guidance**
   - Suggest storing templates in a shared, read-only location
   - Encourage PR/review for template updates

## Quick Prompts
- “Create a default client project template with Briefs, Assets, Working, Deliverables, Archive.”
- “Add a README that explains where to put drafts vs. finals.”
- “Give me a shell command to clone the template into Projects/new-site.”
