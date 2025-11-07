---
allowed-tools: Task, Glob
argument-hint: <prd-path> <domain-model-path> [optional: output-path]
description: Create C4 architecture model diagrams from PRD and Domain Model documents
---

Create comprehensive C4 architecture model diagrams and documentation from Product Requirements Document (PRD) and Domain Model using the c4-architecture-advisor agent.

## Usage
`/arch-toolkit:c4:create-model <prd-path> <domain-model-path> [output-path]`

Examples:
- `/arch-toolkit:c4:create-model prd.md domain-model.md`
- `/arch-toolkit:c4:create-model docs/prd.md models/domain.md c4-architecture.md`
- `/arch-toolkit:c4:create-model ./requirements/spec.md ./models/domain.md ./architecture/c4-model.md`

## Process

1. **Parse Arguments**:
   - Extract the PRD file path from `$ARGUMENTS` (first argument, required)
   - Extract the Domain Model file path (second argument, required)
   - Extract the optional output file path (if not provided, default to `c4-architecture.md`)
   - Handle both relative and absolute paths

2. **Validate Inputs**:
   - Verify both input files exist and are readable
   - Check if the output directory exists (create if needed)
   - Verify write permissions for the output location

3. **Generate C4 Model**:
   - Use the Task tool to launch the c4-architecture-advisor agent
   - Pass file paths to the agent (NOT the content - agent will read them)
   - The prompt should be structured as:
     ```
     I need you to create comprehensive C4 architecture model diagrams and documentation based on the
     provided Product Requirements Document and Domain Model.

     **Input Files to Read:**
     - PRD: [FULL PATH TO PRD FILE]
     - Domain Model: [FULL PATH TO DOMAIN MODEL FILE]

     First, use the Read tool to read both input files, then proceed with creating the C4 model.

     Please create a complete C4 model following Simon Brown's C4 methodology, including:

     1. **System Context Diagram**: Show users and external systems
     2. **Container Diagram**: Define major technical building blocks
     3. **Component Diagrams**: Detail internal structure where complexity warrants
     4. **Deployment Diagram**: Show how containers map to infrastructure

     Include PlantUML code for all diagrams using C4-PlantUML syntax.

     Also provide:
     - Architectural Decision Records (ADRs) for key decisions
     - Technology stack justification
     - Deployment architecture
     - Security considerations
     - Performance and scalability notes
     - Integration patterns and API designs

     Be pragmatic and focus on what the team needs to understand the system.
     Avoid over-engineering or unnecessary complexity.
     Ensure diagrams are clear enough for new team members to understand.

     **OUTPUT INSTRUCTIONS:**
     1. Use the Write tool to save the C4 model directly to: [FULL PATH TO OUTPUT FILE]
     2. After saving, return ONLY a brief overview:
        - Number of diagrams created (per level)
        - Key architectural decisions made
        - Technology stack chosen
        - Main containers and components identified
     3. DO NOT return the full document content - just confirm it was saved and provide the overview
     ```

4. **Process Agent Response**:
   - **CRITICAL: DO NOT read the saved document - the agent has already saved it correctly**
   - Receive the agent's overview of what was created
   - Do NOT use Read tool to view the document
   - Do NOT attempt to modify the file
   - Confirm successful creation of the C4 architecture model
   - Show the file path where it was saved
   - Display the agent's overview