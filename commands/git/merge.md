---
allowed-tools: Read, Glob, Bash(git:*)
description: Squash all branch changes and merge into main with comprehensive commit message
project: true
gitignored: true
model: haiku
---

Squash all changes in the current branch and merge into main/master with a comprehensive commit message.

**PROCESS:**

1. First, analyze the current branch to understand all changes:
   - Uncommitted changes: 
      !`git status`
   - All commits in the branch:
      !`git log --oneline main..HEAD`
   - All file changes summary:
      !`git diff main...HEAD --stat`

2. If there are uncommitted changes:
   - Stage and commit them using `/commit` command

3. Determine the base branch (main or master):
   - Main ref: !`git show-ref --verify --quiet refs/heads/main`
   - If not, use 'master'

4. Create a comprehensive squash commit message that includes:
   - **Title**: Clear, concise summary of what was accomplished
   - **Summary**: 2-3 paragraphs explaining the changes
   - **Key Changes**: Bulleted list of major modifications
   - **Technical Details**: Any important implementation notes
   - **Breaking Changes**: If any (marked clearly)
   - **Related Issues**: If applicable

5. Perform the squash and merge:
   ```bash
   # Ensure we're up to date with the base branch
   git fetch origin
   git checkout [base-branch]
   git pull origin [base-branch]

   # Merge with squash
   git merge --squash [feature-branch]

   # Commit with comprehensive message
   git commit -m "[comprehensive message]"
   ```

6. After successful merge:
   - Show the final commit with `git show HEAD`
   - Optionally delete the feature branch if requested
   - Provide summary of what was merged
   - Delete branch after merge

**COMMIT MESSAGE TEMPLATE:**
```
[Component/Feature]: Brief description of what and why was done

## Summary
[2-3 paragraphs explaining the context, problem solved, and approach taken]

## Key Changes
- [Major change what and why 1]
- [Major change what and why 2]
- [Major change what and why 3]
...

## Technical Details
- [Implementation note 1]
- [Implementation note 2]
...

[If applicable:]
## Breaking Changes
⚠️ [Description of breaking changes]
```

**Important**:
- NEVER add footer ```
🤖 Generated with [Claude Code](https://claude.com/claude-code)
Co-Authored-By: Claude <noreply@anthropic.com>")
``` 
- DO NOT push to remote (user will do that manually)
- If pre-commit hooks modify files, check if safe to amend or create new commit

**OPTIONS:**
- Branch name: {{branch:-"current branch"}}
- Push after merge: {{push:-"no"}}

**SAFETY CHECKS:**
- Confirm before merging if there are conflicts
- Warn if merging directly to main/master without PR
- Ensure no uncommitted changes are lost

**NOTE:** This command is best used for feature branches that are ready to be integrated into the main branch. For work-in-progress or experimental changes, consider using a pull request instead.