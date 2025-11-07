---
allowed-tools: Bash(git:*), Read, Glob, Grep, Task
argument-hint: <bug-description-or-issue-reference>
description: Create a branch, write a failing test that reproduces the bug, then fix it following TDD
---

Fix a bug following Test-Driven Development (TDD) principles by first writing a failing test that reproduces the issue, then implementing the fix.

## Usage
`/fix-bug <bug-description-or-issue-reference>`

Examples:
- `/fix-bug "User login fails when email contains special characters"`
- `/fix-bug "#142"` (GitHub issue reference)
- `/fix-bug ./bugs/auth-timeout-issue.md`
- `/fix-bug "Calculator returns NaN when dividing by zero instead of throwing error"`

## Process

1. **Parse Input & Understand the Bug**:
   - Determine input type:
     - Issue reference (starts with #): Fetch issue details using `gh issue view`
     - File path (.md or starts with . or /): Read bug report document
     - Description: Use directly as bug specification
   - Extract:
     - Bug symptoms and behavior
     - Expected vs actual behavior
     - Steps to reproduce
     - Affected components/files

2. **Create Bug Fix Branch**:
   - Check current branch and working directory status: `git status`
   - Ensure clean working directory (commit or stash if needed)
   - Create branch following pattern: `fix/[short-description]` or `bugfix/issue-[number]`
   - Example: `git checkout -b fix/special-chars-login` or `bugfix/issue-142`

3. **Locate Relevant Code**:
   - Use Grep to find potentially affected code based on bug description
   - Identify:
     - Main implementation files
     - Existing test files (if any)
     - Related components that might be impacted
   - Document findings for reference

4. **Implement Bug Fix with TDD**:
   Use Task tool to launch kent-beck-implementer agent:

   ```
   You are tasked with fixing a bug using strict Test-Driven Development.

   **BUG FIX MODE**

   Bug Description:
   <bug>
   [Insert bug description/issue details]
   </bug>

   Affected Code:
   <code>
   [Insert relevant code files]
   </code>

   Existing Tests:
   <tests>
   [Insert existing test files if any]
   </tests>

   TDD Requirements:
   1. **RED Phase**: Write a failing test that reproduces the bug
      - Test must clearly demonstrate the bug
      - Use descriptive test name
      - Include comments explaining the scenario
      - Verify test fails for the right reason

   2. **GREEN Phase**: Implement minimal fix
      - Fix the bug with simplest solution
      - Ensure test now passes
      - Verify no regression in existing tests

   3. **REFACTOR Phase**: Improve if needed
      - Clean up the fix if necessary
      - Add edge case tests
      - Maintain all tests green

   **OUTPUT REQUIREMENTS:**
   1. Save test file FIRST (must fail initially)
   2. Save fix implementation after confirming test fails
   3. Return a bug fix report with:
      - Root cause identified
      - Test file created/updated
      - Fix approach taken
      - Files modified
      - Test results (initially failed, now passing)
   4. DO NOT output code in response
   ```

   **For architectural guidance** (if the bug reveals design issues):
   - Use Task tool to launch bob-martin-architect agent
   - Ask for architectural review of the problem area
   - Get recommendations for preventing similar issues

5. **Process Agent Response**:
   - Receive bug fix report from kent-beck-implementer
   - **DO NOT** read the created files (agent already handled everything)
   - Verify agent confirms test initially failed (RED) then passed (GREEN)
   - Note files modified and test results

6. **Create Fix Commit**:
   - Stage all changes (test + fix) using `git add`
   - Create commit with clear message:
     ```
     fix: [description of what was broken]

     - Added test to reproduce issue
     - [Brief explanation of root cause]
     - [Brief explanation of fix]

     Fixes #[issue-number] (if applicable)
     ```

7. **Provide Summary**:
   - Confirm branch creation and current branch
   - Show test file location and test name
   - Confirm test initially failed (RED)
   - Show files modified for the fix
   - Confirm test now passes (GREEN)
   - Remind about next steps (`/commit` for additional commits, `/merge` when complete)

## Important Principles

### TDD Discipline
- **Never skip the failing test**: The test must fail first to prove it catches the bug
- **Minimal fix**: Write just enough code to make the test pass
- **One bug, one test**: Each bug should have at least one specific test

### Test Quality
- Test should be:
  - **Specific**: Targets the exact bug scenario
  - **Isolated**: Doesn't depend on other tests
  - **Fast**: Runs quickly for rapid feedback
  - **Deterministic**: Always produces same result
  - **Descriptive**: Clear test name and assertions

### Branch Naming
- Use `fix/` prefix for general bugs
- Use `bugfix/issue-[number]` for tracked issues
- Keep names short but descriptive (max 30 chars)

### Commit Strategy
- First commit: Failing test that reproduces the bug
- Second commit: The fix implementation
- Or single commit with both test and fix if preferred
- Clear commit messages linking to issues when applicable

## Error Handling
- If no test framework is found, kent-beck-implementer will ask for clarification
- If bug cannot be reproduced, kent-beck-implementer will report and suggest investigation steps
- If fix causes other tests to fail, agent will analyze and report regression risks

## Agent Usage Guidelines

### Kent Beck Implementer (Primary)
The kent-beck-implementer agent handles all bug fix implementation:
- Writing failing tests that reproduce bugs
- Implementing minimal fixes
- Refactoring while keeping tests green
- Ensuring high test coverage
- Following TDD discipline strictly

### Bob Martin Architect (When Needed)
Use bob-martin-architect for architectural guidance when:
1. **Bug reveals design flaws**: The bug indicates architectural problems
2. **SOLID violations**: Fix might violate design principles
3. **Major refactoring needed**: Significant restructuring required
4. **Pattern guidance**: Need advice on design patterns
5. **Technical debt**: Bug is symptom of deeper issues

Example architectural review prompt:
```
The bug fix revealed potential architectural issues:
- Bug: [description]
- Root cause: [what kent-beck-implementer found]
- Current design: [problematic area]

Please review and recommend:
- Architectural improvements to prevent similar bugs
- Design pattern suggestions
- Refactoring strategy for the affected area
```

## Output Format

After the kent-beck-implementer completes the fix:
```
✓ Bug fixed using TDD by Kent Beck

Bug Fix Report:
• Root cause: [Brief description]
• Test added: [test file and name]
• Fix applied: [approach taken]
• Files modified: [list]
• Test status: Failed → Passing
• All regression tests: Passing

Branch: fix/[bug-name]
Ready for commit with /commit
```