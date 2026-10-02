# TA AI Solutions Website: Handoff Document

Prepared 2 October 2026 for whoever (human or AI) continues this project.
Everything needed to understand, edit, and publish the site is in this file plus the repository itself.

---

## 1. Project summary

**What it is:** A public, static showcase website for the AI solutions built by and for the Talent Attraction (TA) team. It has a landing page and one detail page per solution. Visitors need no login.

**Owner:** Sam Prieto, sprieto@degreed.com. GitHub username `samprieto`.

**Live URL:** https://samprieto.github.io/ta-ai-solutions/

**Repository:** https://github.com/samprieto/ta-ai-solutions (public, branch `main`, GitHub Pages serving from `/ (root)`)

**Stack:** Plain HTML and CSS. No framework, no build step, no JavaScript beyond tiny inline `onerror` handlers on screenshot images. Each page is fully self-contained (CSS inline in a `<style>` block). Only external dependency: Google Fonts (Inter).

**Design inspiration:** degreedlabs.com, but in a light/clean style rather than dark.

---

## 2. Repository file inventory

```
ta-ai-solutions/
├── index.html                      Landing page
├── solution-northstar.html         NorthStar detail page (indigo accent)
├── solution-quickslot.html         QuickSlot detail page (cyan accent)
├── solution-language-fluency.html  Language Fluency detail page (emerald accent)
├── solution-scout.html             Scout detail page (teal accent)
├── solution-skill-scanner.html     Skill Scanner detail page (sky blue accent)
├── solution-template.html          Blank template for future solutions (reference only, not linked from the site)
├── favicon.svg                     Teal gradient rounded square with white "TA"
├── screenshots/
│   ├── northstar-1.png             Org chart + scenario impact dashboard (wide)
│   ├── northstar-2.png             Leader profile card (tall, narrow)
│   ├── quickslot-1.png             Candidate "Interview Availability" page with timezone prompt
│   ├── quickslot-2.png             Weekly availability grid with green blocks
│   ├── quickslot-3.png             Candidate Availability Summary card
│   ├── language-fluency-1.png      "Before you record" instructions card
│   ├── language-fluency-2.png      Recording screen (timer, waveform, stop button)
│   ├── scout-1.png                 "New Search" form (tall)
│   └── scout-2.png                 "Current Pipeline" progress view (wide)
├── solution-intake-prompt.md       Prompt Sam pastes into an AI to document a new solution with minimal input
├── README.md                       GitHub Pages deploy guide (generic, somewhat outdated; see section 11)
└── HANDOFF.md                      This file
```

Skill Scanner has no screenshots yet. Its three slots show "Screenshot coming soon".

---

## 3. How to publish changes

GitHub's API (`api.github.com`) was blocked from the previous AI's sandbox, so all publishing was done with plain `git` over HTTPS using a Personal Access Token embedded in the remote URL. `github.com` itself was reachable.

```bash
git clone https://samprieto:<TOKEN>@github.com/samprieto/ta-ai-solutions.git
cd ta-ai-solutions
git config user.email "sprieto@degreed.com"
git config user.name "Sam Prieto"
# edit files
git add -A
git commit -m "Describe the change"
git push
```

GitHub Pages redeploys automatically within 1 to 3 minutes of each push. A hard refresh (Cmd+Shift+R) may be needed to see favicon or CSS changes.

**Token:** Sam has a GitHub Personal Access Token (classic, `ghp_...`) with repo scope. It is deliberately not written in this file because the file lives in a public repository. Ask Sam for it. It was shared in a chat transcript earlier, so Sam may want to revoke it and issue a new one.

**Working-directory tip for sandboxed AIs:** cloning into a mounted/synced folder caused `.lock` file errors in the previous environment. Clone into a plain temp directory (e.g. `/tmp`) and copy files in.

---

## 4. Global design system

### 4.1 Typography and base
- Font: `'Inter', system-ui, sans-serif` from Google Fonts (weights 300 to 800)
- Body font-size 15px (solution pages) / default (index). Line-height 1.6
- Headline letter-spacing is tight (`-.02em` to `-.03em`), weight 800

### 4.2 Core CSS variables (index.html and shared by all pages)
```css
--bg: #ffffff;        --bg-subtle: #f7f8fa;
--border: #e8eaed;    --border-hover: #c2c7cf;
--text-primary: #111827;  --text-secondary: #6b7280;  --text-muted: #9ca3af;
--radius: 14px;
--shadow-sm / --shadow-md / --shadow-lg: soft black shadows at 4 to 10 percent opacity
```

### 4.3 Site accent (index.html, nav logo, favicon)
```css
--accent: #0d9488;       /* teal */
--accent-hover: #0f766e;
--accent-3: #2dd4bf;
--accent-light: #f0fdfa;
```
Logo: 34px rounded square (radius 9px), `linear-gradient(135deg, var(--accent), var(--accent-3))`, white "TA" at weight 800.

### 4.4 Per-solution accent colours
Each solution page overrides the accent variables in its own `:root`. The landing-page card uses a matching `.theme-*` class.

| Solution | Card theme class | --accent | --accent-3 | --accent-light | Card icon |
|---|---|---|---|---|---|
| NorthStar | `theme-indigo` | `#4f46e5` | `#818cf8` | `#eef2ff` | 🧭 |
| QuickSlot | `theme-cyan` | `#0891b2` | `#06b6d4` | `#ecfeff` | 📅 |
| Language Fluency | `theme-emerald` | `#059669` | `#34d399` | `#ecfdf5` | 🎙️ |
| Scout | `theme-teal` | `#0d9488` | `#2dd4bf` | `#f0fdfa` | 🔍 |
| Skill Scanner | `theme-sky` | `#0284c7` | `#38bdf8` | `#f0f9ff` | 🎧 |

Unused theme classes still defined in index.html: `theme-rose` (`#e11d48`), `theme-amber` (`#d97706`, formerly Quest Keeper).

### 4.5 Layout patterns
- Max content width 1100px, centred
- Nav: sticky, frosted glass (`rgba(255,255,255,.88)` + `backdrop-filter: blur(14px)`), 64px tall, bottom border
- Solution pages: two-column body. `main.main-content` on the left, `aside.sidebar` on the right (sticky). Collapses to one column on mobile
- Cards: white background, `1.5px solid var(--border)`, `border-radius: var(--radius)`
- Section headings on solution pages: `h2.section-title`, some pages draw a short accent bar via `::before`

### 4.6 Responsive
Breakpoint around 640 to 900px depending on page. Grids collapse to one column; nav padding shrinks.

---

## 5. Landing page (index.html) current content

**`<title>`:** TA AI Solutions

**Nav:** Logo "TA" + "TA AI Solutions" (links to index.html). One link "AI Solutions" (anchor `#solutions`). A "Get in Touch" button exists in the markup but is commented out / hidden.

**Hero**
- H1 (plain black, two lines): `Talent Attraction<br>AI Solutions`
- Button: "Explore Solutions" → `#solutions`
- Stats row:
  - **2** Solutions Deployed
  - **3** In Development
  - **~$34K** Est. Annual Cost Savings

> Note: the ~$34K figure was derived from the enterprise-comparison savings on QuickSlot (~$16.4K) and Language Fluency (~$18.3K) when those sections still showed savings math. That math has since been removed from the pages. Sam has been asked whether to keep this stat; no decision yet.

**Value strip (3 items)**
1. ⚡ **Built In-House**: No vendor lock-in. Every solution is owned, maintained, and evolved internally.
2. 🚀 **Built to Scale**: Designed and built to enable and scale the business for growth, positioning TA as a strategic partner.
3. 🔒 **Secure by Design**: Built with security and compliance perimeters from day one.

(A fourth item, "Cost-Conscious", was removed on request.)

**Solutions grid**: heading "AI Solutions". No subtitle. Cards in this order, each linking to its page, no status or date stamps, arrow icon bottom-right:

| Order | Name | Tag | Card description |
|---|---|---|---|
| 1 | NorthStar | Business & Workforce OS | The business intelligence layer that transforms strategy into the organization, capabilities, and talent required to win. |
| 2 | QuickSlot | Workflow | Generate live candidate availability links without calendar permissions, manual coordination, or scheduling back-and-forth. |
| 3 | Language Fluency | Skill Assessment | A browser-based fluency assessment: candidates record a response to a standardized prompt with zero third-party storage and full data privacy compliance. |
| 4 | Scout | Sourcing | Autonomously searches public web data to find and rank the best-fit candidates for any role. No manual searching required. |
| 5 | Skill Scanner | Skill Assessment | A voice-based AI interviewer that assesses candidates on up to five role-specific skills and delivers a scored evaluation report, automatically, in 30 minutes. |

**Contact section**: exists in markup, `style="display:none"`. Contains a "Get in Touch on GitHub" button linking to `https://github.com/samprieto/ta-ai-solutions/issues/new?title=Getting+in+Touch&body=Hi+Sam%2C%0A%0A`.

**Footer:** Logo + "TA AI Solutions" (links home) · "© 2026 TA AI Solutions"

---

## 6. Solution page structure (common to all)

Top to bottom:

1. **Sticky nav**: `TA AI Solutions › [Solution name]` on the left (TA AI Solutions links home; the solution name is a plain span in `.nav-sol`), "← Back to AI Solutions" on the right. Stays frozen at top while scrolling.
2. **Hero**: breadcrumb (`TA AI Solutions` link › category), category tag pill, H1 solution name, one-sentence description (`.hero-desc`). **No** status pill, **no** date, **no** Open/Preview button (all removed on request).
3. **Body, left column (`main`)** in this order:
   - **What it does**: `The problem:` paragraph, `The solution:` paragraph, checkmark feature list
   - **See It in Action**: screenshot grid (`.shots`). Each `<figure class="shot">` holds an `<img>` whose `onerror` removes the image and adds class `missing`, which renders the text "Screenshot coming soon". So slots degrade gracefully when a file is absent.
   - **Business Impact**: Before / After two-card grid, then impact bullet list
   - (Skill Scanner only) **Beyond Hiring** vision callout
   - **Tech Stack** (NorthStar instead has **Strategic Value** and **Data & Integrations**)
4. **Body, right column (`aside.sidebar`)**:
   - **Key Metrics** card: 2-cell grid (NorthStar: 6 cells)
   - **Enterprise Comparison** card (not on NorthStar): a 3-row table of comparable products. The Avg cost / Our run cost / Estimated savings summary was removed from all pages.
   - **Removed on request**: Status card, Cost Breakdown table, Links card
5. **Footer**: same as index.

Screenshot grid variants:
- Default `.shots`: 2 columns, first image spans full width (used by QuickSlot: 3 images)
- `.shots.two`: 2 equal columns (Language Fluency: 2 images)
- `.shots.stack`: single column, first image constrained to 640px (Scout: 2 images)
- NorthStar `.shots.stack`: single column, second image constrained to 360px (tall profile card)

---

## 7. Per-solution content (verbatim as currently published)

### 7.1 NorthStar (solution-northstar.html)

- **Category:** Business & Workforce OS
- **Hero description:** The business intelligence layer that transforms strategy into the organization, capabilities, and talent required to win.
- **Status (not shown on page):** Conceptual / in development. No live link.
- **Tone directive from Sam:** business-intelligence voice throughout; the product unifies company BI so leaders can build the right talent to deliver business outcomes.

**What it does**

The problem: The data leaders need to build the right workforce lives in disconnected systems: strategy in presentations, people in the HRIS, budgets in Finance models, skills in learning platforms, and hiring in the ATS. Leaders define ambitious business goals but lack a single, trusted view of whether they have the capabilities, skills, structure, budget, and talent required to deliver the business outcomes.

Without connected business intelligence, fundamental questions are surprisingly hard to answer: Do we have the capabilities required to deliver our strategy? Where are our biggest workforce gaps? Is our organization structured effectively? What will our workforce plan cost? What happens if we restructure a team, move roles, invest in a new capability, or change our hiring plan?

The solution: NorthStar is a Business & Workforce Operating System that unifies a company's business intelligence across strategy, organization, skills, finance, and talent into one integrated platform. Leaders start with where the business is going, and NorthStar turns that data into decision intelligence: the capabilities, skills, structure, workforce investment, and talent strategy required to deliver business outcomes.

Core capabilities (10):
- Translate business goals and outcomes into the organizational capabilities and workforce needs required to deliver them
- Visualize the organization through interactive org charts enriched with people, skills, cost, span of control, and workforce analytics
- Quantify current vs. future capability and skills gaps with data, not opinion
- Model future organizational structures through a drag-and-drop workforce sandbox
- Measure the real-time impact of organizational changes on headcount, payroll, spans, layers, skills, capabilities, and risk
- Model workforce budgets, positions, hiring plans, and financial forecasts against business targets
- Compare workforce scenarios across cost, capability, structure, talent, and hiring feasibility
- Understand individual and team capabilities through role-based skills analytics
- Close the loop from workforce plan to positions, requisitions, sourcing, assessment, and hiring execution, and track results against the plan
- Use NorthStar AI to surface risks, opportunities, scenarios, and insights across the organization's combined data

**See It in Action:** northstar-1.png (org chart + scenario impact), northstar-2.png (leader profile).

**Business Impact**

Before: Business strategy, workforce planning, organizational design, skills, financial planning, and recruiting run on disconnected data. Leaders stitch together spreadsheets, presentations, HR systems, Finance models, and ATS reports by hand, and the answers are stale by the time they arrive. / Workforce planning becomes a headcount budgeting exercise rather than a strategic discussion about the capabilities needed to hit business goals. Organizational changes are judged on headcount and cost alone, with limited visibility into skills, capabilities, structure, talent risk, and future hiring needs.

After: NorthStar creates a single source of truth where executives, business leaders, Finance, People, and Talent teams plan the organization together. Business goals flow through to capabilities, skills, organization, positions, people, investment, and talent strategy, with every decision grounded in shared data. / Leaders can model decisions before making them and immediately see the impact on cost, capability, structure, and risk. The result is a different workforce-planning conversation, driven by insight rather than instinct. Not simply "How many people can we afford?" but "What organization and capabilities do we need to execute our strategy, and what is the smartest way to build them?"

(No impact bullet list on this page.)

**Strategic Value** (6 cards)
- For Executives: Connect business strategy and outcomes to organizational capability and workforce investment.
- For Leaders: Design teams, see capability gaps, model changes, and make data-driven organizational decisions.
- For Finance: Connect headcount, positions, compensation, hiring forecasts, workforce scenarios, and budget.
- For People / HR: Understand organizational structure, skills, capabilities, internal mobility, succession, and workforce risk.
- For Talent Acquisition: Translate approved workforce plans directly into executable hiring strategies.
- For Employees: Create greater visibility into skills, development opportunities, career paths, and internal mobility.

**Data & Integrations**
Intro: NorthStar unifies the business intelligence already spread across the systems companies use, turning it into one decision-ready view.
Cards: HRIS (People · Organization · Positions · Compensation); ATS (Requisitions · Candidates · Pipelines · Hiring outcomes); Finance (Budgets · Forecasts · Cost centers · Workforce investment); Skills & Learning (Skills · Proficiency · Development · Learning); Compensation Intelligence (Market benchmarks · Geographic differentials · Salary ranges); Business Systems (Goals · KPIs · Revenue · Productivity · Business outcomes).
Note: NorthStar becomes the decision-intelligence layer connecting these systems, rather than requiring any of them to be replaced.

**Sidebar Key Metrics** (product metrics, not ROI; Sam explicitly did not want invented ROI figures)
Workforce Investment / Real-time cost & forecast · Capability Coverage / Current vs. future needs · Organization Health / Spans, layers & structure · Workforce Plan / Current vs. future HC · Talent Supply / Internal + external · Execution / Plan → position → hire. Footnote: "What NorthStar enables organizations to manage."

**Removed from the original NorthStar brief on request:** Product Stories section (6 stories + "Ask NorthStar AI" questions), Intelligence Model flow diagram, and the closing "Build the organization your strategy requires" statement. The original brief text is preserved in Appendix A in case it is wanted later.

### 7.2 QuickSlot (solution-quickslot.html)

- **Category:** Workflow · **Live** since April 2026 (status not shown on page)
- **Live app (not linked on page):** https://schedule.degreedlabs.com/
- **Hero description:** Generate live candidate availability links without calendar permissions, manual coordination, or scheduling back-and-forth.

The problem: Interview scheduling is one of the most repetitive and time-consuming workflows in recruiting. Recruiters spend significant time coordinating availability, converting timezones, following up with candidates, and manually managing scheduling logistics across multiple stakeholders.

The solution: QuickSlot gives recruiters a lightweight way to generate live availability links that candidates can update in real time. Recruiters can suggest interview times, manage timezone conversion automatically, batch-manage links, and view structured availability summaries, all without collecting private calendar data or requiring permissions or integrations.

Features: Generate individual or batch candidate availability links in seconds · Allow candidates to update availability dynamically through a live self-service workflow · Automatically convert availability and suggested interview times across recruiter and candidate timezones · Manage individual or batch candidate scheduling workflows from a centralized recruiter view

Screenshots: quickslot-1/2/3.png

Before: Recruiters manually coordinated interview availability through email threads, Slack messages, spreadsheets, timezone conversions, and repeated follow-ups. Scheduling coordination often required multiple touchpoints per candidate and created unnecessary operational overhead across the hiring process.

After: Recruiters now generate live availability links in seconds while candidates self-manage scheduling asynchronously. Suggested interview times, timezone handling, and availability updates happen automatically through a centralized workflow.

Impact bullets: Saves approximately 350 recruiter hours annually across the team · Approximately $13,700 in annual recruiter capacity value · Reduces manual scheduling coordination and timezone conversion errors · Improves the candidate experience: candidates share availability on their own time and in their own timezone, update it anytime through the same link, and never need an account or to grant calendar access · Enables scalable batch scheduling workflows for high-volume recruiting

Tech Stack chips: Lovable, React, TypeScript, Supabase, Vercel, Tailwind CSS. Note: Designed to avoid calendar integrations, private data collection, and permission dependencies while still enabling live scheduling workflows.

Key Metrics: **350 hrs** saved / year · **$13,700** Est. saved value / yr

Enterprise Comparison: GoodTime Hire (GoodTime) Enterprise interview scheduling ~$14K–22K/yr · Prelude (Calendly) Recruiting scheduling automation ~$15K–30K/yr · Calendly Teams (Calendly) Team scheduling coordination ~$7K–15K/yr

### 7.3 Language Fluency (solution-language-fluency.html)

- **Category:** Skill Assessment · **Live** since May 2026
- **Live app (not linked on page):** https://degreed-ta.github.io/degreed-english-assessment/
- **Hero description:** A browser-based fluency assessment: candidates record a response to a standardized prompt with zero third-party storage and full data privacy compliance.

The problem: Confirming a candidate's English fluency used to require coordinating availability, scheduling, and running a screening call, only to discover, sometimes 20 or more minutes in, that the level wasn't where the role needed it to be. That cycle burned recruiter time on every applicant regardless of whether they could realistically move forward.

The solution: Language Fluency is a single-page web app hosted free on GitHub Pages. The candidate receives a link in their Greenhouse outreach email, opens it, reads a standardized prompt in the language being assessed, and records a response of up to 5 minutes directly in the browser. The audio is generated locally, previewed by the candidate, downloaded to their device, and re-uploaded to their Greenhouse application, where the recruiter and hiring manager can listen asynchronously before deciding whether to invest interview time.

Features: Branded interface with a fixed prompt and a 5-minute soft cap on response length · Records audio entirely in the candidate's browser memory: no server, no database, no third-party storage at any point in the flow · Step-by-step submission guidance that updates as the candidate progresses (record, preview, download, upload to Greenhouse) · Editable in minutes: prompts, branding, and timing can all be updated by replacing one HTML file in the repository · Scalable to any language: updating the prompt and interface language is a one-line edit, at no additional cost

Screenshots: language-fluency-1/2.png (grid class `shots two`)

Before: English fluency was assessed during a live screening interview, which meant the team invested in availability coordination, scheduling, and a 30+ minute call before learning whether the candidate's English met the bar, burning recruiter capacity on candidates who couldn't move forward.

After: Candidates self-serve a 5-minute standardized assessment before any live screen. Recruiters and hiring managers review the audio asynchronously, advancing only candidates who meet the language bar to a full screening call.

Impact bullets: Improves the candidate experience: candidates complete the assessment on their own schedule, from any browser, with no account, no scheduling, and no live-screen pressure · In its first deployment (Senior TA Partner role), 7 candidates were invited and 90% completed the assessment, a strong signal that the candidate experience works · Saves an estimated approximately 30 minutes of recruiter time per candidate by replacing scheduled language screens with async audio review (estimated) · Eliminates data privacy exposure entirely: candidate audio never touches a third-party server · Available to the entire TA team for any role going forward, with no per-seat or per-use cost

Tech Stack chips: HTML5, Vanilla JavaScript, CSS, MediaRecorder API, GitHub Pages. Note: No backend, no database, no AI APIs. The MediaRecorder API is built into every modern browser, so audio is generated and held in the candidate's local browser memory until they choose to download it. That's what makes the solution both free to run and privacy-compliant by design.

Key Metrics: **~30 min** saved per candidate screened · **TBD** Est. saved value / yr

Enterprise Comparison: HireVue (HireVue Inc.) Enterprise async video and audio interviewing with AI assessment ~$35K–50K/yr · VidCruiter (VidCruiter Inc.) Recruitment suite with structured async video and audio interviews ~$5K–10K/yr · Spark Hire (Spark Hire) Mid-market one-way video/audio interview platform ~$3.6K–6K/yr

Small copy wart to consider fixing: "Saves an estimated approximately 30 minutes" (double hedge).

### 7.4 Scout (solution-scout.html)

- **Category:** Sourcing · **In Development**, expected June 2026
- **Preview app (not linked on page):** https://profile-sourcing.lovable.app/app?co=90a60d730af94f3c880cfc609bce1e9fb578649f2d882c99
- **Hero description:** Autonomously searches public web data to find and rank the best-fit candidates for any role. No manual searching required.

The problem: Sourcing candidates for a new role requires recruiters to manually build searches, review hundreds of profiles, and compile a shortlist. This process is time-consuming, inconsistent across team members, and hard to scale when multiple roles are open simultaneously.

The solution: A recruiter enters a role title and location, and Scout automatically generates targeted search queries, runs them across publicly available web data in parallel, and uses Claude AI to score and rank each candidate profile for fit. The result is a prioritized shortlist delivered in minutes, with a written reason for every score.

Features (bold lead + text): Natural language input: enter any role title and location to launch a sourcing run instantly · AI-generated search queries: Claude creates multiple targeted search angles tailored to the role · Broad public web search: scans publicly available professional data across the web simultaneously via Tavily API · Intelligent candidate scoring: Claude Haiku scores each profile 1 to 5 with a written fit rationale · Real-time pipeline tracking: live progress view showing Analyze, Search, Score, and Done phases

Screenshots: scout-1.png (New Search form), scout-2.png (Current Pipeline) (grid class `shots stack`)

Before: Recruiters manually built searches, reviewed profiles one by one across multiple platforms, and compiled shortlists by hand. This process required significant time and produced results that varied based on individual skill and effort.

After: Data collection in progress. This section will be updated once Scout is fully deployed.

Impact bullets: Consistent AI scoring methodology applied to every candidate on every search, reducing individual bias in the shortlisting process · Frees recruiter time from manual search mechanics so it can be reinvested in candidate engagement and hiring manager partnership · Time savings per search: data collection in progress, will be updated post-launch

Tech Stack chips: React, TanStack Start, Cloudflare Workers, Supabase, Tavily API, Claude (Haiku + Sonnet), Lovable. Note: Pipeline runs in Cloudflare Workers background execution. All database and API calls use native AbortSignal.timeout() to ensure reliability in serverless edge contexts.

Key Metrics: **TBD** hrs saved / sourcing run · **TBD** Est. saved value / yr

Enterprise Comparison: SeekOut (SeekOut Inc.) AI talent intelligence platform that autonomously sources and ranks candidates ~$40,000/yr · HireEZ (HireEZ Inc.) AI outbound sourcing platform that finds candidates across 45+ data sources ~$13,000/yr · Findem (Findem Inc.) Agentic AI sourcing platform that discovers and ranks candidates from 100M+ public profiles ~$27,000/yr

### 7.5 Skill Scanner (solution-skill-scanner.html)

- **Category:** Skill Assessment · **In Development**, pilot expected June 2026 (internal pilot targeting June 10, 2026). No public link.
- **Hero description:** A voice-based AI interviewer that assesses candidates on up to five core role-specific skills, delivers a scored evaluation report automatically in 30 minutes.

The problem: Traditional skill screening requires recruiters to manually schedule, conduct, and score phone or video screens for every candidate. This process takes 60 to 90 minutes per person and introduces inconsistency across interviewers and roles.

The solution: Recruiters configure up to five essential skills for a role by uploading a Job Ad or Job Description, then set a minimum pass score. Candidates complete a fully automated 30-minute voice conversation with an AI interviewer. When the session ends, Skill Scanner processes the live transcript to generate a skill-by-skill evaluation report with AI-generated feedback and a total score, requiring no recruiter time during the assessment itself.

Features: Skill configuration console: recruiters upload a Job Ad or Job Description to automatically extract and define up to 5 role-specific skills, with scoring on a 1 to 5 scale and a configurable pass/fail threshold · Voice-based AI interviewing: candidates engage in a real-time, two-way spoken conversation powered by LiveKit, capped at 30 minutes to reduce candidate friction · Automated transcript scoring: the system analyzes the full conversation and produces a structured skill-by-skill evaluation with AI-generated feedback and a total score

Screenshots: none yet; 3 slots show "Screenshot coming soon" (expects skill-scanner-1/2/3.png)

Before: Recruiters spent 60 to 90 minutes per candidate on manual skill screens: scheduling calls, conducting the interview, taking notes, and writing up a score, with little consistency across interviewers and roles.

After: Data collection in progress. This section will be updated once the solution is fully deployed.

Impact bullets: Estimated time savings: TBD, will be updated once the solution is fully deployed. · Improves the candidate experience: candidates take the interview on demand, without waiting for recruiter availability, and receive a consistent, fair evaluation · Standardizes skill evaluation across all candidates and roles with consistent scoring criteria and AI-generated rubrics · Frees recruiters to focus on high-judgment work like offer conversations and stakeholder management

Beyond Hiring callout: Skill Scanner is designed to extend well beyond the hiring decision. When a candidate is hired, their skills have already been mapped and assessed during the hiring process. From day one, the new hire will have a personalized growth pathway ready, based on the gaps and strengths identified during their assessment. Onboarding becomes smarter, development starts immediately, and employees hit the ground running with a clear picture of where they are and where they are going.

Tech Stack chips: Claude (Anthropic), LiveKit, Azure App Services. Note: Claude powers both the real-time voice conversation logic and the post-session transcript evaluation. LiveKit handles the real-time audio layer. Azure App Services hosts the application via internal DevOps infrastructure.

Key Metrics: **TBD** hrs saved / month · **TBD** Est. saved value / yr

Enterprise Comparison card: shows placeholder text "TBD".

---

## 8. Content and style rules Sam has set (follow these)

1. **No em-dashes (—) anywhere.** Use commas, colons, periods, or `|` instead. Sam has asked for this repeatedly.
2. **"Talent Attraction"**, not "Talent Acquisition", in all copy. (Exception: the "For Talent Acquisition" card on NorthStar came from Sam's own brief and was not flagged; consider confirming.)
3. **No mentions of "Degreed"** in visible text. Footer says "© 2026 TA AI Solutions". The only remaining occurrences are inside two live-app URLs (degreedlabs.com, degreed-ta.github.io), which are no longer displayed on the pages.
4. **No "LGPD"**; say "data privacy" instead.
5. **Say "solution(s)", not "tool(s)".**
6. **No status pills, launch dates, or "Open/Preview" buttons** on solution pages or cards.
7. **No Cost Breakdown tables, no Links cards, no enterprise savings math** (avg cost / our cost / savings). Key Metrics show only two cells: time saved and estimated saved value. Enterprise Comparison tables of three products are still shown (except NorthStar).
8. **Do not invent ROI metrics.** Use TBD or "Data collection in progress" where real data does not exist. QuickSlot's 350 hrs / $13,700 and Language Fluency's ~30 min / 90% completion are Sam-supplied figures.
9. **Include a candidate-experience bullet** in Business Impact wherever a candidate interacts with the solution (QuickSlot, Language Fluency, Skill Scanner have one; Scout does not because candidates do not use it).
10. **Light, clean visual style.** Keep per-solution accent colours consistent between card and page.
11. **Screenshot section is titled "See It in Action"** on every solution page.

---

## 9. Open items and likely next requests

- **Skill Scanner screenshots**: add `screenshots/skill-scanner-1.png`, `-2.png`, `-3.png`. Nothing else needs changing; the slots fill automatically.
- **Landing-page "~$34K Est. Annual Cost Savings" stat**: awaiting Sam's decision on whether to keep, change, or remove, given the savings math was removed from the pages.
- **"In Development" count** on the landing page is 3 (Scout, Skill Scanner, NorthStar). Sam has not confirmed NorthStar should be counted.
- **Hidden contact section / Get in Touch button**: still present in index.html but hidden. Sam may want to enable it later.
- **Custom domain**: Sam said early on they want one "later". Requires adding a `CNAME` file and DNS records (see README.md for steps).
- **README.md** is a generic deploy guide with stale references (mentions `solution-template.html`, `solution-1.html`, uses em-dashes and "Degreed"). It is not user-facing, but could be tidied.
- **solution-template.html** still carries the old layout (status card, cost table, links card, hero button, "Degreed" footer was fixed). If a new solution is added, it is faster to copy an existing finished page (e.g. solution-scout.html for a simple page, solution-northstar.html for a rich one) than to use the template.
- **solution-intake-prompt.md** still outputs sections (cost breakdown, links, status) that the site no longer displays. Update it if Sam uses it again.
- **Quest Keeper** solution was fully removed (page deleted, card removed). Its preview app was password-protected; that password appeared in earlier public commits, so Sam may wish to rotate it.
- **Security**: a GitHub token was pasted into chat during this project. Recommend Sam revokes and reissues it.

---

## 10. How to add a new solution (procedure)

1. Copy the closest existing page (e.g. `solution-scout.html`) to `solution-<slug>.html`.
2. In `:root`, set `--accent`, `--accent-hover`, `--accent-3`, `--accent-light` to the new colour family. Search-and-replace any hard-coded `rgba(r,g,b,...)` values derived from the old accent (they appear in a few borders and gradients).
3. Update `<title>`, nav `.nav-sol` name, breadcrumb category, category tag, H1, hero description.
4. Fill in What it does, feature list, Business Impact, Tech Stack, Key Metrics, Enterprise Comparison.
5. Add screenshots as `screenshots/<slug>-1.png` etc. and matching `<figure class="shot">` elements.
6. In `index.html`: add a `.theme-<name>` pair of CSS rules (icon bg, tag bg/colour) next to the others, then add a card in the solutions grid (copy an existing card; keep `style="justify-content:flex-end"` on the footer so the arrow sits right).
7. Update the hero stats counts if appropriate.
8. Commit and push.

Check tag balance after large edits: counts of `<div` vs `</div>` and `<section` vs `</section>` should match.

---

## 11. Change log (chronological)

1. Initial build: landing page + template + README + intake prompt. Brand "TA AI Labs", purple accent.
2. Renamed to "TA AI Lab", switched to teal accent, replaced "tool" with "solution", removed About page, added hidden GitHub contact CTA. Built 5 real solution pages from Sam's PDF (QuickSlot, Language Fluency, Quest Keeper, Scout, Skill Scanner).
3. Hero copy, stats, category tags, em-dash purge, hidden contact section.
4. Key Metrics 2×2 grid, TBD values, Open vs Preview button rule, Quest Keeper research-backed hours (2 to 4 hrs/week).
5. Published to GitHub Pages at samprieto/ta-ai-solutions.
6. Renamed "TA AI Lab" → "TA AI Solutions". LGPD → data privacy. Hero H1 → "Talent Acquisition / AI Solutions". Added favicon.
7. Removed Cost-Conscious value item, reworded Built In-House and Secure by Design, "Purpose-Built" → "Built to Scale", "Talent Acquisition" → "Talent Attraction", removed solutions subtitle. On solution pages: removed buttons, status and dates, cost table, links card; added Screenshots section; renamed "How it helps the team" → "Business Impact".
8. Removed enterprise savings summary and two Key Metric cells on all pages. QuickSlot $13,700 metric and copy edits. Candidate-experience bullets added. Quest Keeper removed entirely. Screenshots added for QuickSlot (3) and Language Fluency (2).
9. Removed all "Degreed" mentions, breadcrumb "TA AI Solutions" made a link, Skill Scanner copy edits (description, Beyond Hiring text, removed integration bullet and Maestro chip, enterprise placeholder → TBD).
10. Removed empty screenshot slot on Language Fluency, removed Scout savings box, sticky nav now shows "TA AI Solutions › Solution", Scout screenshots added (2).
11. Added NorthStar page and card (indigo). Landing-page In Development count 2 → 3.
12. NorthStar revised: BI tone, new tagline, removed Product Stories / Intelligence Model / closing section, "For Business Leaders" → "For Leaders", two screenshots added. Screenshot section renamed "See It in Action" site-wide.

---

## Appendix A: Original NorthStar brief content not currently on the page

Kept here in case Sam wants any of it back.

**Product Stories (removed)**
1. Organization Intelligence. See your organization as more than an org chart. Explore people, roles, levels, locations, compensation, spans of control, workforce cost, skills, capabilities, and organizational structure from one connected view.
2. Team Capability Intelligence. Understand how your team is built. Give managers a Moneyball-style view of their workforce: each person's role, critical skills, capability strengths, development gaps, and where important capabilities are concentrated across the team.
3. Organization Sandbox. Design the future organization before making the change. Move employees, restructure teams, eliminate or create positions, change reporting lines, and model promotions in a safe sandbox environment. NorthStar recalculates the organizational impact in real time: Headcount · Payroll · Management Cost · Spans · Layers · Skills · Capabilities · Talent Risk · Hiring Demand.
4. Workforce & Financial Planning. Connect workforce decisions to financial outcomes. Finance and business leaders can understand workforce budget, forecasted spend, position status, hiring assumptions, vacancies, compensation, geographic cost, and workforce investment.
5. Workforce Scenario Intelligence. Compare options before committing resources. Model alternative strategies: Hire · Develop · Promote · Move · Restructure · Change Location · Contract · Automate / Redesign. Compare across: Cost · Capacity · Capability · Organization Structure · Time · Talent Availability · Hiring Feasibility · Risk.
6. NorthStar AI. Turn workforce data into decisions. NorthStar AI continuously analyzes organizational, financial, skills, talent, and hiring data to surface risks and opportunities leaders may otherwise miss. Ask: Where are our biggest capability gaps? Which teams have unhealthy spans of control? What capabilities are concentrated in only one or two employees? Where are we forecast to exceed workforce budget? What happens if we remove a management layer? Which roles will we need to hire to deliver our FY27 strategy? Could internal mobility solve some of our planned hiring demand?

**Intelligence Model (removed)**
Business Goals → Capabilities → Organization → Skills & People → Workforce Investment → Build · Buy · Develop · Move · Redesign → Execution → Business Results, with NorthStar Intelligence + AI running horizontally across the entire lifecycle.

**Closing (removed)**
Build the organization your strategy requires. Companies don't win because they have the most headcount. They win because they have the right capabilities, in the right organization, with the right people, deployed against the right priorities. NorthStar gives leaders the intelligence to build it.

**Original tagline options:** "Turn business strategy into the organization, capabilities, workforce, and investment required to win." / "NorthStar, The Business & Workforce Operating System".

## Appendix B: Removed solution, Quest Keeper (for reference)

Category Work Management, amber accent (#d97706), icon ⚔️. "An AI-powered work management system that transforms daily priorities into structured, time-allocated tasks, automatically captured from screenshots, emails, meetings, and transcripts." Preview at https://task-forge-saga.lovable.app/ (password-protected). Metrics used: ~2 to 4 hrs saved/week/user; ~$312/user/yr enterprise comparables. Tech: Lovable, Gemini Flash. Removed from the site in change 8 at Sam's request.
