# AGENTS.md - Guidelines for Agentic Coding

This file provides guidelines for agents operating in this repository.

## Build / Lint / Test Commands

### General Commands
- `npm install` - Install dependencies
- `npm run build` - Build the project
- `npm run dev` - Start development server
- `npm run lint` - Run linter
- `npm run typecheck` - Run TypeScript type checking

### Running Tests
- `npm test` - Run all tests
- `npm test -- --testPathPattern=<pattern>` - Run tests matching a pattern
- `npm test -- --testNamePattern=<name>` - Run tests with specific name
- `npm test -- <file>` - Run tests in a specific file
- `npm run test:watch` - Run tests in watch mode
- `npm run test:coverage` - Run tests with coverage

### Other Commands
- `npm run format` - Format code with prettier
- `npm run lint:fix` - Fix linting issues automatically

---

## Code Style Guidelines

### General Principles
- Keep code simple and readable
- Follow the existing code style in the project
- Write self-documenting code with clear variable/function names
- Keep functions small and focused (single responsibility)
- Avoid premature optimization

### Imports
- Use absolute imports when possible (configured via path aliases)
- Order imports: external libraries → internal modules → relative imports
- Group imports: React/framework imports → utilities → types → styles
- Example:
  ```typescript
  import { useState, useEffect } from 'react'
  import { format } from 'date-fns'
  import { api } from '@/lib/api'
  import { User } from '@/types'
  import { Button } from './Button'
  import './styles.css'
  ```

### Formatting
- Use 2 spaces for indentation
- Use single quotes for strings in JavaScript/TypeScript
- Add trailing commas in multi-line objects/arrays
- Maximum line length: 100 characters
- Use semicolons in JavaScript

### Types
- Use TypeScript for all new code
- Avoid `any` - use `unknown` when type is truly unknown
- Use explicit return types for functions
- Define interfaces for objects
- Use type aliases for unions/enums

### Naming Conventions
- **Files**: kebab-case (e.g., `user-profile.tsx`)
- **Components**: PascalCase (e.g., `UserProfile.tsx`)
- **Functions/variables**: camelCase (e.g., `getUserData`)
- **Constants**: SCREAMING_SNAKE_CASE (e.g., `MAX_RETRIES`)
- **Interfaces**: PascalCase with optional 'I' prefix (e.g., `User` or `IUser`)
- **Booleans**: Use 'is', 'has', 'should', 'can' prefixes (e.g., `isActive`)

### Error Handling
- Always handle async errors with try/catch
- Log errors appropriately (use project's logging utility)
- Return meaningful error messages to users
- Never expose sensitive information in error messages
- Example:
  ```typescript
  try {
    const data = await fetchUser(id)
    return data
  } catch (error) {
    logger.error('Failed to fetch user', { id, error })
    throw new UserFriendlyError('Unable to load user data')
  }
  ```

### React/Component Guidelines
- Use functional components with hooks
- Memoize expensive computations with `useMemo`
- Memoize callbacks with `useCallback` when passed to child components
- Keep component state minimal - lift state up when needed
- Use composition over inheritance
- Extract reusable logic into custom hooks

### Testing Guidelines
- Write tests alongside code (TDD recommended for complex features)
- Use descriptive test names: `describe('UserService', () => { it('should...') })`
- Follow AAA pattern: Arrange → Act → Assert
- Mock external dependencies (API calls, localStorage, etc.)
- Test edge cases and error scenarios
- Aim for meaningful test coverage, not just high percentage

### Git Conventions
- Write clear, descriptive commit messages
- Use conventional commits format: `type(scope): description`
- Types: feat, fix, docs, style, refactor, test, chore
- Keep commits atomic and focused

### Security
- Never commit secrets, API keys, or credentials
- Use environment variables for sensitive configuration
- Validate and sanitize all user inputs
- Follow OWASP security guidelines

---

## Project Structure

```
src/
├── components/     # Reusable UI components
├── hooks/          # Custom React hooks
├── lib/            # Utilities and libraries
├── pages/          # Page components
├── services/       # API services
├── types/          # TypeScript type definitions
└── styles/         # Global styles
```

---

## Notes for Agents

1. Always check package.json for available scripts
2. Run lint and typecheck before submitting changes
3. Test your changes before marking as complete
4. If unsure about conventions, look at existing code in the project
5. Ask for clarification when requirements are ambiguous
