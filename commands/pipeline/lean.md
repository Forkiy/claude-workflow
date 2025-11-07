---
allowed-tools: SlashCommand, Read, Write, Bash
argument-hint: <project-idea> [optional: output-folder]
description: Execute lean document pipeline from idea to implementation-ready design (PRD → Domain → C4 → Design)
---

Execute the complete lean documentation pipeline from a project idea to implementation-ready design documents. This creates a full set of concise, AI-agent-optimized documents perfect for rapid development.

## Usage
`/pipeline.lean "<project idea>" [output-folder]`

Examples:
- `/pipeline.lean "A mobile app for tracking personal carbon footprint"`
- `/pipeline.lean "Developer productivity dashboard" ./docs/lean-pipeline`

## Pipeline Stages

This command orchestrates the following lean document generation:

1. **Lean PRD** → Problem definition and requirements (2-4 pages)
2. **Lean Domain Model** → Core business concepts and boundaries (2-3 pages)
3. **Lean C4 Architecture** → System structure and technology (3-4 pages)
4. **Lean Design Document** → Implementation blueprint (4-5 pages)

Total output: ~15 pages of focused, actionable documentation

## Process

1. **Parse Arguments**:
   - Extract project idea from `$ARGUMENTS` (required, may be quoted)
   - Extract optional output folder (default to `./lean-docs-[timestamp]`)
   - Create output folder if it doesn't exist

2. **Stage 1: Generate Lean PRD**
   ```bash
   echo "📝 Stage 1/4: Generating Lean PRD..."
   ```
   - Invoke `/prd.create-lean "$PROJECT_IDEA" $OUTPUT_FOLDER/1-lean-prd.md`
   - Verify successful creation before proceeding

3. **Stage 2: Generate Lean Domain Model**
   ```bash
   echo "🏗️ Stage 2/4: Generating Lean Domain Model..."
   ```
   - Invoke `/ddd.create-lean $OUTPUT_FOLDER/1-lean-prd.md $OUTPUT_FOLDER/2-lean-domain-model.md`
   - Verify successful creation before proceeding

4. **Stage 3: Generate Lean C4 Architecture**
   ```bash
   echo "🏛️ Stage 3/4: Generating Lean C4 Architecture..."
   ```
   - Invoke `/c4.create-lean $OUTPUT_FOLDER/1-lean-prd.md $OUTPUT_FOLDER/2-lean-domain-model.md $OUTPUT_FOLDER/3-lean-c4-architecture.md`
   - Verify successful creation before proceeding

5. **Stage 4: Generate Lean Design Document**
   ```bash
   echo "📐 Stage 4/4: Generating Lean Design Document..."
   ```
   - Invoke `/arch.create-design-lean $OUTPUT_FOLDER/1-lean-prd.md $OUTPUT_FOLDER/2-lean-domain-model.md $OUTPUT_FOLDER/3-lean-c4-architecture.md $OUTPUT_FOLDER/4-lean-design-document.md`
   - Verify successful creation

6. **Create Pipeline Summary**
   Create `$OUTPUT_FOLDER/README.md` with:
   ```markdown
   # Lean Documentation Pipeline Output

   Generated: [timestamp]
   Project: [project idea]

   ## Documents Created

   1. **[Lean PRD](1-lean-prd.md)** - Problem definition and requirements
   2. **[Lean Domain Model](2-lean-domain-model.md)** - Business concepts and boundaries
   3. **[Lean C4 Architecture](3-lean-c4-architecture.md)** - System structure and technology
   4. **[Lean Design Document](4-lean-design-document.md)** - Implementation blueprint

   ## Pipeline Characteristics

   - **Optimized for AI agents**: Structured for machine processing
   - **Concise**: ~15 pages total vs 50+ for full documentation
   - **Implementation-focused**: Skip theory, focus on building
   - **Fast generation**: Complete pipeline in 2-3 minutes

   ## Next Steps

   With these documents, you can:
   1. Start implementation with `/dev.implement-feature 4-lean-design-document.md`
   2. Generate epics with `/pm.decompose-epics 4-lean-design-document.md`
   3. Create detailed versions if needed with standard commands
   4. Share with team for rapid alignment

   ## Document Flow

   ```
   [Idea] → PRD → Domain Model → C4 Architecture → Design Document → [Implementation]
            ↓         ↓              ↓                  ↓
         Problem → Concepts →   Structure →      Blueprint
   ```
   ```

7. **Final Summary**
   Display to user:
   ```
   ✅ Lean Pipeline Complete!

   📁 Output folder: [folder path]

   Documents generated:
   • Lean PRD (2-4 pages)
   • Lean Domain Model (2-3 pages)
   • Lean C4 Architecture (3-4 pages)
   • Lean Design Document (4-5 pages)

   Total: ~15 pages of implementation-ready documentation

   Ready to start coding! Use the design document for implementation.
   ```

## Error Handling

- If any stage fails, stop the pipeline and report which stage failed
- Provide the error message and suggest manual completion
- Save progress so far (partial pipeline is still useful)

## Benefits

This lean pipeline provides:
- **90% faster** than full documentation pipeline
- **More focused** - only essential information for building
- **AI-optimized** - perfect for agent-driven development
- **Iterative-friendly** - easy to regenerate as requirements change