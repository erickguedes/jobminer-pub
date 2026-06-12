# Job Miner OS

**Your Career Command Center.** An AI-powered Career CRM that helps professionals organize job applications, track opportunities, manage networking activities, and optimize resumes throughout their career journey.

---

## The Problem

Job hunting is a fragmented, stressful process. Professionals manage dozens of applications simultaneously — each requiring:
- A tailored resume adapted to the role
- A cover letter that stands out
- Salary research for negotiation
- Interview preparation
- Pipeline tracking across companies

Existing tools are either **recruiter-side ATS** (not built for candidates) or generic spreadsheets. There was no dedicated workspace for *the candidate*.

## The Solution

Job Miner centralizes the entire job search workflow into a single platform:

1. **Track opportunities** across companies with a visual pipeline (new → applied → interview → offer → accepted/rejected)
2. **AI-powered analysis** that reads job descriptions against your profile and generates compatibility analysis, tailored resumes, cover letters, and salary suggestions
3. **Document generation** with both PDF (for submission) and DOCX (for editing) formats
4. **Analytics dashboard** with activity heatmaps and pipeline statistics to visualize your job search progress
5. **Networking tools** including saved search links and message templates with tags

---

## Tech Stack at a Glance

| Layer | Technology |
|---|---|
| Frontend + API | TanStack Start (React, SSR, Nitro) |
| Database | Supabase PostgreSQL |
| Authentication | Supabase Auth (Google + LinkedIn) |
| File Storage | Supabase Storage |
| AI Engine | Google Gemini API (4-model fallback chain) |
| PDF Generation | @react-pdf/renderer |
| DOCX Generation | docx (npm) |
| Hosting | Vercel |
| CI/CD | GitHub Actions |

---

## Key Features

- **Unified company + opportunity creation** — one form, no context switching
- **AI job-fit analysis** with automatic fallback across 4 Gemini models
- **Personalized resume adaptation** per job description
- **Cover letter generation** with professional tone
- **Salary suggestion** based on role, seniority, company size, and market
- **Company intelligence** — AI-powered sector, size, and technology analysis
- **Interview question generator** tailored to the role and your profile
- **Pipeline tracking** with visual status board
- **Activity heatmap** — GitHub-style contributions graph for your job search
- **Monthly analytics** — applications, responses, interviews over time
- **Saved search links** — bookmark job boards and searches
- **Message templates** with tag variables for networking
- **PDF + DOCX export** — professional formatting, editable documents
- **Dark mode** — light/dark system preference

---

## Repositories

- [**jobminer**](https://github.com/erickguedes/jobminer) (private) — application source code
- [**jobminer-pub**](https://github.com/erickguedes/jobminer-pub) (public) — this portfolio overview

---

*Built with TypeScript, React, Supabase, and Google Gemini. Deployed on Vercel.*
