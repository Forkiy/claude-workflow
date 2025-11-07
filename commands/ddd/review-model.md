---
allowed-tools: Task, Write, Glob
argument-hint: <domain-model-path> [optional: output-path]
description: Review an existing domain model for DDD alignment and best practices
---

Perform a comprehensive review of an existing domain model document using the ddd-architect agent to evaluate its alignment with Domain-Driven Design principles.

## Usage
`/ddd.review-model <domain-model-path> [output-path]`

Examples:
- `/ddd.review-model domain-model.md`
- `/ddd.review-model models/payment-domain.md review-results.md`
- `/ddd.review-model ./architecture/domain.md ./reviews/domain-review.md`

## Process

1. **Parse Arguments**:
   - Extract the domain model file path from `$ARGUMENTS` (required)
   - Extract the optional output file path (if not provided, default to `domain-model-review.md`)
   - Handle both relative and absolute paths

2. **Validate Inputs**:
   - Verify the domain model file exists and is readable
   - Check if the output directory exists (create if needed)
   - Verify write permissions for the output location

3. **Perform Review**:
   - Use the Task tool to launch the ddd-architect agent
   - Pass file path to the agent (NOT the content - agent will read it)
   - The prompt should be structured as:
     ```
     I need you to perform a comprehensive review of the provided domain model document.

     **Input File to Read:**
     - Domain Model: [FULL PATH TO DOMAIN MODEL FILE]

     First, use the Read tool to read the domain model file. Also check for any related implementation files if referenced and read them as well.

     Please evaluate this domain model against Domain-Driven Design principles and best practices.

     Focus your review on:
     - Alignment with DDD tactical and strategic patterns
     - Bounded context definitions and boundaries
     - Aggregate design for consistency and transactional boundaries
     - Ubiquitous language usage and clarity
     - Identification of anti-patterns or violations of DDD principles
     - Implementation gaps if code references are present

     Please create a comprehensive review document in markdown format with:
     - Executive summary of findings
     - Detailed analysis of domain model strengths
     - Identified problems and their severity (Critical/Major/Minor)
     - Specific recommendations for each issue
     - Implementation gaps between model and code (if applicable)
     - Prioritized action items for improvement
     ```

4. **Save and Report**:
   - Use Write tool to save the review output to the specified file
   - Confirm successful creation of the review
   - Show the file path where it was saved
   - Provide a summary of key findings and recommendations