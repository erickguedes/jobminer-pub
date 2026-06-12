# Features

> *Screenshots coming soon.*

---

## 1. Dashboard

Central view of the user's job search progress:

- **Pipeline summary cards** — visual count per status (New → Not Applied → Applied → Interview Scheduled → In Process → Offer → Accepted → Rejected), each color-coded
- **Activity heatmap** — GitHub-style contributions graph showing daily application activity over 12 months
- **Monthly analytics chart** — bar/line chart comparing applications, responses, and interviews per month
- **Recent opportunities** — last 5 updated entries with status badges and quick actions
- **Quick stats** — "7 active applications · 2 interviews this week · 1 offer"

## 2. Opportunity Management

### List View
- Sortable table with company, job title, status, and dates
- Search by company name, job title, or description
- Filter by pipeline status
- Column sorting (updated date, company, status)

### Detail View (Tabbed)
Each opportunity has a workspace with tabs:

| Tab | Content |
|---|---|
| **Overview** | Job info, company link, status change dropdown, status history timeline |
| **Analysis** | AI compatibility analysis with model attribution |
| **CV** | Editable markdown preview of AI-generated resume, PDF/DOCX download |
| **Cover Letter** | Editable AI-generated cover letter, PDF/DOCX download |
| **Salary** | AI salary suggestion with market context |
| **Questions** | AI-generated interview questions by category (behavioral, technical, experience) |

### Unified Creation Form
One form to create a company + opportunity simultaneously:
- Company dropdown with search
- "+ New Company" option that expands inline fields
- Job details, description, link, salary expectation
- Language selector (en, pt-BR, es)

## 3. AI Processing

One-click AI analysis that:
1. Reads the job description against the user's profile
2. Generates a compatibility analysis with match percentage
3. Produces a tailored resume highlighting relevant experience
4. Writes a professional cover letter
5. Suggests a fair salary range based on role, seniority, company size, and market

**Fallback chain** ensures processing continues even if the primary AI model is rate-limited:
`gemini-2.5-flash → gemini-2.5-pro → gemini-2.0-flash → gemini-2.0-flash-lite`

## 4. Resume Configuration

Structured profile editor based on a JSON schema that supports any profession:

- **Personal info** — name, titles, contact, website, Calendly
- **Availability** — work preference, relocation, travel, driver's license
- **Professional summary**
- **Skills** — categorized groups (e.g., "Backend": ["Python", "Node.js"])
- **Experience** — with dates, location, current job flag, context, and bullet points
- **Education** — degrees, institutions, years
- **Certifications** — grouped by category
- **Languages** — with proficiency levels
- **Extra context** — target roles, keywords, additional notes
- **CTA configuration** — call-to-action for PDF footer

## 5. Company Intelligence

- Company CRUD with notes and website
- **AI company analysis** — generates sector, size, products, technologies, and HQ location
- **Contacts** — per-company contact list (name, role, email, LinkedIn)
- Related opportunities listed on the company detail page

## 6. Analytics

- **Activity timeline** — GitHub-inspired heatmap showing consistency
- **Monthly trends** — track applications, responses, interviews over time
- **Pipeline distribution** — see where opportunities are concentrated in the funnel

## 7. Productivity Tools

### Saved Search Links
Bookmark job board searches with labels and tags:
```
Label: "Remote Senior SWE — Europe"
URL: linkedin.com/jobs/search/?keywords=senior+software+engineer&f_WT=2
Tags: [LinkedIn, Remote]
```

### Message Templates
Pre-written networking messages with `{{variable}}` tags:
```
"Hi {{name}}, I saw the {{role}} opening at {{company}}..."
Tags: [LinkedIn Connection, Follow Up, Profile Visit]
```

## 8. Document Export

Every generated document can be exported in two formats:

| Format | Use Case |
|---|---|
| **PDF** | Ready-to-submit, professional layout with brand colors and typography |
| **DOCX** | Editable in Word/Google Docs — user can make adjustments before submitting |

## 9. User Experience

- **Dark mode** — follows system preference
- **Responsive** — desktop-first with functional mobile layout
- **Empty states** — helpful messages when no data exists
- **Loading skeletons** — animated placeholders during data fetch
- **AI processing states** — model name displayed, fallback notifications
- **Toast notifications** — success/error feedback via sonner
- **Authentication** — Google or LinkedIn login via Supabase Auth

---

## Planned Features

- Admin analytics dashboard (user growth, feature usage, AI call metrics)
- Cookie consent banner (LGPD/GDPR compliance)
- Multiple resume versions per user
- Collaborative opportunity sharing
- Browser extension for one-click job saving
