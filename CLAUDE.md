# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

UIGen is an AI-powered React component generator with live preview. It allows users to describe React components in natural language and generates them using Claude AI, with a virtual file system for preview and editing.

## Development Commands

- `npm run setup` - Install dependencies, generate Prisma client, and run migrations (required for first-time setup)
- `npm run dev` - Start development server with Turbopack on http://localhost:3000
- `npm run dev:daemon` - Start dev server in background, logging to logs.txt
- `npm run build` - Build production bundle
- `npm run lint` - Run ESLint
- `npm run test` - Run tests with Vitest
- `npm run db:reset` - Reset database with force flag

## Architecture

### Core Components
- **Virtual File System** (`src/lib/file-system.ts`): In-memory file system that manages generated components without writing to disk
- **Chat Interface** (`src/components/chat/`): AI conversation interface for component generation
- **Code Editor** (`src/components/editor/`): Monaco-based editor with file tree navigation
- **Preview System** (`src/components/preview/`): Live preview of generated React components

### Database Schema
- **Users**: Authentication with email/password using bcrypt
- **Projects**: Store chat messages and component data as JSON strings, with optional user association
- Uses SQLite with Prisma ORM, client generated to `src/generated/prisma/`

### AI Integration
- Uses Anthropic Claude via Vercel AI SDK (`src/app/api/chat/route.ts`)
- Tools for file management and string replacement operations (`src/lib/tools/`)
- Generation prompts in `src/lib/prompts/`

### Key Contexts
- **ChatContext**: Manages conversation state and AI interactions
- **FileSystemContext**: Manages virtual file system state across components

## Testing
- Uses Vitest with jsdom environment
- React Testing Library for component tests
- Tests located in `__tests__` directories alongside source files
- Run single test file: `npm test -- filename`

## Environment
- Optional `ANTHROPIC_API_KEY` in `.env` - without it, returns static code instead of AI-generated
- Next.js 15 with App Router, React 19, TypeScript
- Tailwind CSS v4 for styling