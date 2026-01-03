# Commit Type Detection Guide

This guide helps determine the correct conventional commit type based on staged changes.

## Type Decision Tree

```
Start
  │
  ├─ Only documentation changed?
  │   └─ YES → docs
  │
  ├─ Tests changed but no production code?
  │   └─ YES → test
  │
  ├─ CI/CD configuration changed?
  │   └─ YES → ci
  │
  ├─ Build system/dependencies changed?
  │   └─ YES → build
  │
  ├─ Only formatting/style, no logic change?
  │   └─ YES → style
  │
  ├─ Performance improvement only?
  │   └─ YES → perf
  │
  ├─ Code restructured without behavior change?
  │   └─ YES → refactor
  │
  ├─ Fixing a bug or error?
  │   └─ YES → fix
  │
  ├─ New feature or user-facing functionality?
  │   └─ YES → feat
  │
  └─ None of the above?
      └─ chore
```

## Type Details

### feat - New Feature
**Use when**: Adding new functionality that affects user-facing behavior.

**Indicators**:
- New functions, classes, modules
- New API endpoints
- New UI components
- New features in existing code
- Feature flags being enabled

**Examples**:
```
feat: add dark mode toggle
feat(auth): implement OAuth2 login
feat(api): add user profile endpoint
feat(ui): add notification system
```

**NOT for**:
- Bug fixes (use `fix`)
- Refactoring (use `refactor`)
- Tests (use `test`)

---

### fix - Bug Fix
**Use when**: Fixing a bug, error, or unexpected behavior.

**Indicators**:
- Words like "fix", "bug", "error", "issue" in commit
- Correcting incorrect behavior
- Handling edge cases
- Fixing crashes or exceptions
- Resolving reported issues

**Examples**:
```
fix: resolve memory leak in image processing
fix(auth): correct token expiration check
fix(ui): prevent button double-click
fix(api): handle null response from database
```

**NOT for**:
- New features (use `feat`)
- Refactoring that doesn't fix bugs (use `refactor`)

---

### docs - Documentation
**Use when**: ONLY documentation files are changed.

**Indicators**:
- All changed files are in `docs/`, `README`, `*.md`
- Comments in code (if ONLY comments changed)
- API documentation
- User guides

**Examples**:
```
docs: update installation instructions
docs(api): document authentication endpoints
docs: add troubleshooting section
docs: clarify license information
```

**NOT for**:
- Code changes with documentation (use primary type)
- Code comments with other changes (use primary type)

---

### style - Style Changes
**Use when**: ONLY formatting/style changes, NO logic/behavior change.

**Indicators**:
- Whitespace changes
- Indentation fixes
- Semicolon additions
- Code formatting (prettier, eslint --fix)
- Renaming variables (no logic change)

**Examples**:
```
style: format code with prettier
style(ui): standardize indentation
style: remove trailing whitespace
style: convert tabs to spaces
```

**NOT for**:
- Logic changes (use appropriate type)
- Refactoring that changes behavior (use `refactor`)

---

### refactor - Code Restructuring
**Use when**: Code structure changes but behavior remains the same.

**Indicators**:
- Extracting functions/classes
- Reorganizing code structure
- Removing dead code
- Simplifying code
- Design pattern implementation

**Examples**:
```
refactor(auth): extract validation to separate module
refactor: simplify data flow
refactor(api): consolidate error handling
refactor: replace callbacks with promises
```

**NOT for**:
- New features (use `feat`)
- Bug fixes (use `fix`)
- Style-only changes (use `style`)

---

### test - Test Changes
**Use when**: Adding or modifying tests.

**Indicators**:
- `*.test.*`, `*.spec.*` files changed
- Test framework updates
- Test fixtures/mocks
- Test utilities

**If ONLY tests changed**: use `test`
**If tests + code changed**: use code's type (e.g., `feat`, `fix`)

**Examples**:
```
test: add unit tests for user service
test(auth): add integration tests
test: increase coverage for payment module
test: fix flaky e2e tests
```

**NOT for**:
- Production code changes (use appropriate type)

---

### chore - Maintenance
**Use when**: Routine tasks that don't fit other categories.

**Indicators**:
- Dependency updates (non-breaking)
- Configuration changes
- Build tool updates
- Package manager changes
- Maintenance scripts

**Examples**:
```
chore: update dependencies
chore: upgrade to Node.js 20
chore: add .editorconfig
chore: update eslint configuration
```

---

### perf - Performance
**Use when**: Improving performance without changing behavior.

**Indicators**:
- Optimization keywords
- Caching changes
- Algorithm improvements
- Resource usage reduction
- Load time improvements

**Examples**:
```
perf(api): add response caching
perf: optimize database queries
perf(ui): lazy load images
perf: reduce bundle size by 30%
```

---

### ci - CI/CD
**Use when**: Changing CI/CD configuration.

**Indicators**:
- GitHub Actions, GitLab CI, Jenkins files
- Workflow changes
- Pipeline updates
- Deployment configuration

**Examples**:
```
ci: add automated testing workflow
ci: update node version in actions
ci: configure artifact caching
ci: add staging deployment
```

---

### build - Build System
**Use when**: Changing build configuration or dependencies.

**Indicators**:
- `package.json`, `pom.xml`, `build.gradle`
- Webpack, Vite, Rollup config
- Build scripts
- Compilation changes

**Examples**:
```
build: upgrade webpack to v5
build: configure tree shaking
build: add TypeScript support
build: minify production bundle
```

---

## Multiple Types

When changes span multiple types:
1. Choose the **primary type** (most significant change)
2. If truly mixed, consider splitting into multiple commits
3. Default to `chore` if genuinely mixed

## Breaking Changes

For breaking changes, add an exclamation mark:
```
feat!: redesign authentication flow
fix(api)!: remove deprecated endpoints
```

And add `BREAKING CHANGE:` footer:
```
feat!: redesign authentication flow

BREAKING CHANGE: OAuth tokens now expire in 24 hours
instead of 30 days. Clients must be updated to handle
refresh tokens.
```
