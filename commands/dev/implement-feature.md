---
allowed-tools: Bash(git:*), Read, Glob, Task, TodoWrite
argument-hint: <feature-description-or-doc-path>
description: Create a new branch and start implementing a feature from description or design document
---

Create a new git branch for a feature and begin its implementation based on either a direct description or a reference to a design document.

## Usage
`/implement-feature <feature-description-or-doc-path>`

Examples:
- `/implement-feature "Add user authentication with OAuth2"`
- `/implement-feature ./docs/auth-feature-design.md`
- `/implement-feature "Implement dark mode toggle in settings"`

## Process

1. **Parse Input**:
   - Determine if `$ARGUMENTS` is a file path (contains `.md` or starts with `.` or `/`)
   - If file path: Read the design document
   - If description: Use directly as feature specification

2. **Understand the Feature**:
   - Extract key requirements and scope
   - Identify main components to implement
   - Determine appropriate branch name

3. **Create Feature Branch**:
   - Check current branch status: `git status`
   - Ensure working directory is clean (commit or stash changes if needed)
   - Create descriptive branch name following pattern: `feature/[short-name]`
   - Create and checkout new branch: `git checkout -b feature/[name]`

4. **Plan Implementation**:
   - Use TodoWrite to create implementation task list
   - Break down feature into logical steps:
     - Core functionality implementation
     - Tests (if applicable)
     - Documentation updates
     - Integration points

5. **Choose Implementation Strategy**:

   **Option A: Full TDD Implementation** (Recommended for well-defined features):
   - Use Task tool to launch kent-beck-implementer agent
   - Provide design document or requirements
   - Agent will implement using Test-Driven Development
   - Returns summary of files created and test coverage

   **Option B: Architecture Guidance First** (For unclear requirements):
   - Use Task tool to launch bob-martin-architect agent
   - Get architectural design and patterns recommendation
   - Then use kent-beck-implementer for implementation

6. **Implementation with Kent Beck** (Primary Approach):
   ```
   You are tasked with implementing a new feature using Test-Driven Development.

   **IMPLEMENTATION MODE**

   Feature Requirements:
   <requirements>
   [Insert feature description or design document]
   </requirements>

   Implementation Instructions:
   1. Follow Red-Green-Refactor cycle for each component
   2. Write comprehensive tests before implementation
   3. Use appropriate design patterns
   4. Maintain high test coverage (>80%)
   5. Keep methods small and focused

   **OUTPUT REQUIREMENTS:**
   1. Save all files directly using Write tool
   2. Return implementation report with:
      - Files created/modified
      - Test statistics and coverage
      - Key patterns used
      - Important decisions made
   3. DO NOT output code in response
   ```

7. **Process Agent Response & Status Update**:
   - Receive implementation report from agent
   - **DO NOT** read created files (trust the expert)
   - Display summary to user:
     ```
     ✓ Feature branch created: feature/[name]
     ✓ Implementation started by Kent Beck

     [Agent's Implementation Report]

     Next steps:
     - Review implementation with git diff
     - Run tests to verify
     - Continue development or commit with /commit
     ```

## Agent Roles

**kent-beck-implementer**: Handles actual code implementation
- Writes tests and production code
- Follows TDD principles strictly
- Returns summaries, not code listings
- Maintains high test coverage

**bob-martin-architect**: Provides design guidance
- Reviews architecture decisions
- Suggests design patterns
- Ensures SOLID principles
- Creates implementation blueprints (no code)

## Important Notes
- Always ensure clean working directory before creating branch
- Branch names should be descriptive but concise (max 30 chars)
- If feature is large, suggest breaking into smaller sub-features
- Trust the agents - don't re-read files they create
- Focus conversation on progress, not code details