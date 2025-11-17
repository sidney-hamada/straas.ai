# CLAUDE.md - AI Assistant Guide for straas.ai

**Last Updated**: 2025-11-17
**Repository**: straas.ai
**Status**: Initial Setup Phase

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Repository Structure](#repository-structure)
3. [Development Workflow](#development-workflow)
4. [Coding Conventions](#coding-conventions)
5. [Git Practices](#git-practices)
6. [Testing Guidelines](#testing-guidelines)
7. [Documentation Standards](#documentation-standards)
8. [AI Assistant Guidelines](#ai-assistant-guidelines)
9. [Common Tasks](#common-tasks)

---

## Project Overview

### About straas.ai

This repository contains the straas.ai project. As this is a newly initialized repository, the specific technical stack and architecture will be established as the project develops.

### Current State

- **Status**: Newly initialized repository
- **Branch**: `claude/claude-md-mi33gkqc4cf4enfk-01CGuoXUWKdgdC394Ba97DRB`
- **Phase**: Initial setup and scaffolding

---

## Repository Structure

### Expected Directory Layout

Once initialized, the repository should follow this organizational structure:

```
straas.ai/
├── .git/                    # Git repository data
├── .github/                 # GitHub-specific files
│   └── workflows/           # CI/CD workflows
├── src/                     # Source code
│   ├── components/          # Reusable components
│   ├── services/            # Business logic and services
│   ├── utils/               # Utility functions
│   ├── types/               # Type definitions
│   ├── config/              # Configuration files
│   └── index.ts             # Main entry point
├── tests/                   # Test files
│   ├── unit/                # Unit tests
│   ├── integration/         # Integration tests
│   └── e2e/                 # End-to-end tests
├── docs/                    # Documentation
├── scripts/                 # Build and utility scripts
├── public/                  # Static assets (if applicable)
├── .gitignore               # Git ignore rules
├── package.json             # Dependencies and scripts
├── tsconfig.json            # TypeScript configuration
├── README.md                # Project readme
└── CLAUDE.md                # This file
```

### Key Directories

- **`src/`**: All source code goes here. Organize by feature or layer.
- **`tests/`**: Mirror the `src/` structure for easy test discovery.
- **`docs/`**: Markdown documentation, architecture diagrams, and guides.
- **`scripts/`**: Build, deployment, and maintenance scripts.

---

## Development Workflow

### Branch Strategy

This project uses a feature branch workflow:

1. **Main Branch**: `main` or `master` (production-ready code)
2. **Feature Branches**: `claude/claude-md-*` or `feature/*` for new features
3. **Bug Fix Branches**: `fix/*` for bug fixes
4. **Release Branches**: `release/*` for preparing releases

### Standard Development Process

1. **Create a branch** from the main branch
2. **Implement changes** with regular commits
3. **Write tests** for new functionality
4. **Update documentation** as needed
5. **Run tests and linting** before committing
6. **Push to remote** using `git push -u origin <branch-name>`
7. **Create a pull request** for review
8. **Address feedback** and merge when approved

### Environment Setup

```bash
# Install dependencies
npm install

# Run development server
npm run dev

# Run tests
npm test

# Run linting
npm run lint

# Build for production
npm run build
```

---

## Coding Conventions

### General Principles

1. **Clarity over cleverness**: Write code that is easy to understand
2. **Consistency**: Follow existing patterns in the codebase
3. **Documentation**: Comment complex logic and public APIs
4. **Type safety**: Use TypeScript strictly, avoid `any` types
5. **Error handling**: Always handle errors explicitly

### Naming Conventions

```typescript
// Files: kebab-case
user-service.ts
api-client.ts

// Classes: PascalCase
class UserService {}
class ApiClient {}

// Functions: camelCase
function getUserById() {}
function fetchData() {}

// Constants: UPPER_SNAKE_CASE
const MAX_RETRIES = 3;
const API_BASE_URL = 'https://api.straas.ai';

// Interfaces: PascalCase with 'I' prefix (optional)
interface User {}
interface IApiResponse {}

// Types: PascalCase
type UserId = string;
type ApiResponse<T> = { data: T };
```

### Code Style

```typescript
// Use const by default, let when necessary, never var
const user = { id: 1, name: 'Alice' };
let counter = 0;

// Prefer arrow functions for callbacks
array.map(item => item.id);
array.filter(item => item.active);

// Use template literals for string interpolation
const message = `User ${user.name} has ID ${user.id}`;

// Destructure when appropriate
const { id, name } = user;
const [first, ...rest] = items;

// Use async/await over raw promises
async function fetchUser(id: string) {
  try {
    const response = await api.get(`/users/${id}`);
    return response.data;
  } catch (error) {
    console.error('Failed to fetch user:', error);
    throw error;
  }
}
```

### TypeScript Best Practices

```typescript
// Define explicit types for function parameters and returns
function calculateTotal(items: Item[]): number {
  return items.reduce((sum, item) => sum + item.price, 0);
}

// Use interfaces for object shapes
interface User {
  id: string;
  name: string;
  email: string;
  createdAt: Date;
}

// Use type aliases for unions and complex types
type Status = 'pending' | 'active' | 'completed';
type ApiResult<T> = { success: true; data: T } | { success: false; error: string };

// Avoid any - use unknown if type is truly unknown
function processData(data: unknown) {
  if (typeof data === 'string') {
    return data.toUpperCase();
  }
  // Handle other cases...
}
```

---

## Git Practices

### Commit Messages

Follow the Conventional Commits specification:

```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types**:
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting, etc.)
- `refactor`: Code refactoring
- `test`: Adding or updating tests
- `chore`: Maintenance tasks

**Examples**:
```
feat(auth): add JWT authentication

Implement JWT-based authentication for API endpoints.
- Add token generation and validation
- Create auth middleware
- Update user routes to require authentication

Closes #123
```

```
fix(api): handle network timeouts correctly

Previously, network timeouts would crash the application.
Now they are caught and handled gracefully.
```

### Git Workflow Commands

```bash
# Create and switch to a new branch
git checkout -b feature/new-feature

# Stage changes
git add .

# Commit with message
git commit -m "feat(scope): description"

# Push to remote (with upstream tracking)
git push -u origin feature/new-feature

# Fetch latest changes
git fetch origin

# Pull changes from remote
git pull origin main

# Retry on network errors (up to 4 times with exponential backoff)
git push -u origin feature/new-feature || \
  (sleep 2 && git push -u origin feature/new-feature) || \
  (sleep 4 && git push -u origin feature/new-feature) || \
  (sleep 8 && git push -u origin feature/new-feature)
```

### Branch Naming

- Feature branches: `claude/claude-md-*` or `feature/descriptive-name`
- Bug fixes: `fix/issue-description`
- Hotfixes: `hotfix/critical-issue`
- Experiments: `experiment/idea-name`

**Important**: When using Claude AI for development, branch names should start with `claude/` and end with the matching session ID to ensure proper permissions.

---

## Testing Guidelines

### Testing Principles

1. **Write tests for all new features**
2. **Maintain high test coverage** (aim for >80%)
3. **Test edge cases and error conditions**
4. **Keep tests simple and focused**
5. **Use descriptive test names**

### Test Structure

```typescript
describe('UserService', () => {
  describe('getUserById', () => {
    it('should return user when ID exists', async () => {
      // Arrange
      const userId = '123';
      const expectedUser = { id: userId, name: 'Alice' };

      // Act
      const result = await userService.getUserById(userId);

      // Assert
      expect(result).toEqual(expectedUser);
    });

    it('should throw error when ID does not exist', async () => {
      // Arrange
      const userId = 'nonexistent';

      // Act & Assert
      await expect(userService.getUserById(userId))
        .rejects.toThrow('User not found');
    });

    it('should handle network errors gracefully', async () => {
      // Arrange
      const userId = '123';
      mockApi.get.mockRejectedValue(new Error('Network error'));

      // Act & Assert
      await expect(userService.getUserById(userId))
        .rejects.toThrow('Network error');
    });
  });
});
```

### Testing Commands

```bash
# Run all tests
npm test

# Run tests in watch mode
npm run test:watch

# Run tests with coverage
npm run test:coverage

# Run specific test file
npm test user-service.test.ts
```

---

## Documentation Standards

### Code Documentation

```typescript
/**
 * Fetches a user by their unique identifier.
 *
 * @param userId - The unique identifier of the user
 * @returns A promise that resolves to the user object
 * @throws {NotFoundError} When the user does not exist
 * @throws {NetworkError} When the API request fails
 *
 * @example
 * ```typescript
 * const user = await getUserById('123');
 * console.log(user.name);
 * ```
 */
async function getUserById(userId: string): Promise<User> {
  // Implementation...
}
```

### README Structure

Every major module or feature should have documentation explaining:

1. **Purpose**: What does this module do?
2. **Usage**: How do you use it?
3. **API**: What are the public interfaces?
4. **Examples**: Show real-world usage
5. **Dependencies**: What does it depend on?
6. **Testing**: How to test it?

### Inline Comments

```typescript
// Use comments to explain WHY, not WHAT
// Good:
// We use a retry mechanism here because the external API is unreliable
await retryRequest(apiCall, { maxRetries: 3 });

// Bad:
// Retry the request 3 times
await retryRequest(apiCall, { maxRetries: 3 });
```

---

## AI Assistant Guidelines

### When Working as an AI Assistant on This Project

#### 1. Understanding Context

- **Always read CLAUDE.md first** when starting work on this repository
- Check for existing patterns before introducing new ones
- Review recent commits to understand ongoing work
- Look for related tests before modifying code

#### 2. Code Modifications

- **Prefer editing over creating**: Modify existing files rather than creating new ones unless necessary
- **Maintain consistency**: Follow the existing code style and patterns
- **Update tests**: Modify or add tests when changing functionality
- **Update documentation**: Keep CLAUDE.md and other docs in sync with code changes

#### 3. Communication

- **Be concise**: Provide clear, actionable information
- **No unnecessary emojis**: Keep communication professional
- **Reference locations**: Use `file_path:line_number` format when discussing code
- **Explain decisions**: Briefly explain why you chose a particular approach

#### 4. Task Management

- **Use TodoWrite**: Track multi-step tasks with the TodoWrite tool
- **Mark progress**: Update todo status as you complete each step
- **Don't batch completions**: Mark tasks complete immediately after finishing

#### 5. Problem Solving

- **Research first**: Use Explore agent to understand the codebase before making changes
- **Test your changes**: Verify that code works before committing
- **Handle errors**: Address compilation errors, test failures, and linting issues
- **Security awareness**: Watch for vulnerabilities (XSS, SQL injection, etc.)

#### 6. Git Operations

- **Develop on feature branches**: Use the designated branch (starts with `claude/`)
- **Write clear commits**: Follow conventional commit format
- **Push with retry logic**: Use `-u` flag and retry on network errors
- **Never force push** to main branches without explicit permission

#### 7. Common Pitfalls to Avoid

- ❌ Don't use `any` type without good reason
- ❌ Don't skip error handling
- ❌ Don't commit without testing
- ❌ Don't create files unnecessarily
- ❌ Don't ignore linting errors
- ❌ Don't modify dependencies without discussion
- ❌ Don't push to wrong branches
- ❌ Don't make breaking changes without documentation

#### 8. Best Practices

- ✅ Write type-safe TypeScript
- ✅ Add tests for new functionality
- ✅ Update documentation when changing behavior
- ✅ Use parallel tool calls when possible
- ✅ Handle edge cases and errors
- ✅ Keep functions small and focused
- ✅ Use meaningful variable names
- ✅ Clean up commented code and console.logs before committing

---

## Common Tasks

### Adding a New Feature

1. Create a feature branch
2. Implement the feature in `src/`
3. Add tests in `tests/`
4. Update relevant documentation
5. Run tests and linting
6. Commit and push
7. Create a pull request

### Fixing a Bug

1. Create a fix branch
2. Write a failing test that reproduces the bug
3. Fix the bug
4. Verify the test passes
5. Add regression tests if needed
6. Commit and push

### Refactoring Code

1. Ensure existing tests pass
2. Make refactoring changes
3. Verify tests still pass
4. Update documentation if interfaces changed
5. Commit with `refactor:` prefix

### Updating Dependencies

```bash
# Check for outdated dependencies
npm outdated

# Update specific package
npm update package-name

# Update all packages (careful!)
npm update

# Verify tests still pass
npm test
```

### Running Quality Checks

```bash
# Type checking
npm run type-check

# Linting
npm run lint

# Linting with auto-fix
npm run lint:fix

# Format code
npm run format

# Run all checks
npm run check
```

---

## Project-Specific Notes

### Technology Stack (To Be Determined)

As the project develops, document the specific technologies here:

- **Language**: TypeScript (likely)
- **Runtime**: Node.js / Browser (TBD)
- **Framework**: (TBD)
- **Database**: (TBD)
- **Testing**: (TBD)
- **Build Tool**: (TBD)

### Architecture Decisions

Document key architectural decisions as they are made:

1. **Decision**: [Title]
   - **Context**: Why was this decision needed?
   - **Decision**: What was decided?
   - **Consequences**: What are the implications?

### Known Issues

Track known issues and limitations:

- None currently (new repository)

### Future Improvements

Track ideas for future enhancements:

- Initialize project structure
- Set up CI/CD pipeline
- Configure linting and formatting
- Add pre-commit hooks
- Set up development environment

---

## Maintenance

### Updating This Document

This document should be updated when:

- Project structure changes significantly
- New conventions are established
- Development workflow changes
- New tools or technologies are adopted
- Common patterns emerge that should be documented

**Update the "Last Updated" date at the top when making changes.**

### Questions or Suggestions

If you have questions about conventions or suggestions for improvements:

1. Document them in issue tracker
2. Discuss with team
3. Update CLAUDE.md once consensus is reached

---

## Additional Resources

### Recommended Reading

- [TypeScript Documentation](https://www.typescriptlang.org/docs/)
- [Conventional Commits](https://www.conventionalcommits.org/)
- [Git Best Practices](https://git-scm.com/book/en/v2)
- [Testing Best Practices](https://testingjavascript.com/)

### Useful Commands Reference

```bash
# Git
git status                          # Check repository status
git log --oneline -10               # View recent commits
git diff                            # See unstaged changes
git branch -a                       # List all branches

# NPM
npm run <script>                    # Run package.json script
npm list --depth=0                  # List installed packages
npm ci                              # Clean install from lock file

# Development
npm run dev                         # Start development server
npm run build                       # Build for production
npm test                            # Run tests
npm run lint                        # Run linter
```

---

**End of CLAUDE.md**

*This document serves as a living guide for AI assistants and developers working on straas.ai. Keep it updated as the project evolves.*
