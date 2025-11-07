---
allowed-tools: Read, Glob, Task, TodoWrite
argument-hint: <design-doc-or-requirements> [optional: output-folder]
description: Implement a feature from design document or requirements using strict TDD
---

# TDD Implementation from Design

Implement a feature from a design document or requirements specification using Test-Driven Development with Kent Beck's methodology.

## Usage
`/implement-tdd <design-doc-or-requirements> [output-folder]`

Examples:
- `/implement-tdd ./docs/user-auth-design.md`
- `/implement-tdd ./docs/payment-processing.md ./src/payments`
- `/implement-tdd "Simple TODO list with add, remove, and complete operations"`

## Process

1. **Parse Arguments**:
   ```bash
   DESIGN_INPUT="${ARGUMENTS%% *}"
   OUTPUT_FOLDER="${ARGUMENTS#* }"

   # If no second argument, use default
   if [ "$OUTPUT_FOLDER" = "$DESIGN_INPUT" ]; then
       OUTPUT_FOLDER="./src"
   fi
   ```

2. **Read Design/Requirements**:
   - If input contains `.md` or starts with `.` or `/`: Read file using Read tool
   - Otherwise: Use as direct requirements description
   - Extract key implementation requirements

3. **Prepare Implementation Context**:
   - Use Glob to identify existing project structure
   - Determine programming language and test framework
   - Identify naming conventions and patterns

4. **Launch Implementation Expert**:
   Use Task tool to launch kent-beck-implementer agent:

   ```
   You are tasked with implementing the following feature using strict Test-Driven Development.

   **IMPLEMENTATION MODE**

   Design/Requirements:
   <design>
   [Insert design document or requirements here]
   </design>

   Project Context:
   - Output folder: [OUTPUT_FOLDER]
   - Language: [Detected or specified]
   - Test framework: [Detected or specified]
   - Existing patterns: [Any identified patterns]

   Implementation Instructions:
   1. Follow the Red-Green-Refactor cycle strictly
   2. Write failing tests FIRST for each component
   3. Implement minimal code to make tests pass
   4. Refactor to improve quality while keeping tests green
   5. Aim for >80% test coverage
   6. Use descriptive test names that document behavior

   File Organization:
   - Place implementation files in: [OUTPUT_FOLDER]
   - Place test files in: [TEST_FOLDER]
   - Follow project naming conventions

   **OUTPUT REQUIREMENTS:**
   1. Save all files directly using Write tool
   2. Return ONLY an implementation report with:
      - List of files created (with brief description)
      - Test statistics (count and coverage)
      - Key patterns/libraries used
      - Any important decisions or trade-offs
   3. DO NOT output code in your response
   4. Keep report concise (max 15-20 lines)
   ```

5. **Process Agent Response**:
   - Receive implementation report from kent-beck-implementer
   - **DO NOT** read the created files (agent already saved them correctly)
   - Display agent's summary report to user
   - Remind user about next steps (testing, commit, etc.)

## Output Format

The command should display:
```
✓ TDD Implementation completed by Kent Beck

[Agent's Implementation Report]

Files have been created in [OUTPUT_FOLDER]
You can now:
- Run tests with your test command
- Review the implementation
- Make commits with /commit
```

## Important Notes

- **Trust the expert**: Kent Beck agent handles all implementation details
- **No code in output**: Only summaries and reports, never full code listings
- **Context preservation**: Implementation details stay in files, not conversation
- **TDD discipline**: Agent enforces test-first development
- **File-based workflow**: All code goes directly to files

## Error Handling

- If design document not found: Show error and exit
- If no test framework detected: Agent will ask for clarification
- If output folder doesn't exist: Agent will create it
- If implementation fails: Agent will report issues in summary

## Integration with Pipeline

This command fits into the development pipeline:
1. `/create-prd` → Product requirements
2. `/create-domain-model` → Domain modeling
3. `/create-c4-model` → Architecture
4. `/create-design-lean` → Design document
5. **`/implement-tdd`** → Implementation with tests
6. `/commit` → Version control

## Key Principles

- **Tests drive design**: Let tests guide the implementation
- **Small steps**: Implement incrementally with continuous testing
- **Clean summaries**: Reports focus on what was done, not how
- **Expert autonomy**: Trust Kent Beck agent for implementation decisions
- **No context pollution**: Keep conversation focused on progress, not code details