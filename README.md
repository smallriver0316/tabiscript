# Tabi Script

Tabi Script is a comprehensive travel recording application that supports users throughout their entire travel journey - from pre-travel planning to post-travel blog creation.

## Features

- **Flexible Planning**: Create travel plans without being forced to set dates first
- **Visual Planning**: Interactive map and calendar views for intuitive travel planning
- **Seamless Recording**: Easy content capture during travel with notes and photos
- **AI-Powered Blogging**: Automatic travel blog generation from recorded experiences
- **Cross-Platform**: Available as both web and mobile applications

## Tech Stack

- **Frontend**: Next.js 15 with App Router, TypeScript, Tailwind CSS
- **Backend**: Hono.js API with Supabase PostgreSQL
- **Maps**: Mapbox GL JS
- **AI**: Groq API with Llama 3.1 70B
- **Package Manager**: pnpm with workspaces

## Prerequisites

- Node.js 18+
- pnpm 9.0+

## Getting Started

### Installation

```bash
# Install pnpm globally if you haven't already
npm install -g pnpm

# Install dependencies
pnpm install
```

### Development

```bash
# Start web development server
pnpm dev

# Start mobile development
pnpm dev:mobile

# Start API development
pnpm dev:api
```

### Building

```bash
# Build all applications
pnpm build

# Build specific application
pnpm --filter=web build
```

### Testing

```bash
# Run all tests
pnpm test

# Run tests for specific package
pnpm --filter=web test
```

## Project Structure

```
tabiscript/
├── apps/
│   ├── web/          # Next.js web application
│   ├── mobile/       # React Native mobile app
│   └── api/          # Hono.js API
├── packages/
│   ├── shared-types/ # Common TypeScript types
│   └── shared-utils/ # Common utilities
└── pnpm-workspace.yaml
```

## Environment Variables

Copy `.env.example` to `.env.local` in the web app and fill in your values:

```bash
# Supabase
NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key

# Mapbox
NEXT_PUBLIC_MAPBOX_ACCESS_TOKEN=your_mapbox_token

# AI/LLM
GROQ_API_KEY=your_groq_api_key
```

## License

Apache License 2.0 - see [LICENSE](LICENSE) file for details.
