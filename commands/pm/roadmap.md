---
description: "Create implementation roadmap with milestones and epics using Jeff Patton's story mapping"
allowed-tools: ["Glob", "Task"]
argument-hint: "<design-doc-path> [optional: output-path]"
---

# Create Implementation Roadmap

Generate a delivery-focused implementation roadmap using Jeff Patton's story mapping methodology.

## Arguments

Parse the arguments from: `$ARGUMENTS`
- First argument: Path to design document (required)
- Second argument: Output path for roadmap (optional, defaults to `implementation-roadmap.md`)

## Process

1. **Validate Input Documents**
   - Verify the design document exists and is readable
   - Look for related documents (PRD, Domain Model, C4 diagrams) in same directory

2. **Launch Jeff Patton Agent**

   Use the Task tool to launch the jeff-patton-pm agent:

   ```
   Create a concise, delivery-focused implementation roadmap from the provided design documentation.

   ## Input Files to Read
   Design Document: [FULL PATH TO DESIGN DOCUMENT]
   Additional documents if found: [LIST OF PATHS TO RELATED DOCUMENTS]

   First, use the Read tool to read all input files, then proceed with creating the roadmap.

   ## Required Output

   Generate a roadmap with these sections:

   1. **Walking Skeleton (Week 1-2)**
      - Minimal end-to-end implementation
      - Core architecture connected
      - Single user journey working
      - List 3-5 specific tasks

   2. **MVP Release (Week 3-6)**
      - Core features only
      - Essential user workflows
      - Basic but complete functionality
      - List 5-7 epics with 1-line descriptions

   3. **Feature Complete (Week 7-10)**
      - All planned features
      - Performance optimization
      - Error handling
      - List 5-7 epics

   4. **Production Ready (Week 11-12)**
      - Polish and refinement
      - Monitoring/observability
      - Documentation
      - List 3-5 tasks

   5. **Implementation Order**
      Prioritized list of what to build first:
      1. [First epic/feature - why it's first]
      2. [Second epic/feature - dependencies]
      3. [Continue for top 10 items]

   6. **Technical Dependencies**
      - Required infrastructure
      - External services needed
      - Key technical decisions

   ## Format Requirements
   - Concise bullet points
   - Focus on WHAT to build, not HOW
   - Include rough time estimates
   - Actionable epic titles (e.g., "Implement user authentication" not "Auth system")
   - No excessive detail - this is for AI agent execution

   Keep the entire roadmap under 500 lines. Focus on delivery sequence and dependencies.

   **OUTPUT INSTRUCTIONS:**
   1. Use the Write tool to save the roadmap directly to: [FULL PATH TO OUTPUT FILE]
   2. After saving, return ONLY the first 3 implementation priorities as a summary
   3. DO NOT return the full document content - just confirm it was saved and provide the priorities
   ```

3. **Process Agent Response**
   - **CRITICAL: DO NOT read the saved document - the agent has already saved it correctly**
   - Receive the agent's summary of implementation priorities
   - Do NOT use Read tool to view the document
   - Do NOT attempt to modify or move the file (agent saved it to the correct location)
   - Display the first 3 implementation priorities from the agent
   - Suggest: `/implement-feature [first-epic]` to begin