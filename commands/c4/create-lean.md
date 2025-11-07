---
allowed-tools: Task, Glob
argument-hint: <prd-path> <domain-model-path> [optional: output-path]
description: Create lean C4 architecture model optimized for agent consumption (3-4 pages)
---

Create a lean, focused C4 architecture model from PRD and Domain Model using the c4-architecture-advisor agent. This command generates concise C4 diagrams and documentation optimized for technical implementation and downstream agent processing.

## Usage
`/arch-toolkit:c4:create-lean <prd-path> <domain-model-path> [output-path]`

Examples:
- `/arch-toolkit:c4:create-lean lean-prd.md lean-domain-model.md`
- `/arch-toolkit:c4:create-lean docs/prd.md models/domain.md lean-c4-architecture.md`
- `/arch-toolkit:c4:create-lean ./prd.md ./domain.md ./architecture/lean-c4.md`

## Process

1. **Parse Arguments**:
   - Extract the PRD file path from `$ARGUMENTS` (first argument, required)
   - Extract the Domain Model file path (second argument, required)
   - Extract the optional output file path (if not provided, default to `lean-c4-architecture.md`)
   - Handle both relative and absolute paths

2. **Validate Inputs**:
   - Verify both input files exist and are readable
   - Check if the output directory exists (create if needed)
   - Verify write permissions for the output location

3. **Generate Lean C4 Model**:
   - Use the Task tool to launch the c4-architecture-advisor agent
   - Pass file paths to the agent (NOT the content - agent will read them)
   - Provide the agent with a specific prompt for lean C4 model creation:
   ```
   Please create a LEAN C4 Architecture Model from the provided documents.

   **Input Files to Read:**
   - PRD: [FULL PATH TO PRD FILE]
   - Domain Model: [FULL PATH TO DOMAIN MODEL FILE]

   First, use the Read tool to read both input files, then proceed with creating the C4 model.

   **IMPORTANT: Create a concise, implementation-focused C4 model with ONLY these sections:**

   ## 1. System Context (Level 1)
   - System purpose (1-2 sentences)
   - Key external actors (users/systems, 3-5 items as bullets)
   - Critical integrations (2-3 most important)

   ```plantuml
   @startuml
   !include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Context.puml
   ' Simple context diagram (5-10 lines max)
   @enduml
   ```

   ## 2. Container Architecture (Level 2)
   For each container (typically 3-6 containers):
   - **[Container Name]** ([Technology])
     - Purpose: [one sentence]
     - Responsibilities: [2-3 bullets]
     - Key APIs/Interfaces: [list 2-3]

   ```plantuml
   @startuml
   !include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Container.puml
   ' Container diagram (10-15 lines max)
   @enduml
   ```

   ## 3. Technology Decisions
   **Core Stack**:
   - Frontend: [technology + why in 5 words]
   - Backend: [technology + why in 5 words]
   - Database: [technology + why in 5 words]
   - Infrastructure: [platform + why in 5 words]

   **Key Libraries/Frameworks** (3-5 most important):
   - [Library]: [purpose in one line]

   ## 4. Key Component Details
   For the 2 most critical containers only:

   ### [Container Name] Components
   - `[Component]`: [responsibility in one line]
   - `[Component]`: [responsibility in one line]
   - `[Component]`: [responsibility in one line]

   ## 5. Deployment Architecture
   **Environment**: [Cloud/On-prem/Hybrid]
   **Key Services** (bullets):
   - [Service type]: [specific use]

   Simple deployment overview (5 lines max):
   ```
   [ASCII or brief description]
   ```

   ## 6. Critical Design Decisions (ADRs)
   Top 3 architectural decisions:
   1. **[Decision]**: [Why + Impact in one line]
   2. **[Decision]**: [Why + Impact in one line]
   3. **[Decision]**: [Why + Impact in one line]

   ## 7. Implementation Starting Point
   - First container to build: [name + why]
   - MVP integration points: [2-3 bullets]
   - Can defer: [2-3 items]

   **LENGTH REQUIREMENT:** Keep the entire document to 3-4 pages (approximately 600-1000 words).
   Focus on essential architectural decisions needed for implementation. Skip detailed
   component internals, extensive security details, monitoring setup, and operational concerns.
   This model is for developers to understand the system structure and start building quickly.

   Keep PlantUML diagrams simple and readable - no more than 15 lines each.
   Use C4-PlantUML notation but prioritize clarity over completeness.

   **OUTPUT INSTRUCTIONS:**
   1. Use the Write tool to save the C4 model directly to: [FULL PATH TO OUTPUT FILE]
   2. After saving, return ONLY a brief summary (3-5 bullets) of the architecture decisions
   3. DO NOT return the full document content - just confirm it was saved and provide the summary
   ```

4. **Process Agent Response**:
   - **CRITICAL: DO NOT read the saved document - the agent has already saved it correctly**
   - Receive the agent's summary of the architecture
   - Do NOT use Read tool to view the document
   - Do NOT attempt to modify file
   - Confirm successful creation of the lean C4 architecture
   - Show the file path where it was saved
   - Display the agent's summary
   - Highlight that this is optimized for:
     - Agent consumption in pipelines
     - Quick implementation start
     - Design document generation
   - Suggest next steps (design document, implementation, etc.)