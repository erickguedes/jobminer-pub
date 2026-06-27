# Job Miner OS

[![Live Demo](https://img.shields.io/badge/demo-jobminer.erickguedes.com-blue?style=flat&logo=vercel)](https://jobminer.erickguedes.com)
[![Stack: TanStack Start](https://img.shields.io/badge/stack-TanStack%20Start-cyan?style=flat&logo=react)](https://github.com/erickguedes/jobminer-pub)
[![AI: Google Gemini](https://img.shields.io/badge/AI-Google%20Gemini-4285F4?style=flat&logo=google)](https://deepmind.google/gemini)
[![DB: Supabase](https://img.shields.io/badge/db-Supabase%20PostgreSQL-3ECF8E?style=flat&logo=supabase)](https://supabase.com)

**An AI-powered Career CRM** — a full-stack SaaS platform that transforms chaotic job hunting into an organized, data-driven pipeline. Built for candidates who want to be intentional about their next move.

---

## The Problem

Job hunting is fragmented. A typical professional juggles:

- **10–30+ active applications** across different companies and stages
- **Tailored resumes** for each role (no two job descriptions are the same)
- **Cover letters** that require research and adaptation
- **Salary research** — knowing what to ask for at each company
- **Interview prep** specific to each role and company
- **Networking follow-ups** that are easy to drop

Existing tools fall short: **ATS platforms** serve recruiters, not candidates. **Spreadsheets** are manual and lack intelligence. There was no dedicated workspace for *the job seeker*.

## The Solution

Job Miner is a **single, unified workspace** that manages your entire job search. It combines pipeline tracking, AI-powered content generation, and document export into one platform — so you spend less time on admin and more time on interviews.

```yaml
What it does:
  Track    : Opportunities, companies, contacts, and pipeline stages
  Analyze  : AI reads job descriptions against your profile for fit analysis
  Generate : Tailored resumes, cover letters, salary suggestions, interview questions
  Export   : PDF (ready to submit) and DOCX (editable in Word/Google Docs)
  Learn    : Analytics dashboard with heatmaps and monthly trends
```

## Key Features

| Capability | Detail |
|---|---|
| **Pipeline tracking** | Visual kanban: New → Applied → Interview → Offer → Accepted/Rejected |
| **AI job-fit analysis** | Gemini-powered, 4-model automatic fallback chain |
| **Tailored resume gen** | Per-job description, structured JSON → PDF + DOCX |
| **Cover letter gen** | Professional tone, complete letter + PDF/DOCX export |
| **Salary suggestions** | Role + seniority + company size + market data |
| **Company intelligence** | AI sector/size/tech analysis per company |
| **Interview questions** | Behavioral, technical, and experience-based categories |
| **Activity heatmap** | GitHub-style contributions graph for your search |
| **Monthly analytics** | Applications, responses, interviews over time |
| **Message templates** | `{{variable}}` tags for networking messages |
| **Saved search links** | Bookmark job board searches with tags & labels |
| **Resume upload + parse** | Upload PDF/DOCX → AI extracts and auto-fills your profile |
| **Dark mode** | System preference detection |

## AI Architecture

The AI layer uses a **4-model fallback chain** for resilience:

```
Primary:  gemini-2.5-flash      ← fastest, handles ~90% of requests
Fallback: gemini-2.5-pro        ← higher quality when flash rate-limits
          gemini-2.0-flash      ← fallback for capacity
          gemini-2.0-flash-lite ← last resort
```

Each request (analysis, resume, cover letter, salary, questions) routes through this chain. If a model is rate-limited, the next model in line handles it transparently. The user sees which model served their result.

## Why These Tech Choices

| Decision | Rationale |
|---|---|
| **TanStack Start over Next.js** | Same capability, more modular. First-class TypeScript inference for routes, params, and loaders without config boilerplate. |
| **Supabase over custom backend** | PostgreSQL + Auth + Storage in one service. RLS enforces multi-tenant isolation at the DB level — every user sees only their own data. |
| **Gemini over OpenAI** | ~10x cheaper per token, 1M-token context window, comparable quality for structured text generation. |
| **@react-pdf/renderer** | PDF generation without Chromium (~200ms vs ~3s Playwright). No cold start on serverless, stays under Vercel free-tier limits. |
| **Serverless + Vercel** | Zero infra management. Single deploy for frontend + API + SSR. Automatic scaling. |

## Live Demo

Try it yourself: **[jobminer.erickguedes.com](https://jobminer.erickguedes.com)**

> The demo is pre-populated with 40 Brazilian companies, 100+ opportunities, sample analysis results, saved searches, and message templates — so you can explore every feature without setting up your own data.

## Repositories

- [**jobminer**](https://github.com/erickguedes/jobminer) *(private)* — Full application source code
- [**jobminer-pub**](https://github.com/erickguedes/jobminer-pub) *(this repo)* — Public portfolio and documentation

## What's Next

- Admin dashboard (user metrics, feature usage, AI call analytics)
- Cookie consent (LGPD/GDPR compliance)
- Multiple resume versions per user
- Browser extension for one-click job saving
- Collaborative opportunity sharing

---

*Built with TypeScript, React 19, TanStack Start, Supabase PostgreSQL, and Google Gemini. Deployed on Vercel. Designed for job seekers who take their search seriously.*
