# Conventional Commit Examples

Real-world examples of well-formatted conventional commits organized by type.

## feat (Features)

```
feat: add dark mode toggle

Implement theme switching between light and dark modes.
Theme preference is persisted in localStorage.

Closes #42
```

```
feat(auth): implement OAuth2 login

Add support for Google and GitHub OAuth providers.
Users can now authenticate using third-party accounts.

BREAKING CHANGE: Session token format changed. Existing
sessions will be invalidated.
```

```
feat(api): add user profile endpoint

Introduce GET /api/users/:id for fetching user profiles.
Includes email, name, and avatar fields.
```

```
feat(ui): add notification system

Implement toast notifications for user feedback.
Supports success, error, warning, and info variants.
```

```
feat(search): add fuzzy search capability

Implement fuzzy matching for search queries.
Improves result relevance for misspelled terms.
```

---

## fix (Bug Fixes)

```
fix: resolve memory leak in image processing

Fix improper cleanup of image buffers causing memory
accumulation over time.

Fixes #156
```

```
fix(auth): correct token expiration check

Fix off-by-one error in token validation that caused
premature session expiration.
```

```
fix(ui): prevent button double-click

Add debounce to button click handlers to prevent
duplicate form submissions.
```

```
fix(api): handle null response from database

Add null check for database queries that may return
empty results. Prevents 500 errors.
```

```
fix(payment): resolve currency conversion bug

Fix incorrect exchange rate calculation for multi-
currency transactions.
```

---

## docs (Documentation)

```
docs: update installation instructions

Clarify Node.js version requirements and add
troubleshooting section for common setup issues.
```

```
docs(api): document authentication endpoints

Add comprehensive API documentation for OAuth flows,
including request/response examples.
```

```
docs: add contributing guidelines

Create contribution guide with coding standards,
commit message conventions, and PR process.
```

```
docs: clarify license information

Update LICENSE file and add README section on
commercial usage rights.
```

---

## style (Style Changes)

```
style: format code with prettier

Apply consistent code formatting across codebase.
Run prettier with standard configuration.
```

```
style(ui): standardize indentation

Convert mixed tabs/spaces to consistent 2-space
indentation in UI components.
```

```
style: remove trailing whitespace

Clean up trailing whitespace from all source files.
```

```
style: organize imports alphabetically

Sort imports in all files for better consistency
and readability.
```

---

## refactor (Code Restructuring)

```
refactor(auth): extract validation to separate module

Move authentication validation logic to dedicated
validator module for reusability.
```

```
refactor: simplify data flow

Remove unnecessary data transformation layers.
Direct pass-through improves performance.
```

```
refactor(api): consolidate error handling

Centralize error handling in middleware. Removes
duplicate try-catch blocks across endpoints.
```

```
refactor: replace callbacks with promises

Modernize async code by converting callback patterns
to async/await. Improves readability.
```

```
refactor(db): extract repository pattern

Implement repository layer for database operations.
Separates business logic from data access.
```

---

## test (Tests)

```
test: add unit tests for user service

Achieve 80% coverage for user CRUD operations.
Include edge case tests for invalid inputs.
```

```
test(auth): add integration tests

Test complete authentication flow including login,
logout, and token refresh scenarios.
```

```
test: increase coverage for payment module

Add tests for refund and chargeback scenarios.
Coverage now at 95%.
```

```
test: fix flaky e2e tests

Stabilize timing-dependent tests by adding proper
waits and assertions.
```

```
test(api): add performance benchmarks

Add automated performance tests for API endpoints.
Alerts if response time exceeds threshold.
```

---

## chore (Maintenance)

```
chore: update dependencies

Update all packages to latest stable versions.
Includes security patches for lodash and eslint.
```

```
chore: upgrade to Node.js 20

Update minimum Node.js version to 20.10. Drop support
for Node.js 16 (end of life).
```

```
chore: add .editorconfig

Standardize editor configuration across team.
Enforces consistent indentation and line endings.
```

```
chore: update eslint configuration

Add new rules for TypeScript strict mode. Configure
import sorting and unused variable detection.
```

---

## perf (Performance)

```
perf(api): add response caching

Implement Redis caching for frequently accessed data.
Reduces database load by 60%.
```

```
perf: optimize database queries

Add proper indexes and use query optimization.
Improves response time by 300ms on average.
```

```
perf(ui): lazy load images

Implement intersection observer for image lazy loading.
Reduces initial page load by 40%.
```

```
perf: reduce bundle size

Configure tree shaking and remove unused dependencies.
Bundle size reduced from 450KB to 280KB.
```

---

## ci (CI/CD)

```
ci: add automated testing workflow

Configure GitHub Actions to run tests on every push.
Includes linting, unit tests, and e2e tests.
```

```
ci: update node version in actions

Update CI to use Node.js 20.10 across all workflows.
```

```
ci: configure artifact caching

Add caching for node_modules and build artifacts.
Reduces workflow duration by 45%.
```

```
ci: add staging deployment

Configure automatic deployment to staging environment
on merge to main branch.
```

---

## build (Build System)

```
build: upgrade webpack to v5

Migrate from webpack 4 to webpack 5.
Update configuration and plugins for compatibility.
```

```
build: configure tree shaking

Enable tree shaking to remove unused code.
Requires proper ES module exports.
```

```
build: add TypeScript support

Configure TypeScript compiler and type checking.
Generate type definitions for package consumers.
```

```
build: minify production bundle

Add terser plugin for code minification.
Enable gzip compression for assets.
```

---

## Multi-line Examples

```
feat(email): add template system

Implement email template engine with support for
variables and conditional blocks. Templates are
stored in database for dynamic updates.

- Add template editor UI
- Implement variable substitution
- Add template versioning

Closes #89
Refs #73
```

```
fix(api): resolve race condition in user creation

Fix concurrent request handling that could cause
duplicate user entries. Add unique constraint on
email field and proper error handling.

This issue occurred when multiple requests created
users with the same email simultaneously.

Fixes #234
```

---

## Breaking Changes

```
feat!: redesign authentication flow

OAuth tokens now expire in 24 hours instead of 30 days.
Clients must implement refresh token handling.

BREAKING CHANGE: Token expiration reduced from 30 days
to 24 hours for improved security. All clients must
update to handle token refresh flow.
```

```
fix(api)!: remove deprecated endpoints

Remove /api/v1/users/* endpoints that were deprecated
in version 2.0. Migrate to /api/v2/users/*.

BREAKING CHANGE: Version 1 API endpoints removed.
Update API clients to use version 2 endpoints.
```

---

## Small/Simple Examples

```
feat: add copy button
fix: prevent scroll on overlay
docs: update readme
style: format json
refactor: simplify validator
test: add auth tests
chore: bump version
perf: cache responses
ci: fix workflow
build: update config
```
