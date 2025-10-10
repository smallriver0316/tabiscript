# Technology Stack

## Architecture Overview

Tabi Script is built as a modern full-stack application with Next.js for web, React Native for mobile, Hono.js for API, and Supabase as the backend-as-a-service platform.

## Tech Stack

### Frontend

- **Web**: Next.js 15 with App Router, TypeScript, Tailwind CSS, React Query (TanStack Query)
- **Mobile**: React Native with Expo, TypeScript, React Navigation, Supabase client
- **Maps**: Mapbox GL JS for web, react-native-mapbox-gl for mobile
- **Calendar**: FullCalendar with React wrapper for web, react-native-calendars for mobile

### Backend

- **API Framework**: Hono.js with TypeScript
- **Database**: Supabase PostgreSQL with Row Level Security
- **Authentication**: Supabase Auth with social providers
- **File Storage**: Supabase Storage with CDN
- **Real-time**: Supabase Real-time subscriptions
- **Maps**: Mapbox API, Geocoding API, Directions API

### Infrastructure

- **Hosting**: Vercel with Edge Runtime
- **Database**: Supabase managed PostgreSQL
- **CDN**: Vercel Edge Network + Supabase CDN
- **Monitoring**: Vercel Analytics + Supabase Dashboard

### AI/LLM Integration

- **Primary**: Groq API with Llama 3.1 70B (free tier)
- **Alternative**: Ollama for self-hosted models
- **Fallback**: Hugging Face Inference API

## Development Tools

### Package Management

- **Node.js**: v18+ required
- **Package Manager**: pnpm (preferred for performance and disk efficiency)
- **Monorepo**: pnpm workspaces for web/mobile shared code

### Code Quality

- **TypeScript**: Strict mode enabled
- **ESLint**: Standard configuration with React/Next.js rules
- **Prettier**: Code formatting
- **Husky**: Git hooks for pre-commit checks

### Testing

- **Unit/Integration**: Vitest for fast testing
- **Component**: React Testing Library
- **API**: Hono testing utilities
- **E2E**: Playwright (web), Detox (mobile)

## Common Commands

### Development Setup

```bash
# Install dependencies
pnpm install

# Start development server (web)
pnpm dev

# Start mobile development
pnpm dlx expo start

# Run tests
pnpm test

# Type checking
pnpm type-check

# Linting
pnpm lint

# Build for production
pnpm build
```

### Database Management

```bash
# Run Supabase locally
pnpm dlx supabase start

# Generate types from database
pnpm dlx supabase gen types typescript --local > types/database.types.ts

# Reset local database
pnpm dlx supabase db reset

# Deploy migrations
pnpm dlx supabase db push
```

### Deployment

```bash
# Deploy to Vercel (web)
pnpm dlx vercel --prod

# Build mobile app
pnpm dlx expo build:android
pnpm dlx expo build:ios

# Deploy Supabase functions
pnpm dlx supabase functions deploy
```

## Environment Variables

### Required Environment Variables

```bash
# Supabase
NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
SUPABASE_SERVICE_ROLE_KEY=your_service_role_key

# Mapbox
NEXT_PUBLIC_MAPBOX_ACCESS_TOKEN=your_mapbox_token
MAPBOX_SECRET_TOKEN=your_mapbox_secret

# AI/LLM
GROQ_API_KEY=your_groq_api_key

# Optional
VERCEL_URL=auto_populated_by_vercel
```

## Cost-Effective Development Strategy

### Free Tier Usage

- **Vercel**: Hobby plan (free) - 100GB bandwidth
- **Supabase**: Free tier - 500MB database, 1GB bandwidth
- **Mapbox**: Free tier - 50,000 map loads/month
- **Groq**: Free Llama 3.1 70B API (rate limited)

### Optimization Guidelines

- Use Vercel Edge Functions for lightweight operations
- Implement proper caching strategies
- Optimize images and media files
- Use Supabase RLS for security
- Implement offline-first mobile architecture
