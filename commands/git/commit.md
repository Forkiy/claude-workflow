---
allowed-tools: Bash(git status:*), Bash(git diff:*), Bash(git log:*), Bash(git add:*), Bash(git commit:*)
argument-hint: [optional: custom commit message prefix]
description: Create a git commit following the repository's commit message style
model: haiku
---

Create a git commit for the current changes following these steps:

1. **Analyze the current state**:
- Current git status: !`git status`
- Current git diff (staged and unstaged changes): !`git diff HEAD`
- Current branch: !`git branch --show-current`
- Recent commits: !`git log --oneline -10`

2. **Draft a commit message**:
   - Summarize the nature of changes (new feature, enhancement, bug fix, refactoring, test, docs, etc.)
   - Ensure accuracy ("add" = wholly new, "update" = enhancement, "fix" = bug fix)
   - **Focus on the "why" rather than the "what"**
   - Keep it concise (1-2 sentences)
   - If the user provided `$ARGUMENTS`, use it as a prefix or context for the commit message
   - Follow the style from recent commits
   - Be short. No need to provide all the changes that was made. 

3. **Safety checks**:
   - DO NOT commit files that likely contain secrets (.env, credentials.json, etc.)
   - Warn if sensitive files are being committed

4. **Create the commit**:
   - Add relevant untracked files using `git add`
   - Create commit with message format:
     ```
     <commit message>
     ```
   - Use HEREDOC format for multi-line messages:
     ```bash
     git commit -m "$(cat <<'EOF'
     Your commit message here.
     EOF
     )"
     ```

5. **Verify**:
   - Run `git status` after commit to confirm success

**Important**:
- NEVER commit without analyzing changes first
- NEVER add footer ```
🤖 Generated with [Claude Code](https://claude.com/claude-code)
Co-Authored-By: Claude <noreply@anthropic.com>")
``` 
- DO NOT push to remote (user will do that manually)
- If pre-commit hooks modify files, check if safe to amend or create new commit
