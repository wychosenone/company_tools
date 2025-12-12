---
name: pr-template
description: PR description generator. Use when users need to write a pull request description, PR summary, or merge request description. Generates standardized, comprehensive PR descriptions.
---

# PR Template Generator

## Overview

You help developers create clear, comprehensive pull request descriptions that follow team standards.

## When to Use

Trigger this skill when users ask to:
- Write a PR description
- Create a pull request summary
- Generate MR (merge request) description
- Summarize changes for review

## IMPORTANT: Gather Information Automatically

**Before generating the PR description, you MUST run these commands to understand the changes:**

### Step 1: Get Git Information

Run these commands using the Bash tool:

```bash
# See what files changed
git status

# See the actual code changes (staged and unstaged)
git diff HEAD

# See commit history on this branch (if already committed)
git log --oneline -10

# See what branch we're on and how it differs from main
git log main..HEAD --oneline
```

### Step 2: Read Modified Files (if needed)

If the diff is large or complex, read the full files to understand context:

```bash
# List the changed files
git diff --name-only HEAD
```

Then use the Read tool to examine key files.

### Step 3: Look for Related Issues

Check for issue/ticket references in:
- Commit messages
- Branch name (e.g., `feature/JIRA-1234-login-fix`)
- Comments in the code

## Information Sources Summary

| Source | How to Get | What It Provides |
|--------|------------|------------------|
| `git diff` | Bash tool | Actual code changes |
| `git log` | Bash tool | Commit messages, history |
| `git status` | Bash tool | Changed files list |
| Branch name | Bash tool | Often contains ticket number |
| User input | Ask if unclear | Context, motivation, test steps |

## Output Format

Generate PR descriptions in this format:

```markdown
## Summary
[1-2 sentence overview based on the actual changes you read]

## Changes
- [Specific change 1 from git diff]
- [Specific change 2 from git diff]
- [Specific change 3 from git diff]

## Why
[Explanation based on commit messages or ask user if unclear]

## Testing
- [ ] Unit tests added/updated
- [ ] Manual testing performed
- Steps to test:
  1. [Specific step based on the changes]
  2. [...]

## Files Changed
[List from git status]

## Checklist
- [ ] Code follows project style guidelines
- [ ] Self-review completed
- [ ] Documentation updated (if needed)
- [ ] No new warnings introduced

## Breaking Changes
[Analyze from diff - any API changes, removed functions, etc.]

## Related Issues
[Extract from branch name or commit messages]
```

## Example Workflow

**User says:** "Write a PR description for me"

**You do:**

1. Run `git status` - see `src/auth/login.js` modified
2. Run `git diff HEAD` - see email validation regex changed
3. Run `git log -3 --oneline` - see commit "fix: allow plus signs in email"
4. Check branch name - `fix/JIRA-1234-email-validation`

**Then generate:**

```markdown
## Summary
Fixed email validation to allow plus signs in email addresses during login.

## Changes
- Updated email regex in `src/auth/login.js` line 45
- Changed pattern from `/^[a-zA-Z0-9]+@/` to `/^[a-zA-Z0-9+.]+@/`
- Added handling for dots in local part

## Why
Users with emails like `user+tag@example.com` were unable to log in.

## Testing
- [ ] Unit tests added/updated
- [ ] Manual testing performed
- Steps to test:
  1. Go to login page
  2. Enter email: `test+filter@example.com`
  3. Should successfully validate and proceed

## Files Changed
- `src/auth/login.js`

## Breaking Changes
None - backwards compatible regex change

## Related Issues
Closes JIRA-1234
```

## When Information is Missing

If you cannot determine something from git:
1. **Ask the user** specific questions
2. Mark sections as `[TODO: need input]`
3. Do not make up information

Example:
```markdown
## Testing
[TODO: Please describe how to test this change]
```

---

## Tips

1. **Always read the diff first** - Do not ask user for info you can get from git
2. **Be specific** - Reference actual file names and line numbers
3. **Detect patterns** - Branch names often contain ticket numbers
4. **Ask only what is missing** - Do not ask user to repeat what is in the code
