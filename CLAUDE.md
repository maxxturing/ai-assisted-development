**IMPORTANT FOR CLAUDE: Reference this file before implementing anything**

# Project: Travel Planning App

## Project Overview

A universal travel planning application built with Solito that allows users to manage trips and create packing lists. The app provides native mobile experience while maintaining full web functionality. Focus on Trip Management and Packing Lists features only.

## Tech Stack

- Language: TypeScript (strict mode)
- Frontend: Solito (React Native + Next.js)
- Styling: Tamagui (Universal Design System)
- Database: Turso (LibSQL) with Drizzle ORM
- State Management: React Query (TanStack Query) + Custom Hooks
- Package Manager: Yarn
- Mobile: React Native with Expo
- Web: Next.js

## Code Style & Conventions

### Import/Module Standards

- External libraries first
- Internal packages second  
- Relative imports last
- Empty lines between groups

### Naming Conventions

- Files: kebab-case for components (`trip-list.tsx`), camelCase for utilities (`formatDate.ts`)
- Components: PascalCase (`TripList`, `PackingItem`)
- Hooks: camelCase with 'use' prefix (`useTrips`, `usePackingItems`)
- Constants: UPPER_SNAKE_CASE (`MAX_TRIP_NAME_LENGTH`)
- Database tables: camelCase (`packingItems`, `packingLists`)

### Patterns to Follow

- Business logic in custom hooks only
- Components focused on UI presentation only
- Shared utilities in appropriate packages
- React Query for all server state
- Optimistic updates for user interactions
- Error boundaries + Toast notifications for error handling

## Development Workflow

- Branch strategy: feature branches (`feature/trip-management`, `feature/packing-lists`)
- Commit message format: Conventional commits (`feat:`, `fix:`, `docs:`)
- PR requirements: Code review required, proper commit messages

## Testing Strategy

- Framework: Jest + React Testing Library (minimal testing approach)
- Focus: Critical business logic and custom hooks only
- Coverage: Essential tests only due to workshop scope

## Environment Setup

- Node.js with Yarn package manager
- Expo CLI for mobile development
- Turso database (edge-distributed LibSQL)

## Common Commands

```bash
# Install dependencies
yarn install

# Development server (web)
yarn web

# Development server (mobile)
yarn native

# Build web
yarn build:web

# Build mobile
yarn build:native

# Type check
yarn type-check
```

## Project Structure

Monorepo package organization:

- `/packages/app` - Shared navigation and business logic
- `/packages/ui` - Universal Tamagui components
- `/packages/db` - Drizzle schema and database queries
- `/packages/config` - Shared TypeScript and build configs
- `/apps/expo` - Mobile application
- `/apps/next` - Web application

## Review Process Guidelines

Before submitting any code, ensure the following steps are completed:

1. **Run all lint, check and test commands**

2. **Review outputs and iterate until all issues are resolved**

3. **Assess compliance**:
   For each standard, explicitly state ✅ or ❌ and explain why:

   - Code style and formatting
   - Naming conventions
   - Architecture patterns (refer to `ARCHITECTURE.md`)
   - Error handling
   - Test coverage
   - Documentation

4. **Self-review checklist**:
   - [ ] Code follows defined patterns
   - [ ] No debug/commented code
   - [ ] Error handling implemented
   - [ ] Tests written and passing
   - [ ] Documentation updated

## Known Issues & Workarounds

Document any current limitations or workarounds Claude should be aware of.

## References

Links to relevant external documentation, design docs, or resources.
