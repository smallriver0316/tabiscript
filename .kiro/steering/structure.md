# Project Structure

## Repository Organization

Tabi Script follows a monorepo architecture using pnpm workspaces, keeping web, mobile, and API applications in a single repository. This approach enables shared code, coordinated releases, and simplified development workflow while maintaining clear separation of concerns.

## Benefits of Monorepo Approach

- **Shared Code**: Common TypeScript types, utilities, and business logic
- **Coordinated Releases**: Deploy web, mobile, and API changes together
- **Simplified Development**: Single repository to clone and manage
- **Consistent Dependencies**: Shared package versions across all apps
- **Cross-Platform Feature Parity**: Easier to maintain consistency

## Current Structure

```
tabiscript/
├── .git/                    # Git repository
├── .vscode/                 # VS Code workspace settings
├── .kiro/                   # Kiro AI assistant configuration
│   ├── specs/               # Project specifications
│   └── steering/            # AI steering rules
├── .gitignore              # Git ignore patterns (Node.js focused)
├── LICENSE                 # Apache License 2.0
├── README.md               # Project documentation
└── concept.md              # Product concept and features
```

## Recommended Monorepo Structure

```
tabiscript/
├── apps/                   # Application packages
│   ├── web/               # Next.js web application
│   │   ├── app/           # Next.js App Router
│   │   │   ├── (auth)/    # Auth route group
│   │   │   │   ├── login/
│   │   │   │   └── register/
│   │   │   ├── dashboard/ # Main dashboard
│   │   │   ├── travel/    # Travel management
│   │   │   │   ├── [id]/  # Dynamic travel routes
│   │   │   │   │   ├── map/       # Map view
│   │   │   │   │   ├── calendar/  # Calendar view
│   │   │   │   │   └── timeline/  # Timeline view
│   │   │   │   └── create/        # Create new travel
│   │   │   ├── blog/      # Blog management
│   │   │   │   └── [id]/  # Dynamic blog routes
│   │   │   ├── api/       # API routes
│   │   │   │   └── [...route]/    # Hono.js catch-all
│   │   │   ├── globals.css        # Global styles
│   │   │   └── layout.tsx         # Root layout
│   │   ├── components/    # Web-specific components
│   │   │   ├── Map/       # Map-related components
│   │   │   ├── Calendar/  # Calendar components
│   │   │   ├── Travel/    # Travel components
│   │   │   ├── Blog/      # Blog components
│   │   │   └── UI/        # Generic UI components
│   │   ├── lib/           # Web-specific utilities
│   │   ├── hooks/         # Web-specific hooks
│   │   ├── public/        # Static assets
│   │   ├── package.json
│   │   ├── next.config.js
│   │   ├── tailwind.config.js
│   │   └── tsconfig.json
│   ├── mobile/            # React Native mobile application
│   │   ├── src/
│   │   │   ├── components/        # Mobile-specific components
│   │   │   │   ├── Map/           # Map components
│   │   │   │   ├── Calendar/      # Calendar components
│   │   │   │   └── Travel/        # Travel components
│   │   │   ├── screens/           # Screen components
│   │   │   │   ├── Auth/          # Authentication screens
│   │   │   │   ├── Travel/        # Travel screens
│   │   │   │   ├── Content/       # Content recording screens
│   │   │   │   └── Blog/          # Blog screens
│   │   │   ├── navigation/        # Navigation configuration
│   │   │   ├── services/          # Mobile-specific services
│   │   │   ├── hooks/             # Mobile-specific hooks
│   │   │   └── utils/             # Mobile-specific utilities
│   │   ├── assets/                # Static assets
│   │   ├── app.json               # Expo configuration
│   │   ├── package.json
│   │   └── tsconfig.json
│   └── api/               # Hono.js API (deployed as Vercel functions)
│       ├── routes/        # API route handlers
│       │   ├── auth.ts    # Authentication routes
│       │   ├── travel.ts  # Travel management
│       │   ├── content.ts # Content recording
│       │   ├── blog.ts    # Blog generation
│       │   ├── map.ts     # Map and location services
│       │   └── calendar.ts        # Calendar operations
│       ├── middleware/    # Custom middleware
│       │   ├── auth.ts    # Authentication middleware
│       │   ├── cors.ts    # CORS configuration
│       │   └── error.ts   # Error handling
│       ├── services/      # Business logic services
│       │   ├── travel.service.ts
│       │   ├── blog.service.ts
│       │   ├── map.service.ts
│       │   └── ai.service.ts
│       ├── utils/         # API-specific utilities
│       ├── package.json
│       ├── tsconfig.json
│       └── index.ts       # Main API entry point
├── packages/              # Shared packages
│   ├── shared-types/      # Common TypeScript types
│   │   ├── src/
│   │   │   ├── travel.ts  # Travel-related types
│   │   │   ├── user.ts    # User-related types
│   │   │   ├── api.ts     # API response types
│   │   │   └── index.ts   # Barrel exports
│   │   ├── package.json
│   │   └── tsconfig.json
│   ├── shared-utils/      # Common utilities
│   │   ├── src/
│   │   │   ├── date.ts    # Date utilities
│   │   │   ├── validation.ts      # Validation helpers
│   │   │   ├── constants.ts       # App constants
│   │   │   └── index.ts   # Barrel exports
│   │   ├── package.json
│   │   └── tsconfig.json
│   └── ui-components/     # Shared UI components (future)
│       ├── src/
│       ├── package.json
│       └── tsconfig.json
├── database/              # Database related files
│   ├── migrations/        # Supabase migrations
│   ├── seed/              # Seed data
│   └── schema.sql         # Database schema
├── docs/                  # Documentation
│   ├── api.md             # API documentation
│   ├── deployment.md      # Deployment guide
│   └── development.md     # Development setup
├── .github/               # GitHub workflows
│   └── workflows/
│       ├── ci.yml         # Continuous integration
│       └── deploy.yml     # Deployment workflow
├── package.json           # Root package.json with workspaces
├── tsconfig.json          # Root TypeScript configuration
├── .env.example           # Environment variables template
└── turbo.json             # Turborepo configuration (optional)
```

## Workspace Configuration

### Root package.json

```json
{
  "name": "tabiscript",
  "private": true,
  "scripts": {
    "dev": "pnpm --filter=web dev",
    "dev:mobile": "pnpm --filter=mobile dev",
    "dev:api": "pnpm --filter=api dev",
    "build": "pnpm -r build",
    "test": "pnpm -r test",
    "lint": "pnpm -r lint",
    "type-check": "pnpm -r type-check"
  },
  "devDependencies": {
    "@types/node": "^20.0.0",
    "typescript": "^5.0.0",
    "eslint": "^8.0.0",
    "prettier": "^3.0.0"
  }
}
```

### pnpm-workspace.yaml

```yaml
packages:
  - 'apps/*'
  - 'packages/*'
```

### Shared Package Usage

```typescript
// In apps/web or apps/mobile
import { Travel, Destination } from '@tabiscript/shared-types'
import { formatDate, validateEmail } from '@tabiscript/shared-utils'
```

## File Naming Conventions

### Components

- **React Components**: PascalCase (e.g., `TravelMap.tsx`, `DestinationMarker.tsx`)
- **Component Files**: Include component name in filename
- **Index Files**: Use `index.ts` for barrel exports

### API Routes

- **Route Files**: kebab-case (e.g., `travel-plans.ts`, `blog-generation.ts`)
- **Handler Functions**: camelCase (e.g., `getTravelPlans`, `createBlogPost`)

### Utilities and Services

- **Service Files**: kebab-case with `.service.ts` suffix
- **Utility Files**: kebab-case with `.utils.ts` or `.helpers.ts` suffix
- **Type Files**: kebab-case with `.types.ts` suffix

### Database

- **Table Names**: snake_case (e.g., `travel_plans`, `calendar_events`)
- **Column Names**: snake_case (e.g., `created_at`, `user_id`)
- **Migration Files**: Timestamp prefix with descriptive name

## Import Organization

### Import Order

1. React and Next.js imports
2. Third-party library imports
3. Internal component imports
4. Utility and service imports
5. Type imports (with `type` keyword)

```typescript
// Example import organization
import React from 'react'
import { NextPage } from 'next'

import { Button } from '@/components/UI/Button'
import { TravelMap } from '@/components/Map/TravelMap'

import { supabase } from '@/lib/supabase'
import { formatDate } from '@/utils/date'

import type { Travel, Destination } from '@/types/travel'
```

## Directory Guidelines

### Component Organization

- Group related components in feature-based directories
- Use barrel exports (`index.ts`) for clean imports
- Keep component files focused and single-responsibility

### API Organization

- Organize routes by feature/domain
- Use middleware for cross-cutting concerns
- Separate business logic into service files

### Asset Management

- Optimize images before committing
- Use appropriate formats (WebP for web, optimized PNG/JPG for mobile)
- Organize assets by feature or type

## Monorepo Management

### Common Workspace Commands

```bash
# Install dependencies for all workspaces
pnpm install

# Run development server for web app
pnpm --filter=web dev

# Run mobile development
pnpm --filter=mobile dev

# Build all applications
pnpm -r build

# Run tests across all packages
pnpm -r test

# Install package in specific workspace
pnpm --filter=web add lodash

# Add shared package as dependency
pnpm --filter=mobile add @tabiscript/shared-types
```

### Shared Package Development

```bash
# Build shared packages first
pnpm --filter=@tabiscript/shared-types build
pnpm --filter=@tabiscript/shared-utils build

# Watch mode for shared package development
pnpm --filter=@tabiscript/shared-types dev

# Build all shared packages
pnpm --filter="./packages/*" build
```

## Configuration Files

### Root Level Configuration

- `package.json`: Root package.json with workspaces configuration
- `tsconfig.json`: Root TypeScript configuration with path mapping
- `.env.example`: Environment variable template for all apps
- `turbo.json`: Turborepo configuration for build optimization (optional)
- `vercel.json`: Vercel deployment configuration
- `.github/workflows/`: CI/CD workflows for all applications

### Application-Specific Configuration

- `apps/web/next.config.js`: Next.js configuration
- `apps/web/tailwind.config.js`: Tailwind CSS configuration
- `apps/mobile/app.json`: Expo configuration
- `apps/api/tsconfig.json`: API-specific TypeScript configuration

### Development Tools

- `.eslintrc.json`: ESLint configuration (root level)
- `.prettierrc`: Prettier configuration (root level)
- `vitest.config.ts`: Test configuration per workspace
