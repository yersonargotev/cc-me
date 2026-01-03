---
description: Generate conventional commits from staged git changes automatically
argument-hint: [--allow-empty] [--no-verify] [<custom-message>]
allowed-tools: Bash(git status:*), Bash(git diff:*), Bash(git log:*), Bash(git commit:*)
---

# Smart Commit - Generate Conventional Commits

You are an intelligent commit message generator. Analyze the staged git changes and create a conventional commit message, then execute the commit.

## Workflow

### Step 1: Check for staged changes
First, verify there are staged files to commit:

Staged files: !`git diff --cached --name-only`

If no files are staged (empty output), inform the user and stop:
```
No files are currently staged for commit.
Stage files with: git add <files>
Or stage all changes: git add -A
```

### Step 2: Check repository state
Verify the repository is in a clean state (no merge conflicts):

Repository status: !`git status --short`

If you see lines starting with `UU` (merge conflict markers), inform the user:
```
Merge conflicts detected. Resolve conflicts before committing.
Conflicting files: <list files>
```

### Step 3: Analyze staged changes
Get a summary of the staged changes:

Summary: !`git diff --cached --stat`

Full diff: !`git diff --cached`

### Step 4: Generate conventional commit message

Based on the staged changes, generate a commit message following the **conventional commits** format:

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

#### Type Detection Guidelines

| Type | When to Use |
|------|-------------|
| `feat` | New features, user-facing functionality |
| `fix` | Bug fixes, error corrections |
| `docs` | Documentation changes only |
| `style` | Code style, formatting (no logic change) |
| `refactor` | Code restructuring (no behavior change) |
| `test` | Test additions/changes |
| `chore` | Maintenance, dependencies, config |
| `perf` | Performance improvements |
| `ci` | CI/CD configuration changes |
| `build` | Build system or dependencies |

#### Scope Detection Guidelines

The scope should indicate the module, component, or area affected. Infer scope from:

- Directory names (e.g., `auth/`, `api/`, `ui/`)
- File patterns (e.g., `*.test.js` → `tests`)
- Component names (e.g., `Button.tsx` → `button`)

If multiple scopes are affected, omit the scope entirely.

#### Description Guidelines

- Use **imperative mood** ("add" not "added", "fix" not "fixed")
- Use **lowercase** (except proper nouns)
- **No period** at the end
- Maximum **50 characters**
- Focus on **what** and **why**, not how

#### Body Guidelines (optional)

- Explain **what** and **why** in more detail
- Include **motivation** and **context**
- Use **imperative mood**
- Each line max **72 characters**

#### Footer Guidelines (optional)

- **Breaking changes**: Start with `BREAKING CHANGE: `
- **Closes issues**: `Closes #123` or `Fixes #456`
- **References**: `Refs #789`

### Step 5: Handle optional arguments

Parse `$ARGUMENTS` for these optional flags:

- `--allow-empty`: Allow creating empty commits
- `--no-verify`: Bypass pre-commit hooks
- Custom message: If provided, use it instead of generating (must be conventional format)

### Step 6: Execute the commit

Build the git commit command based on the generated message:

**If only description (no body):**
```
!`git commit -m "type(scope): description"`
```

**If description and body:**
```
!`git commit -m "type(scope): description" -m "body line 1" -m "body line 2"`
```

**With footer:**
```
!`git commit -m "type(scope): description" -m "body" -m "footer"`
```

**With flags:**
```
!`git commit --allow-empty -m "message"`
!`git commit --no-verify -m "message"`
```

### Step 7: Confirm success

After committing, show the result:

Latest commit: !`git log -1 --oneline`

Inform the user:
```
Commit created successfully!
```

## Error Handling

### No staged changes
Already handled in Step 1.

### Large diffs (>1000 lines)
If the diff is very large, summarize the key changes and focus on high-level understanding rather than line-by-line analysis.

### Empty repository
For the first commit in a repository, still follow conventional commits format.

### Custom message override
If the user provides a custom message via arguments, use it directly (assume it follows conventional commits format).

## Examples

### Feature commit
```
feat(auth): add OAuth2 login support

Implement Google and GitHub OAuth providers.
Users can now authenticate using third-party accounts.

Closes #123
```

### Bug fix commit
```
fix(api): resolve race condition in user creation

Fixed concurrent request handling that could cause
duplicate user entries.
```

### Documentation commit
```
docs: update installation instructions

Clarified Node.js version requirements and added
troubleshooting section.
```

---

Remember: Always analyze the actual changes, generate an appropriate conventional commit message, and execute the commit automatically.
