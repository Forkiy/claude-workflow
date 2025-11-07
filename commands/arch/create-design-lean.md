---
allowed-tools: Task, Glob
argument-hint: <prd-path> <domain-model-path> <c4-architecture-path> [optional: output-path]
description: Create lean design document optimized for agent implementation (4-5 pages)
---

Create a lean, implementation-focused Design Document from PRD, Domain Model, and C4 Architecture using the bob-martin-architect agent. This command generates a concise design document optimized for developers and AI agents to start implementation immediately.

## Usage
`/arch.create-design-lean <prd-path> <domain-model-path> <c4-architecture-path> [output-path]`

Examples:
- `/arch.create-design-lean lean-prd.md lean-domain-model.md lean-c4-architecture.md`
- `/arch.create-design-lean docs/prd.md models/domain.md arch/c4.md lean-design.md`

## Process

1. **Parse Arguments**:
   - Extract the PRD file path (first argument, required)
   - Extract the Domain Model file path (second argument, required)
   - Extract the C4 Architecture file path (third argument, required)
   - Extract the optional output file path (default to `lean-design-document.md`)
   - Handle both relative and absolute paths

2. **Validate Inputs**:
   - Verify all input files exist and are readable
   - Check if the output directory exists (create if needed)
   - Verify write permissions for the output location

3. **Generate Lean Design Document**:
   - Use the Task tool to launch the bob-martin-architect agent
   - Pass file paths to the agent (NOT the content - agent will read them)
   - Provide the agent with a specific prompt for lean design document creation:
   ```
   Please create a LEAN Design Document from the provided documents, applying clean architecture principles.

   **Input Files to Read:**
   - PRD: [FULL PATH TO PRD FILE]
   - Domain Model: [FULL PATH TO DOMAIN MODEL FILE]
   - C4 Architecture: [FULL PATH TO C4 ARCHITECTURE FILE]

   First, use the Read tool to read all three input files, then proceed with creating the design document.

   **IMPORTANT: Create a concise, implementation-ready design document with ONLY these sections:**

   ## 1. Design Overview
   - System purpose (1 sentence referencing the PRD problem)
   - Architectural style (Clean/Hexagonal/Layered/etc. + why in 1 sentence)
   - Key design principles we'll follow (3-5 bullets, one line each)

   ## 2. Core Design Structure

   ### Layer Architecture
   Brief description of layers and their responsibilities:
   - **Domain Layer**: [what it contains, 1-2 lines]
   - **Application Layer**: [what it contains, 1-2 lines]
   - **Infrastructure Layer**: [what it contains, 1-2 lines]
   - **Presentation Layer**: [what it contains, 1-2 lines]

   ### Dependency Rules
   - [Layer A] → [Layer B]: [what's allowed]
   - Key rule violations to avoid: [2-3 bullets]

   ## 3. Module Implementation Design

   For each bounded context/major module (2-4 modules):

   ### [Module Name]
   **Core Components**:
   - `[Interface/Class Name]`: [responsibility + key methods in one line]
   - `[Interface/Class Name]`: [responsibility + key methods in one line]

   **Design Patterns Used**:
   - [Pattern]: [where and why in one line]

   **Key Interfaces** (2-3 most important):
   ```
   interface [Name] {
     [method signature]  // [purpose in 3-5 words]
     [method signature]  // [purpose in 3-5 words]
   }
   ```

   ## 4. Data Design

   ### Storage Strategy
   - Primary storage: [technology + pattern (Repository/DAO/etc.)]
   - Domain model mapping: [how entities map to storage]

   ### Key Data Structures (3-5 most important)
   ```
   [EntityName]: {
     [key fields with types]
   }
   ```

   ## 5. API Design

   ### External APIs (REST/GraphQL/gRPC)
   Key endpoints (5-7 most important):
   - `[METHOD] /path`: [purpose + request/response summary]

   ### Internal Service Interfaces
   Critical service contracts (2-3):
   - `[ServiceName].[method]`: [input → output summary]

   ## 6. Critical Algorithms

   For 1-2 most complex/important algorithms:
   - **[Algorithm Name]**:
     - Purpose: [one line]
     - Approach: [2-3 lines or pseudocode]
     - Complexity: O([complexity])

   ## 7. Error Handling Strategy
   - Exception hierarchy: [2-3 main exception types]
   - Error propagation: [how errors flow through layers]
   - Client error format: [standard error response structure]

   ## 8. Testing Strategy
   - Unit test focus: [what to test heavily]
   - Integration test boundaries: [key integration points]
   - Test data approach: [builders/fixtures/mocks strategy]

   ## 9. Key Risks & Mitigations
   Top 3 technical risks:
   1. **[Risk]**: Mitigation: [one line action]
   2. **[Risk]**: Mitigation: [one line action]
   3. **[Risk]**: Mitigation: [one line action]

   # Output rules:

   **ABSOLUTELY FORBIDDEN:**
   - Complete function/method implementations
   - Detailed algorithm implementations
   - Full class implementations with logic
   - Working code examples longer than 10 lines
   - Any code that could be copy-pasted and run
   - Implementation-level details or specific library usage
   - Low-level code optimizations

   **ACCEPTABLE ONLY:**
   - Interface definitions (signatures only, max 5-10 lines)
   - High-level pseudocode 
   - API contract examples (structure only)
   - Data structure schemas (without implementation)
   - Architecture patterns (described, not implemented)

   **PRIMARY OUTPUT FOCUS:**
   1. PlantUML diagrams (C4, sequence, component) - diagrams replace code!
   2. Architectural decisions and rationale (ADRs)
   3. Component responsibilities and boundaries
   4. Quality attribute requirements (performance, security, scalability)
   5. Trade-off analysis and alternatives considered

   **SELF-CHECK before each document:**
   □ Am I describing architecture or implementation?
   □ Could this code be copy-pasted and run? (If yes, DELETE)
   □ Can this be expressed as a diagram instead? (If yes, DO IT)
   □ Am I explaining WHAT and WHY, not HOW to code it?

   **CRITICAL REMINDER:** If you're about to write more than 10 lines of code, STOP. Create a sequence diagram instead. A good diagram is worth 1000 lines of code you DON'T write.

   **LENGTH REQUIREMENT:** Keep the entire document to 4-5 pages (approximately 800-1200 words).
   Focus on concrete implementation guidance. Skip philosophical discussions, extensive
   background, detailed database schemas, deployment procedures, and monitoring setup.
   This document should enable a developer to start coding immediately with clear direction.

   Apply Bob Martin's clean architecture principles throughout but keep explanations brief.
   Code examples should be minimal but illustrative - prefer interface definitions over implementations.

   **OUTPUT INSTRUCTIONS:**
   1. Use the Write tool to save the design document directly to: [FULL PATH TO OUTPUT FILE]
   2. After saving, return ONLY a brief summary (3-5 bullets) of the key design decisions
   3. DO NOT return the full document content - just confirm it was saved and provide the summary
   ```

5. **Process Agent Response**:
   - **CRITICAL: DO NOT read the saved document - the agent has already saved it correctly**
   - Receive the agent's summary of the design decisions
   - Do NOT use Read tool to view the document
   - Do NOT attempt to modify the file
   - Confirm successful creation of the lean design document
   - Show the file path where it was saved
   - Display the agent's summary
   - Highlight that this is optimized for:
     - Immediate implementation start
     - AI agent code generation
     - Clear architectural boundaries
   - Suggest next steps (implementation, epic decomposition, etc.)