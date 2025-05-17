# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a full-stack SaaS starter kit built on Cloudflare's platform using:
- Next.js for the frontend with App Router
- TailwindCSS and ShadcnUI for styling/components
- Drizzle ORM for database access
- NextAuth for authentication
- Cloudflare D1 for serverless database
- Cloudflare Pages for hosting

## Commands

### Development
- `bun run dev` - Start the development server
- `bun run lint` - Run ESLint
- `bun run build` - Build the application
- `bun run start` - Start the production server

### Cloudflare Specific
- `bun run pages:build` - Build for Cloudflare Pages
- `bun run preview` - Preview locally with Wrangler
- `bun run deploy` - Deploy to Cloudflare Pages
- `bun run cf-typegen` - Generate TypeScript types for Cloudflare env

### Database
- `bun run db:generate` - Generate Drizzle migration files
- `bun run db:migrate:dev` - Apply migrations to local dev database
- `bun run db:migrate:prod` - Apply migrations to production database
- `bun run db:studio:dev` - Open Drizzle Studio for local database
- `bun run db:studio:prod` - Open Drizzle Studio for production database

## Architecture

### Authentication
The app uses NextAuth.js with Google OAuth provider and Drizzle adapter. Authentication configuration is in `src/server/auth.ts`.

### Database
- Uses Cloudflare D1 (SQLite-compatible serverless database)
- Schema defined in `src/server/db/schema.ts`
- Database connection in `src/server/db/index.ts`
- Local development uses SQLite files in `.wrangler/state/v3/d1`
- Production uses the remote D1 database

### Cloudflare Services Configuration
Cloudflare bindings and services are configured in `wrangler.toml`, including:
- D1 database
- Optionally can add R2 for file storage, KV for key-value storage, etc.

## Environment Setup

### Local Environment
1. Requires Wrangler CLI installed and authenticated (`wrangler login`)
2. Create a `.dev.vars` file with:
   - `AUTH_GOOGLE_ID` and `AUTH_GOOGLE_SECRET` for Google OAuth
   - `AUTH_SECRET` for session encryption

### Production Environment
The following environment variables are needed for production:
- For database migrations: `CLOUDFLARE_D1_ACCOUNT_ID`, `DATABASE`, `CLOUDFLARE_D1_API_TOKEN`

## Code Style Guidelines

This codebase follows these style conventions:
- Functional and declarative programming patterns over classes
- TypeScript for all code with proper typing
- React Server Components (RSC) by default, minimize `use client` directives
- Shadcn UI and Tailwind CSS for styling
- Descriptive variable names with auxiliary verbs (e.g., isLoading, hasError)
- Favor composition and modularization over code duplication