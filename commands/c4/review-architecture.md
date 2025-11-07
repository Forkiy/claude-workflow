---
allowed-tools: Task, Write, Glob
argument-hint: <architecture-doc-path> [optional: output-path]
description: Review architecture documentation and C4 diagrams for clarity and best practices
---

Review existing architecture documentation and C4 diagrams using the c4-architecture-advisor agent to evaluate clarity, completeness, and alignment with best practices.

## Usage
`/c4.review-architecture <architecture-doc-path> [output-path]`

Examples:
- `/c4.review-architecture c4-architecture.md`
- `/c4.review-architecture docs/architecture.md review-results.md`
- `/c4.review-architecture ./system/c4-model.md ./reviews/architecture-review.md`

## Process

1. **Parse Arguments**:
   - Extract the architecture document path from `$ARGUMENTS` (required)
   - Extract the optional output file path (if not provided, default to `architecture-review.md`)
   - Handle both relative and absolute paths

2. **Validate Inputs**:
   - Verify the architecture document exists and is readable
   - Check if the output directory exists (create if needed)
   - Verify write permissions for the output location

3. **Perform Architecture Review**:
   - Use the Task tool to launch the c4-architecture-advisor agent
   - Pass file path to the agent (NOT the content - agent will read it)
   - The prompt should be structured as:
     ```
     I need you to review the provided architecture documentation and provide pragmatic feedback.

     **Input File to Read:**
     - Architecture Documentation: [FULL PATH TO ARCHITECTURE FILE]
     - Additional files if found: [LIST OF PATHS TO REFERENCED FILES]

     First, use the Read tool to read the architecture file. Check for any referenced diagram files or supporting documentation and read them as well.

     Please evaluate the documentation and diagrams focusing on:

     **Clarity and Communication:**
     - Can a new team member understand this architecture?
     - Are the diagrams clear and properly labeled?
     - Is the intended audience clear for each diagram?

     **C4 Model Alignment:**
     - Consistency across abstraction levels (Context → Container → Component)
     - Appropriate level of detail at each level
     - Clear boundaries and relationships

     **Pragmatic Concerns:**
     - Is this documentation "just enough" or is there unnecessary complexity?
     - Will this stay maintainable as the system evolves?
     - Are the technology choices justified?
     - Are key architectural decisions documented?

     **Missing Elements:**
     - What important information is missing?
     - Which relationships or boundaries are unclear?
     - What questions would a developer have?

     Please provide:
     - Executive summary of the review
     - Strengths of the current documentation
     - Issues identified (categorized by severity)
     - Specific, actionable recommendations
     - Suggestions for keeping documentation in sync with code

     Be pragmatic and direct. Focus on what will actually help the team,
     not theoretical perfection. Avoid over-engineering suggestions.
     ```

4. **Save and Report**:
   - Use Write tool to save the review to the specified file
   - Confirm successful completion of the review
   - Show the file path where it was saved
   - Provide a summary of:
     - Overall assessment
     - Key strengths identified
     - Critical issues found
     - Top recommendations for improvement