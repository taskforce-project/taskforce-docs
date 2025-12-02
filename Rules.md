# Rules for git repository contributions

## Table of Contents
1. [General Guidelines](#general-guidelines)
2. [Code Quality](#code-quality)
3. [Commit Messages](#commit-messages)
4. [Branching Strategy](#branching-strategy)
5. [Pull Requests](#pull-requests)
6. [Issue Tracking](#issue-tracking)
7. [Security Practices](#security-practices)
8. [Documentation](#documentation)
9. [Testing](#testing)
10. [Continuous Integration/Continuous Deployment (CI/CD)](#continuous-integrationcontinuous-deployment-cicd)

## 1. General Guidelines
- Follow the project's coding standards and style guides.
- Ensure all code is well-documented and maintainable.
- Respect the project's architecture and design patterns.
- Collaborate respectfully and constructively with other contributors.
- Keep the repository organized and clean.

## 2. Code Quality
- Write clean, readable, and maintainable code.
- Follow language-specific best practices and conventions.
- Use meaningful variable and function names.
- Keep functions small and focused on a single responsibility.
- Avoid code duplication (DRY principle).
- Handle errors gracefully and provide meaningful error messages.
- Optimize code for performance without sacrificing readability.
- Remove commented-out code and debug statements before committing.

## 3. Commit Messages

### Conventional Commits with Gitmoji

All commits must follow the **Conventional Commits** specification with a **Gitmoji** prefix for better readability.

#### Format
```
<gitmoji> <type>(<scope>): <subject>

[optional body]

[optional footer(s)]
```

#### Commit Types and Gitmoji

| Gitmoji | Type | Description | Example |
|---------|------|-------------|---------|
| ✨ | `feat` | New feature or functionality | `✨ feat(auth): add OAuth2 authentication` |
| 🐛 | `fix` | Bug fix | `🐛 fix(api): resolve null pointer exception in user service` |
| 📝 | `docs` | Documentation changes | `📝 docs(readme): update installation instructions` |
| 💄 | `style` | Code style/formatting (no logic change) | `💄 style(css): improve button hover effects` |
| ♻️ | `refactor` | Code refactoring (no feature or bug fix) | `♻️ refactor(services): simplify user validation logic` |
| ⚡ | `perf` | Performance improvements | `⚡ perf(db): optimize database query for user search` |
| ✅ | `test` | Adding or updating tests | `✅ test(auth): add unit tests for login service` |
| 🔧 | `build` | Build system or dependencies | `🔧 build(deps): upgrade Spring Boot to 3.2.0` |
| 👷 | `ci` | CI/CD configuration changes | `👷 ci(github): add automated testing workflow` |
| 🔒 | `security` | Security improvements | `🔒 security(api): implement rate limiting` |
| 🚀 | `deploy` | Deployment related changes | `🚀 deploy(prod): configure production environment` |
| ⏪ | `revert` | Revert previous commit | `⏪ revert: revert commit abc1234` |
| 🎨 | `ui` | UI/UX improvements | `🎨 ui(dashboard): redesign user dashboard layout` |

#### Rules for Commit Messages
1. Use the imperative mood ("add" not "added" or "adds")
2. Don't capitalize the first letter of the subject
3. No period (.) at the end of the subject
4. Limit subject line to 72 characters
5. Separate subject from body with a blank line
6. Use the body to explain **what** and **why**, not **how**
7. Reference issues and pull requests in the footer

#### Examples

**Simple commit:**
```
✨ feat(user): add profile picture upload
```

**Commit with body:**
```
🐛 fix(payment): resolve transaction timeout issue

The payment gateway was timing out due to increased response time.
Implemented retry logic with exponential backoff to handle
temporary failures gracefully.

Fixes #123
```

**Breaking change:**
```
♻️ refactor(api): change authentication endpoint structure

BREAKING CHANGE: Auth endpoints moved from /auth/* to /api/v2/auth/*
All clients must update their API calls accordingly.
```

## 4. Branching Strategy

### Main Branches
- **`main`**: Production-ready code. Protected branch.
- **`develop`**: Integration branch for features. Protected branch.

### Supporting Branches
- **Feature branches**: `feature/<issue-number>-<short-description>`
  - Example: `feature/42-user-authentication`
  - Branch from: `develop`
  - Merge back into: `develop`

- **Bugfix branches**: `bugfix/<issue-number>-<short-description>`
  - Example: `bugfix/87-fix-login-error`
  - Branch from: `develop`
  - Merge back into: `develop`

- **Hotfix branches**: `hotfix/<version>-<short-description>`
  - Example: `hotfix/1.2.1-critical-security-patch`
  - Branch from: `main`
  - Merge back into: `main` and `develop`

- **Release branches**: `release/<version>`
  - Example: `release/1.3.0`
  - Branch from: `develop`
  - Merge back into: `main` and `develop`

### Branch Rules
- Never commit directly to `main` or `develop`
- Delete feature/bugfix branches after merging
- Keep branches focused on a single feature or fix
- Regularly sync with the base branch to avoid conflicts
- Use meaningful and descriptive branch names

## 5. Pull Requests

### PR Guidelines
- Create a PR as soon as you start working (draft PR for WIP)
- Link related issues using keywords (Fixes #123, Closes #456)
- Provide a clear and detailed description of changes
- Include screenshots or GIFs for UI changes
- Ensure all CI checks pass before requesting review
- Keep PRs small and focused (< 400 lines of code when possible)
- Respond to review comments promptly and professionally

### PR Template
```markdown
## Description
[Describe what this PR does]

## Type of Change
- [ ] 🐛 Bug fix
- [ ] ✨ New feature
- [ ] ♻️ Refactoring
- [ ] 📝 Documentation update
- [ ] ⚡ Performance improvement

## Related Issues
Fixes #[issue number]

## Changes Made
- [Change 1]
- [Change 2]
- [Change 3]

## Testing
- [ ] Unit tests added/updated
- [ ] Integration tests added/updated
- [ ] Manual testing completed

## Screenshots (if applicable)
[Add screenshots here]

## Checklist
- [ ] Code follows project style guidelines
- [ ] Self-review completed
- [ ] Comments added for complex logic
- [ ] Documentation updated
- [ ] No new warnings generated
- [ ] Tests pass locally
```

### Code Review Process
- At least one approval required before merging
- Address all review comments or explain why changes aren't needed
- Re-request review after making significant changes
- Use "Resolve conversation" only after implementing feedback
- Be respectful and constructive in reviews

## 6. Issue Tracking

### Issue Creation
- Use clear and descriptive titles
- Provide detailed reproduction steps for bugs
- Include environment details (OS, browser, versions)
- Add appropriate labels (bug, enhancement, documentation, etc.)
- Assign to relevant milestone or project board
- Use issue templates when available

### Issue Labels
- **Priority**: `priority:critical`, `priority:high`, `priority:medium`, `priority:low`
- **Type**: `type:bug`, `type:feature`, `type:enhancement`, `type:docs`
- **Status**: `status:in-progress`, `status:blocked`, `status:needs-review`
- **Component**: `component:frontend`, `component:backend`, `component:api`

### Issue Workflow
1. **Open**: Issue created and awaiting triage
2. **Triaged**: Issue reviewed and prioritized
3. **In Progress**: Actively being worked on
4. **In Review**: PR submitted and under review
5. **Closed**: Issue resolved and merged

## 7. Security Practices

### Secure Coding
- Never commit sensitive data (passwords, API keys, tokens)
- Use environment variables for configuration
- Validate and sanitize all user inputs
- Implement proper authentication and authorization
- Use HTTPS for all communications
- Keep dependencies up to date
- Follow OWASP Top 10 guidelines

### Secret Management
- Use `.gitignore` to exclude sensitive files
- Rotate credentials if accidentally committed
- Use secret management tools (HashiCorp Vault, AWS Secrets Manager)
- Never hardcode credentials in source code

### Vulnerability Reporting
- Report security vulnerabilities privately
- Use GitHub Security Advisories for sensitive issues
- Provide detailed information about the vulnerability
- Allow reasonable time for fix before public disclosure

## 8. Documentation

### Code Documentation
- Write clear and concise comments for complex logic
- Use JSDoc/JavaDoc style comments for functions and classes
- Document API endpoints with OpenAPI/Swagger
- Keep comments up to date with code changes
- Explain **why**, not **what** (code should be self-explanatory)

### Project Documentation
- Maintain an up-to-date README.md
- Document setup and installation procedures
- Provide usage examples and tutorials
- Keep architecture diagrams current
- Document API changes in CHANGELOG.md
- Include troubleshooting guides

### Required Documentation Files
- **README.md**: Project overview and quick start
- **CONTRIBUTING.md**: Contribution guidelines
- **CHANGELOG.md**: Version history and changes
- **LICENSE**: Project license information
- **CODE_OF_CONDUCT.md**: Community behavior guidelines

## 9. Testing

### Test Requirements
- Write tests for all new features
- Maintain minimum 80% code coverage
- Include unit, integration, and e2e tests
- Tests must pass before merging
- Mock external dependencies appropriately

### Test Structure
```
├── unit/              # Unit tests
├── integration/       # Integration tests
├── e2e/              # End-to-end tests
└── fixtures/         # Test data and mocks
```

### Testing Best Practices
- Follow AAA pattern (Arrange, Act, Assert)
- Use descriptive test names
- Test edge cases and error conditions
- Keep tests independent and isolated
- Avoid test interdependencies
- Use test coverage tools to identify gaps

### Test Naming Convention
```
test_<functionName>_<scenario>_<expectedResult>
```
Example: `test_userLogin_invalidPassword_returnsError`

## 10. Continuous Integration/Continuous Deployment (CI/CD)

### CI Pipeline
- Automated tests run on every PR
- Code quality checks (linting, formatting)
- Security vulnerability scanning
- Build verification
- Test coverage reporting

### CD Pipeline
- Automated deployment to staging on merge to `develop`
- Manual approval required for production deployment
- Rollback capability for failed deployments
- Environment-specific configuration management

### CI/CD Best Practices
- Keep build times under 10 minutes
- Fail fast on critical errors
- Use caching to speed up builds
- Monitor pipeline success rates
- Maintain separate environments (dev, staging, prod)
- Implement blue-green or canary deployments

### Required Checks Before Merge
- ✅ All tests pass
- ✅ Code coverage meets threshold
- ✅ No linting errors
- ✅ No security vulnerabilities
- ✅ Build succeeds
- ✅ Code review approved
- ✅ Documentation updated

---

## Additional Resources
- [Conventional Commits Specification](https://www.conventionalcommits.org/)
- [Gitmoji Guide](https://gitmoji.dev/)
- [Semantic Versioning](https://semver.org/)
- [Git Flow Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)

## Questions or Suggestions?
If you have questions about these guidelines or suggestions for improvement, please open an issue for discussion.

---
**Last Updated**: December 2, 2025
