# Technology Stack

## Frontend & API Framework

| Technology | Version | Role |
|---|---|---|
| **TanStack Start** | 1.x | Full-stack React meta-framework (SSR, file-based routing, server functions) |
| **TanStack Router** | 1.x | Type-safe file-based routing |
| **TanStack Query** | 5.x | Server state management, caching, and data synchronization |
| **React** | 19.x | UI library |
| **Vite** | 7.x | Build tool |
| **TypeScript** | 5.x | Type safety |
| **shadcn/ui** | latest | UI component library (Radix-based, customizable) |
| **Tailwind CSS** | 4.x | Utility-first styling |
| **Recharts** | 2.x | Chart library (activity heatmap, monthly stats) |
| **Lucide React** | latest | Icon library |

**Why TanStack Start over Next.js:** Equivalent performance and features, but with a more modular, library-driven approach. TanStack Router provides first-class TypeScript inference for route params, search params, and loader data without additional configuration.

## Backend & Data

| Technology | Version | Role |
|---|---|---|
| **Supabase** | latest | Backend-as-a-Service: PostgreSQL, Auth, Storage |
| **Supabase JS SDK** | latest | Client and server database access |
| **PostgreSQL** | 15+ | Relational database with RLS |
| **Nitro** | 3.x | Server engine (runs server functions on Vercel Edge) |

**Why Supabase over a custom backend:** Eliminates the need to manage a server, handle authentication infrastructure, or maintain file storage. Row-Level Security provides multi-tenant isolation at the database level — each user can only see their own data, enforced by the database itself.

## AI / Machine Learning

| Technology | Version | Role |
|---|---|---|
| **Google Gemini API** | latest | LLM for job analysis, content generation |
| **@google/generative-ai** | latest | TypeScript SDK for Gemini |
| **Models used** | — | gemini-2.5-flash (primary), 2.5-pro, 2.0-flash, 2.0-flash-lite (fallback) |

**Why Gemini over OpenAI:** Lower cost per token, larger context window (1M tokens for 2.5-flash), and comparable quality for structured text generation tasks like resume adaptation and analysis.

## Document Generation

| Technology | Version | Role |
|---|---|---|
| **@react-pdf/renderer** | 4.x | Declarative PDF generation (JSX → PDF) |
| **docx** | 9.x | Programmatic DOCX generation |

**Why @react-pdf/renderer over Playwright:** No headless browser dependency means zero cold start on serverless, smaller deployment size, and faster generation (~200ms vs ~3s for Playwright). The trade-off is learning a custom layout system (similar to Flexbox but not CSS).

## DevOps & Infrastructure

| Technology | Role |
|---|---|
| **Vercel** | Hosting, serverless functions, edge network, automatic HTTPS |
| **GitHub Actions** | CI/CD pipeline (test → lint → typecheck → deploy) |
| **GitHub** | Source control (private + public repos) |

## Why These Choices

1. **Single language (TypeScript)** — reduces context switching between Python backend and React frontend, simplifies hiring if the team grows
2. **Serverless-first** — zero infrastructure management, automatic scaling, pay-per-use
3. **BaaS for data layer** — Supabase handles auth, database, and storage, letting the application focus on business logic
4. **No headless browser** — PDF generation without Chromium avoids cold start problems and keeps deployment size under Vercel's free tier limits
5. **AI SDK over raw API** — the `@google/generative-ai` SDK handles retries, streaming, and error normalization
