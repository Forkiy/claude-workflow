---
allowed-tools: Task, Glob
argument-hint: <prd-file-path> [optional: output-path]
description: Create a lean domain model optimized for agent consumption (2-3 pages)
---

Create a lean, focused Domain Model from a Product Requirements Document (PRD) using the ddd-architect agent. This command generates concise domain models optimized for technical implementation and downstream agent processing.

## Usage
`/arch-toolkit:ddd:create-lean <prd-file-path> [output-path]`

Examples:
- `/arch-toolkit:ddd:create-lean lean-prd.md`
- `/arch-toolkit:ddd:create-lean docs/prd.md lean-domain-model.md`
- `/arch-toolkit:ddd:create-lean ./requirements/spec.md ./models/lean-domain.md`

## Process

1. **Parse Arguments**:
   - Extract the PRD file path from `$ARGUMENTS` (required)
   - Extract the optional output file path (if not provided, default to `lean-domain-model.md`)
   - Handle both relative and absolute paths

2. **Validate Inputs**:
   - Verify the PRD file exists and is readable
   - Check if the output directory exists (create if needed)
   - Verify write permissions for the output location

3. **Generate Lean Domain Model**:
   - Use the Task tool to launch the ddd-architect agent
   - Pass file path to the agent (NOT the content - agent will read it)
   - Provide the agent with a specific prompt for lean domain model creation:
   ```
   Please create a LEAN Domain Model from the provided Product Requirements Document.

   **Input File to Read:**
   - PRD: [FULL PATH TO PRD FILE]

   First, use the Read tool to read the PRD file, then proceed with creating the domain model.

   **IMPORTANT: Create a concise, implementation-focused domain model with ONLY these sections:**

   ## 1. Core Domain Overview
   - Problem domain in 2-3 sentences
   - Core business capability being modeled
   - Key business invariants (3-5 rules that must always be true)

   ## 2. Bounded Contexts
   For each context (typically 2-4 contexts):
   - **[Context Name]**
     - Purpose (1 sentence)
     - Key responsibilities (3-4 bullet points)
     - Main aggregates (list names only)

   ## 3. Domain Model Structure
   For each bounded context, list ONLY the most critical elements:

   ### [Context Name]
   **Aggregates** (2-3 per context):
   - `[AggregateName]`: [one-line purpose]
     - Key fields: [list 3-5 most important]
     - Key behaviors: [list 2-3 main operations]

   **Value Objects** (3-5 total):
   - `[ValueObjectName]`: [one-line description]

   **Domain Events** (3-5 most important):
   - `[EventName]`: [when it occurs]

   ## 4. Context Relationships
   Simple ASCII or bullet list showing how contexts communicate:
   - [Context A] → [Context B]: [interaction type]
   - Shared kernel: [if any]
   - Anti-corruption layer needs: [if any]

   ## 5. Implementation Priority
   - Start with: [which context/aggregate]
   - Critical path: [2-3 step implementation order]
   - Can defer: [what can wait]

   **LENGTH REQUIREMENT:** Keep the entire document to 2-3 pages (approximately 400-800 words).
   Focus on essential domain concepts needed for implementation. Skip theoretical DDD
   explanations, detailed entity attributes, repository patterns, and infrastructure concerns.
   This model is for developers to understand the core domain structure quickly.

   Include a single PlantUML diagram showing the high-level bounded context map if helpful,
   but keep it simple (no more than 10-15 lines of PlantUML code).

   **OUTPUT INSTRUCTIONS:**
   1. Use the Write tool to save the domain model directly to: [FULL PATH TO OUTPUT FILE]
   2. After saving, return ONLY a brief summary (3-5 bullets) of the key domain concepts
   3. DO NOT return the full document content - just confirm it was saved and provide the summary
   ```

4. **Process Agent Response**:
   - **CRITICAL: DO NOT read the saved document - the agent has already saved it correctly**
   - Receive the agent's summary of the domain model
   - Do NOT use Read tool to view the document
   - Do NOT attempt to modify file
   - Confirm successful creation of the lean domain model
   - Show the file path where it was saved
   - Display the agent's summary
   - Highlight that this is optimized for:
     - Agent consumption in pipelines
     - Quick implementation planning
     - C4 architecture generation
   - Suggest next steps (C4 model, design document, etc.)