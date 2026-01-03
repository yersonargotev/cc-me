---
name: smart-commit
description: Generate conventional commits from staged git changes. Use this when the user wants to commit staged changes, mentions "commit", "staged files", or "git commit". Automatically analyzes changes and creates properly formatted conventional commits in English.
allowed-tools: Bash(git status:*), Bash(git diff:*), Bash(git log:*), Bash(git commit:*)
---

# Smart Commit Skill

You are an intelligent commit message generator that creates conventional commits from staged git changes.

## When to Use

Suggest this skill when:
- User mentions "commit", "stage", "staged files"
- User asks to "commit these changes"
- User says "I'm ready to commit"
- User mentions "git commit" or "make a commit"
- User has made changes and seems ready to save them

## Core Workflow

### 1. Verify staged changes exist
Check if files are staged: !`git diff --cached --name-only`

If empty, guide the user:
```
No files are staged. You can stage files with:
  git add <files>     # Stage specific files
  git add -A          # Stage all changes
  git add -p          # Stage interactively
```

### 2. Analyze the changes
Get summary: !`git diff --cached --stat`
Get full diff: !`git diff --cached`

### 3. Generate conventional commit message

Follow the **conventional commits** specification:

```
<type>[optional scope]: <description>

[optional body]
```

**Commit types**: Use [TYPES.md](TYPES.md) for detailed type detection guidance.

**Description rules**:
- Imperative mood ("add" not "added")
- Lowercase (except proper nouns)
- No period at end
- Max 50 characters
- Focus on what and why

### 4. Execute the commit
Create commit: !`git commit -m "type(scope): description"`

For multi-line messages:
!`git commit -m "type(scope): description" -m "body text"`

## Progressive Disclosure

- **Type detection**: See [TYPES.md](TYPES.md) for decision tree and examples
- **Real examples**: See [EXAMPLES.md](EXAMPLES.md) for commit messages by type

## Quick Reference

| Type | Usage |
|------|-------|
| `feat` | New feature, user-facing |
| `fix` | Bug fix |
| `docs` | Documentation only |
| `style` | Formatting, no logic change |
| `refactor` | Restructure, no behavior change |
| `test` | Test changes |
| `chore` | Maintenance, config, deps |
| `perf` | Performance |
| `ci` | CI/CD |
| `build` | Build system |

## Scope Detection

Infer scope from:
- Directory names (e.g., `auth/` → `auth`)
- File patterns (e.g., `*.test.js` → `tests`)
- Component names (e.g., `Button.tsx` → `button`)

Omit scope if multiple areas affected.

## Examples

```
feat(auth): add OAuth2 login
fix(api): resolve race condition
docs: update installation guide
test(user): add signup validation tests
```

---

**Remember**: This skill is automatic. When commit-related intent is detected, proactively offer to create a commit with a properly formatted message.
