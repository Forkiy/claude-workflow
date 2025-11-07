---
allowed-tools: Read, Glob, Grep, Task, TodoWrite
argument-hint: <file-or-directory> "<refactoring-goals>"
description: Refactor existing code while maintaining all tests using TDD principles
---

# TDD Refactoring

Refactor existing code to improve its quality while maintaining all functionality, using Test-Driven Development principles to ensure safety.

## Usage
`/refactor-tdd <file-or-directory> "<refactoring-goals>"`

Examples:
- `/refactor-tdd ./src/services/UserService.js "Extract validation logic and reduce complexity"`
- `/refactor-tdd ./src/payment "Apply repository pattern and improve testability"`
- `/refactor-tdd ./lib/calculator.py "Remove duplication and improve naming"`

## Process

1. **Parse Arguments**:
   ```bash
   TARGET="${1:-}"
   GOALS="${2:-}"

   if [ -z "$TARGET" ] || [ -z "$GOALS" ]; then
       echo "Usage: /refactor-tdd <file-or-directory> \"<refactoring-goals>\""
       exit 1
   fi
   ```

2. **Analyze Existing Code**:
   - Use Read/Glob to load target files
   - Use Grep to find related test files
   - Identify current patterns and structure
   - Check for existing test coverage

3. **Prepare Refactoring Context**:
   - Map dependencies and imports
   - Identify all test files that verify the code
   - Note any integration points
   - Document current behavior that must be preserved

4. **Launch Refactoring Expert**:
   Use Task tool to launch kent-beck-implementer agent:

   ```
   You are tasked with refactoring existing code using Test-Driven Development principles.

   **REFACTORING MODE**

   Target Code:
   <existing-code>
   [Insert existing code files here]
   </existing-code>

   Existing Tests:
   <existing-tests>
   [Insert existing test files here]
   </existing-tests>

   Refactoring Goals:
   [GOALS]

   Refactoring Requirements:
   1. **Ensure all existing tests pass before starting**
   2. **Add characterization tests** if coverage is insufficient
   3. **Make small, safe refactoring steps**:
      - Each step should keep all tests green
      - Commit points should be clearly identifiable
   4. **Improve without changing behavior** unless explicitly requested
   5. **Add new tests** for any uncovered edge cases discovered

   Refactoring Priorities:
   - Code clarity and readability
   - Reduced complexity and duplication
   - Better separation of concerns
   - Improved testability
   - Consistent naming and structure

   Safety Checks:
   - Run tests after each refactoring step (conceptually)
   - Preserve all public interfaces unless change is requested
   - Maintain backward compatibility
   - Document any necessary API changes

   **OUTPUT REQUIREMENTS:**
   1. Save all refactored files directly using Write tool
   2. Return ONLY a refactoring report with:
      - Files modified (with type of changes)
      - Refactoring patterns applied
      - Tests added or modified
      - Complexity reduction metrics (if applicable)
      - Any risks or breaking changes
   3. DO NOT output code in your response
   4. Keep report focused on improvements made
   ```

5. **Process Agent Response**:
   - Receive refactoring report from kent-beck-implementer
   - **DO NOT** read the refactored files (trust the expert)
   - Display agent's summary of improvements
   - Suggest running tests to verify changes

## Output Format

The command should display:
```
✓ Refactoring completed by Kent Beck

[Agent's Refactoring Report]

Refactoring complete. Please run your test suite to verify all changes.
Suggested commands:
- Run tests: [appropriate test command]
- Review changes: git diff
- Commit if satisfied: /commit "refactor: [description]"
```

## Refactoring Catalog

Common refactoring patterns the agent may apply:
- **Extract Method**: Break large methods into smaller, focused ones
- **Extract Class**: Move cohesive functionality to new classes
- **Inline Method**: Remove unnecessary indirection
- **Rename**: Improve names for clarity
- **Move Method**: Relocate methods to more appropriate classes
- **Replace Conditional with Polymorphism**: Use OO instead of if/switch
- **Introduce Parameter Object**: Group related parameters
- **Remove Duplication**: Extract common code to shared methods

## Important Notes

- **Tests as safety net**: Never refactor without tests
- **Incremental changes**: Small steps maintain safety
- **Behavior preservation**: Refactoring doesn't change what code does
- **Trust the expert**: Kent Beck handles the details
- **Clean reports**: Focus on what improved, not implementation details

## Error Handling

- If no tests exist: Agent will create characterization tests first
- If tests fail initially: Agent will report and stop
- If refactoring breaks tests: Agent will revert and report
- If goals are unclear: Agent will ask for clarification

## TDD Refactoring Principles

The agent follows these TDD refactoring principles:
1. **Green before refactoring**: All tests must pass initially
2. **Stay green**: Never leave tests failing during refactoring
3. **Test additions**: Add tests for uncovered behavior found
4. **Small steps**: Each change should be reversible
5. **Continuous validation**: Conceptually run tests after each change

## Integration with Other Commands

Works well with:
- `/fix-bug` - Refactor after bug fixes
- `/implement-feature` - Clean up after initial implementation
- `/code-review` - Address issues found in review
- `/architecture-audit` - Implement recommended improvements

## Advanced Usage

For complex refactoring across multiple modules:
```bash
# Refactor an entire subsystem
/arch-toolkit:dev:refactor-tdd ./src/auth "Implement clean architecture with ports and adapters"

# Prepare for new features
/arch-toolkit:dev:refactor-tdd ./src/payment "Extract interfaces for payment provider abstraction"

# Improve testability
/arch-toolkit:dev:refactor-tdd ./src/services "Remove tight coupling and add dependency injection"
```

## Key Benefits

- **Safe refactoring**: Tests ensure nothing breaks
- **Incremental improvement**: Code gets better step by step
- **Expert guidance**: Kent Beck's experience guides decisions
- **Clean context**: No code pollution in conversation
- **Documented changes**: Clear report of what was improved