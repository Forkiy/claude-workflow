---
allowed-tools: Task, Glob
argument-hint: <prd-file-path> [optional: output-path]
description: Create a Domain Model from a PRD using Domain-Driven Design principles
---

Create a comprehensive Domain Model from a Product Requirements Document (PRD) using the ddd-architect agent and Domain-Driven Design principles.

## Usage
`/ddd.create-model <prd-file-path> [output-path]`

Examples:
- `/ddd.create-model carbon-tracker-prd.md`
- `/ddd.create-model docs/prd.md domain-model.md`
- `/ddd.create-model ./requirements/product-spec.md ./models/domain.md`

## Process

1. **Parse Arguments**:
   - Extract the PRD file path from `$ARGUMENTS` (required)
   - Extract the optional output file path (if not provided, default to `domain-model.md`)
   - Handle both relative and absolute paths

2. **Validate Inputs**:
   - Verify the PRD file exists and is readable
   - Check if the output directory exists (create if needed)
   - Verify write permissions for the output location

3. **Generate Domain Model**:
   - Use the Task tool to launch the ddd-architect agent
   - Pass file path to the agent (NOT the content - agent will read it)
   - The prompt should be structured as:
     ```
     I need you to create a comprehensive domain model from the provided Product Requirements Document.

     **Input File to Read:**
     - PRD: [FULL PATH TO PRD FILE]

     First, use the Read tool to read the PRD file, then proceed with creating the domain model.

     Please analyze the PRD and create a complete domain model following Domain-Driven Design principles.

     Focus on:
     - Identifying core domains, supporting domains, and generic subdomains
     - Defining bounded contexts with clear boundaries and relationships
     - Modeling aggregates, entities, value objects, and domain events
     - Establishing ubiquitous language for each bounded context
     - Creating PlantUML diagrams showing the domain model structure

     Please create a detailed markdown document with the complete domain model, including all necessary
     diagrams, explanations, and implementation guidance.

     **OUTPUT INSTRUCTIONS:**
     1. Use the Write tool to save the domain model directly to: [FULL PATH TO OUTPUT FILE]
     2. After saving, return ONLY a brief overview of what was created (3-5 bullets)
     3. DO NOT return the full document content - just confirm it was saved and provide the overview
     ```

4. **Process Agent Response**:
   - **CRITICAL: DO NOT read the saved document - the agent has already saved it correctly**
   - Receive the agent's overview of the domain model
   - Do NOT use Read tool to view the document
   - Do NOT attempt to modify or move the file (agent saved it to the correct location)
   - Confirm successful creation of the domain model
   - Show the file path where it was saved
   - Display the agent's overview