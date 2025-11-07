---
allowed-tools: Task, Read, Write, Glob, Grep
argument-hint: [optional: codebase-path] [optional: output-path]
description: Extract and refine domain model from existing codebase
---

Extract the implicit domain model from an existing codebase and create a refined DDD-aligned version using the ddd-architect agent.

## Usage
`/ddd.extract-model [codebase-path] [output-path]`

Examples:
- `/ddd.extract-model` (analyzes current directory)
- `/ddd.extract-model ./src extracted-domain.md`
- `/ddd.extract-model /path/to/project ./models/extracted-domain.md`

## Process

1. **Parse Arguments**:
   - Extract the optional codebase path (default to current directory)
   - Extract the optional output file path (default to `extracted-domain-model.md`)
   - Handle both relative and absolute paths

2. **Analyze Codebase Structure**:
   - Use Glob to find key directories (src, lib, app, domain, etc.)
   - Identify the technology stack and framework patterns
   - Locate domain/model/entity directories if they exist

3. **Extract Key Domain Elements**:
   - Use Grep to find common domain patterns:
     - Entity/Model classes
     - Service/Repository patterns
     - Event definitions
     - API endpoints and controllers
   - Use Read to examine key files for domain logic

4. **Generate Extraction Analysis**:
   - Use the Task tool to launch the ddd-architect agent
   - Provide the agent with:
     - Overview of codebase structure
     - Key domain files and patterns found
     - Sample code showing domain implementation
   - The prompt should be structured as:
     ```
     I need you to extract and refine the domain model from an existing codebase.

     Based on the following codebase analysis, please create a comprehensive domain model extraction.

     Codebase Overview:
     [STRUCTURE AND TECHNOLOGY STACK]

     Key Domain Elements Found:
     [ENTITIES, SERVICES, REPOSITORIES, EVENTS]

     Sample Implementation Code:
     [RELEVANT CODE SAMPLES]

     Please create a document with three distinct sections:

     1. **Current Model Extraction**: Document the domain model as it exists in the code
        - Identify existing entities, aggregates, and services
        - Map current bounded contexts (even if implicit)
        - Document actual relationships and dependencies

     2. **Refined Domain Model**: Create the ideal DDD-aligned model
        - Apply proper bounded context separation
        - Design clean aggregates with proper boundaries
        - Define clear domain events and value objects
        - Establish proper ubiquitous language

     3. **Gap Analysis**: Identify differences between current and ideal
        - List specific changes needed
        - Prioritize refactoring efforts (High/Medium/Low impact)
        - Provide justification for each proposed change
        - Estimate complexity and risk for transformations

     Include PlantUML diagrams for both current and refined models.
     ```

5. **Save and Report**:
   - Use Write tool to save the extraction analysis to the specified file
   - Confirm successful extraction and analysis
   - Show the file path where it was saved
   - Provide a summary of:
     - Current domain structure found
     - Key improvements recommended
     - Priority refactoring suggestions