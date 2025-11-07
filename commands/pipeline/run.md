---
description: "Orchestrate software development pipeline with intelligent stage management"
allowed-tools: ["Read", "Write", "Glob", "Task", "Bash", "SlashCommand", "TodoWrite"]
argument-hint: "[start|resume|status] <project-name-or-folder>"
---

# Software Development Pipeline Orchestrator

Intelligent pipeline orchestration that can start new projects or resume existing ones.

## Arguments

Parse the arguments from: `$ARGUMENTS`

Expected formats:
- `start <project-name>` - Start new pipeline for project
- `resume <project-folder>` - Resume from last completed stage
- `status <project-folder>` - Show pipeline status
- Just `<project-idea>` - Auto-detect and start new pipeline

## Pipeline Stages

1. **PRD** - Product Requirements Document
2. **Domain** - Domain Model from DDD
3. **C4** - Architecture diagrams
4. **Design** - Comprehensive design document
5. **Roadmap** - Implementation roadmap with epics
6. **Implement** - Begin feature development

## Execution Logic

### For NEW Projects (start or auto-detected)

1. **Initialize Project Structure**
   ```
   projects/<project-name>/
   ├── .pipeline-state.json
   ├── 01-requirements/
   │   └── prd.md
   ├── 02-domain/
   │   └── domain-model.md
   ├── 03-architecture/
   │   └── c4-diagrams/
   ├── 04-design/
   │   └── design-doc.md
   ├── 05-roadmap/
   │   └── roadmap.md
   └── 06-implementation/
       └── feature-branches/
   ```

2. **Create Pipeline State Tracker**
   ```json
   {
     "project": "project-name",
     "created": "timestamp",
     "current_stage": "prd",
     "completed_stages": [],
     "stage_outputs": {},
     "last_updated": "timestamp"
   }
   ```

3. **Execute Stages Sequentially**
   - Use TodoWrite to track pipeline progress
   - After each stage, update state file
   - Ask for user review between stages

### For RESUME Operations

1. **Read Pipeline State**
   - Load `.pipeline-state.json`
   - Identify last completed stage
   - Show summary of completed work

2. **Continue from Next Stage**
   - Use existing outputs as inputs
   - Skip completed stages
   - Maintain context from previous stages

### For STATUS Operations

1. **Display Pipeline Overview**
   - Show completed stages with checkmarks
   - List generated documents
   - Show current stage and next steps
   - Estimate remaining work

## Stage Execution Details

### Stage 1: PRD Creation
```bash
# Check if PRD exists
if [[ ! -f "01-requirements/prd.md" ]]; then
  # Execute PRD creation
  /arch-toolkit:prd:create "$PROJECT_IDEA" "01-requirements/prd.md"
fi
```

### Stage 2: Domain Modeling
```bash
# Use PRD as input
/arch-toolkit:ddd:create-model "01-requirements/prd.md" "02-domain/domain-model.md"
```

### Stage 3: C4 Architecture
```bash
/arch-toolkit:c4:create-model "01-requirements/prd.md" "02-domain/domain-model.md" "03-architecture/"
```

### Stage 4: Design Document
```bash
# Gather implementation details if needed
/arch-toolkit:arch:create-design-document "01-requirements:02-domain:03-architecture" "$IMPLEMENTATION_DETAILS" "04-design/design-doc.md"
```

### Stage 5: Roadmap Creation
```bash
/arch-toolkit:pm:roadmap "04-design/design-doc.md" "05-roadmap/roadmap.md"
```

### Stage 6: Implementation
```bash
# Read roadmap and identify first epic
# Show user the priorities
# Ask which to implement first
/arch-toolkit:dev:implement-feature "$SELECTED_EPIC"
```

## Interactive Checkpoints

Between each stage, present:
```
✅ Stage X completed: [Stage Name]
📄 Generated: [document-path]

Review options:
1. View generated document
2. Edit document
3. Continue to next stage
4. Pause pipeline (can resume later)

Choice [1-4]:
```

## Progress Tracking

Use TodoWrite tool to maintain task list:
- [ ] Create PRD
- [ ] Generate Domain Model
- [ ] Design C4 Architecture
- [ ] Write Design Document
- [ ] Create Implementation Roadmap
- [ ] Start Implementation

## Error Recovery

If any stage fails:
1. Save error details to `.pipeline-errors.log`
2. Mark stage as "failed" in state
3. Provide recovery options:
   - Retry stage
   - Skip stage (if optional)
   - Fix manually and continue
   - Abort pipeline

## Completion

When pipeline completes:
1. Generate `PIPELINE-COMPLETE.md` summary
2. Include all document links
3. Show implementation quick-start
4. Provide next step commands

## Smart Features

- **Auto-resume**: Detects incomplete pipelines in current directory
- **Parallel Docs**: Can generate independent docs simultaneously
- **Incremental Updates**: Can re-run stages with updated inputs
- **Version Tracking**: Maintains document versions through pipeline