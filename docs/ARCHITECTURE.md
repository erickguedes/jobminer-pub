# Architecture Overview

## High-Level Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                        Browser                               │
│                    (React SPA + SSR)                         │
└──────────────────────┬──────────────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────────────┐
│                     Vercel (TanStack Start)                   │
│                                                               │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────┐  │
│  │ TanStack     │  │ TanStack     │  │ Server Functions │  │
│  │ Router       │  │ Query        │  │ (API endpoints)  │  │
│  │ (file-based) │  │ (caching)    │  │                  │  │
│  └──────┬───────┘  └──────┬───────┘  └────────┬─────────┘  │
│         │                 │                    │             │
│         └─────────────────┴────────────────────┘             │
└──────────────────────────────────────────────────────────────┘
         │                    │                    │
         ▼                    ▼                    ▼
┌──────────────┐   ┌──────────────────┐   ┌──────────────────┐
│  Supabase    │   │  Google Gemini   │   │  @react-pdf      │
│  PostgreSQL  │   │  API (AI)        │   │  /renderer       │
│  + Auth      │   │  4-model        │   │  (PDF gen)       │
│  + Storage   │   │  fallback chain │   │  + docx (DOCX)   │
└──────────────┘   └──────────────────┘   └──────────────────┘
```

## Architecture Decisions

### Single-Deploy Full-Stack (TanStack Start)

The entire application runs as a single TanStack Start project on Vercel. This eliminates:
- CORS configuration between frontend and backend
- Network latency for API calls
- Multiple deployment pipelines
- Additional hosting costs

Server functions (equivalent to traditional API routes) run as Nitro serverless functions on Vercel's edge network.

### Supabase as Backend-as-a-Service

Supabase provides the entire data layer:
- **PostgreSQL** — relational database with Row-Level Security for multi-tenant data isolation
- **Auth** — Google and LinkedIn OAuth providers, JWT session management
- **Storage** — file storage for PDFs and user knowledge-base files

Each database query is automatically scoped to the authenticated user via RLS policies — no manual `WHERE user_id = ?` logic needed.

### Google Gemini with Fallback Chain

The AI service uses Gemini 2.5 Flash as the primary model, with automatic fallback through 2.5 Pro → 2.0 Flash → 2.0 Flash Lite when rate limits are hit. This ensures robustness without exposing rate limit errors to the user.

### PDF Generation Without Headless Browser

Instead of using Playwright or Puppeteer (which require Chromium and have cold start issues on serverless), the application uses `@react-pdf/renderer` — a React component library that renders to PDF natively in Node.js. The same React components that render the UI also render the PDF, ensuring visual consistency.

## Data Flow

### Opportunity Processing Flow

```
User submits job description
        │
        ▼
Server function receives request
        │
        ▼
Builds prompt with:
  ├── User's resume (from Supabase)
  ├── Optional KB files (from Storage)
  └── Job description + instructions
        │
        ▼
Sends to Gemini API (with fallback chain)
        │
        ▼
Parses response using delimiters (===ANALISE===, ===CURRICULO===, etc.)
        │
        ▼
Saves documents to Supabase (analysis, cv, cover_letter, salary)
        │
        ▼
User views, edits inline, and exports as PDF or DOCX
```

### PDF/DOCX Generation Flow

```
User clicks "Download PDF" or "Download DOCX"
        │
        ▼
Server function loads document markdown from Supabase
        │
        ├── PDF: Renders @react-pdf component → buffer → response
        └── DOCX: Builds docx document → buffer → response
        │
        ▼
Browser receives file as download
```

## Security

- **Row-Level Security** — every Supabase table has `USING (user_id = auth.uid())`
- **JWT authentication** — all server functions validate the Supabase session
- **No sensitive data in public repo** — KB files, API keys, and secrets are never committed
- **API keys** stored as Vercel Environment Variables
