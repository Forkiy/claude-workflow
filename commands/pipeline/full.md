---
description: "Execute complete software implementation pipeline from PRD to implementation"
allowed-tools: ["Read", "Write", "Glob", "Task", "Bash"]
argument-hint: "<project-idea> [optional: output-folder]"
---

# Full Software Implementation Pipeline

You are about to execute the complete software implementation pipeline, taking a project from initial idea through to implementation.

## Pipeline Overview

This command orchestrates the entire document generation and implementation pipeline:
1. **PRD Creation** - Generate Product Requirements Document
2. **Domain Modeling** - Extract domain model from PRD
3. **C4 Architecture** - Create architecture diagrams
4. **Design Document** - Generate comprehensive design doc
5. **Roadmap Creation** - Develop implementation roadmap with epics
6. **Implementation** - Begin feature development

## Arguments

Parse the arguments from: `$ARGUMENTS`

Expected format:
- First argument: Project idea or description (required)
- Second argument: Output folder path (optional, defaults to `docs/pipeline-output`)

## Execution Steps

1. **Parse Arguments**
   - Extract project idea from first argument
   - Determine output folder (use second argument or default)
   - Create output folder structure if it doesn't exist

2. **Create Output Structure**
   ```
   output-folder/
   ├── 01-prd/
   ├── 02-domain-model/
   ├── 03-c4-architecture/
   ├── 04-design-doc/
   ├── 05-roadmap/
   └── 06-implementation/
   ```

3. **Execute Pipeline Stages**

   a. **Stage 1: PRD Creation**
   - Use `/create-prd` command
   - Save to `01-prd/product-requirements.md`

   b. **Stage 2: Domain Model**
   - Use `/create-domain-model` with PRD path
   - Save to `02-domain-model/domain-model.md`

   c. **Stage 3: C4 Architecture**
   - Use `/create-c4-model` with PRD and domain model paths
   - Save to `03-c4-architecture/`

   d. **Stage 4: Design Document**
   - Gather implementation requirements from user if needed
   - Use `/create-design-doc` with all previous docs
   - Save to `04-design-doc/design-document.md`

   e. **Stage 5: Roadmap & Epics**
   - Use `/create-roadmap` with design document
   - Save to `05-roadmap/implementation-roadmap.md`

   f. **Stage 6: Implementation Start**
   - Start from the most important epic
   - Use `general-purpose` agent to start the implementation

   g. **Stage 7: Implementation**
   - Receive feedback from the implementation agent
   - Use `/code-review` to review agent's work result
   - Give the feedback to agent and ask to fix
   - Check that the epic is really complete and all the requirements fullfilled
   - Mark epic as complete and move to the Stage 6 with next epic

4. **Progress Tracking**
   - After each stage, create a `progress.md` file tracking:
     - Completed stages with timestamps
     - Generated documents and their locations
     - Next steps and decisions needed

5. **Final Summary**
   - Present complete pipeline results
   - Show document hierarchy
   - Provide next steps for implementation

## Important Notes

- Each stage depends on the previous one's output
- Maintain consistent project context throughout
- Save all intermediate results for traceability
- Use clear folder structure for organization

## Error Handling

- If any stage fails, save progress so far
- Allow resuming from last successful stage
- Provide clear error messages with recovery options

## User Interaction Points
No interactions before the MVP implementation