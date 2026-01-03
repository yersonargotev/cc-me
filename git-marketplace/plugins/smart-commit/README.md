# Smart Commit Plugin

Generate conventional commits from staged git changes using AI analysis.

## Features

- **Automatic commit message generation** based on staged changes
- **Conventional commits format** with proper type detection
- **Dual invocation**: Slash command or automatic skill suggestion
- **Smart type detection**: feat, fix, docs, style, refactor, test, chore, perf, ci, build
- **Scope inference**: Automatically determines affected module/component
- **Fully automatic**: Analyzes changes and creates commit in one step
- **English messages**: All commit messages in English

## Installation

### Add Marketplace

```bash
/plugin marketplace add /path/to/git-marketplace
```

### Install Plugin

```bash
/plugin install smart-commit@git-marketplace
```

## Usage

### Slash Command

Execute the commit command when you have staged changes:

```bash
/commit-staged
```

### Optional Arguments

```bash
# Allow empty commits
/commit-staged --allow-empty

# Bypass pre-commit hooks
/commit-staged --no-verify

# Use custom message
/commit-staged feat: my custom message
```

### Agent Skill

The `smart-commit` skill will be automatically suggested when:
- You mention "commit", "stage", or "staged files"
- You ask to "commit these changes"
- You say "I'm ready to commit"

Simply acknowledge the suggestion and the skill will analyze your staged changes and create an appropriate commit message.

## How It Works

1. **Detects staged changes** using `git diff --cached`
2. **Analyzes the diff** to understand what changed
3. **Determines commit type** based on the nature of changes
4. **Infers scope** from affected directories/components
5. **Generates description** using imperative mood
6. **Creates the commit** automatically with proper formatting

## Commit Message Format

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

### Example Output

```
feat(auth): add OAuth2 login support

Implement Google and GitHub OAuth providers.
Users can now authenticate using third-party accounts.

Closes #123
```

## Commit Types

| Type | Description |
|------|-------------|
| `feat` | New feature, user-facing functionality |
| `fix` | Bug fix, error correction |
| `docs` | Documentation changes only |
| `style` | Code style, formatting (no logic change) |
| `refactor` | Code restructuring (no behavior change) |
| `test` | Test additions/changes |
| `chore` | Maintenance, dependencies, config |
| `perf` | Performance improvements |
| `ci` | CI/CD configuration changes |
| `build` | Build system or dependencies |

See [TYPES.md](skills/smart-commit/TYPES.md) for detailed type detection guidelines.

## Requirements

- Git repository initialized
- At least one staged file
- No merge conflicts

## Error Handling

The plugin handles common scenarios:

- **No staged changes**: Prompts to stage files with `git add`
- **Merge conflicts**: Detects and informs about conflicts
- **Large diffs**: Summarizes key changes for analysis
- **Empty repository**: Works for first commit

## Examples

### Feature Commit

```bash
# Stage your changes
git add auth/oauth.ts

# Run the command
/commit-staged

# Output:
feat(auth): add OAuth2 login support
```

### Bug Fix Commit

```bash
# Stage bug fix
git add api/user.ts

# Run the command
/commit-staged

# Output:
fix(api): resolve race condition in user creation
```

### Documentation Commit

```bash
# Stage docs
git add README.md

# Run the command
/commit-staged

# Output:
docs: update installation instructions
```

## File Structure

```
smart-commit/
├── .claude-plugin/
│   └── plugin.json          # Plugin manifest
├── commands/
│   └── commit-staged.md     # Slash command
├── skills/
│   └── smart-commit/
│       ├── SKILL.md         # Agent skill
│       ├── TYPES.md         # Type detection guide
│       └── EXAMPLES.md      # Commit examples
└── README.md                # This file
```

## Development

### Local Testing

```bash
# Test the plugin locally
claude --plugin-dir ./git-marketplace/plugins/smart-commit

# Validate plugin
claude plugin validate ./git-marketplace/plugins/smart-commit
```

## License

MIT

## Contributing

Contributions welcome! Please feel free to submit a Pull Request.
