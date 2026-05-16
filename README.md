# Groundwork — Product Specification
**Team OS for early-stage founders**
Version 1.0 · May 2026

---

## Product overview

**Groundwork** is a phase-aware team operating system for founders building organizations from scratch. It combines a scaling roadmap, decision-making frameworks, org visualization, and meeting infrastructure into a single opinionated product — guiding a team from the founding moment through to 100+ people.

Unlike generic project management tools (Asana, Linear) or org chart software (ChartHop, Lucidchart), Groundwork tells you *what to do next* based on where you are in your scaling journey, and gives you the actual frameworks to do it.

**Tagline:** The operating system for building your team before you know how to build your team.

---

## Problem statement

Early-stage founders face a structural knowledge gap. They know how to build their product, but not how to build the organization that builds the product. The consequences are predictable:

- Decisions made by instinct become bottlenecks when the team grows
- No documentation means institutional knowledge lives in founders' heads
- The wrong people get promoted, or the right people leave because ownership is unclear
- Hiring outpaces structure, creating chaos that costs months to unwind

Existing tools don't solve this. Org chart tools show structure but don't guide you to build it. HR platforms assume you already have HR. Project management tools track tasks, not organizational health.

**The gap:** There is no opinionated, phase-aware guide that gives a 4-person team the exact frameworks they need *right now*, then evolves with them as they grow.

---

## Target user

**Primary persona: The founding CEO/co-founder**
- 1–30 person team, pre-Series B
- Technical or product background — people management is new territory
- Time-poor, skeptical of consultants and heavyweight HR software
- Wants to do this right but doesn't know where to start

**Secondary persona: The first operations/people hire**
- Joining a team of 10–25 people
- Needs to build people infrastructure from near-zero
- Wants a credible, structured framework to show the founder

**Anti-persona:** HR teams at 200+ person companies. Enterprise. Anything that needs an implementation partner.

---

## Core value proposition

| Without Groundwork | With Groundwork |
|---|---|
| "Who owns this?" arguments | DRI table — one owner per area, public, updated |
| Decisions made in Slack, never written down | DACI log — structured, searchable, assigned |
| Meetings with no purpose or outcome | 3-meeting cadence with built-in agendas |
| Values written on a wall, ignored in practice | Values that have been tested against real criteria |
| "Are we ready to hire a manager?" guesswork | Phase readiness check with objective triggers |
| Org chart in PowerPoint, always out of date | Live org chart tied to real team data |

---

## Core features

### 5.1 Scaling roadmap
The backbone of the product. Four phases with objective trigger conditions:

| Phase | Size | Key threshold to advance |
|---|---|---|
| 1 · Foundation | 1–6 | 7+ people + 80% Phase 1 checklist |
| 2 · Early team | 7–20 | 20+ people + functional owners assigned |
| 3 · Growing | 21–60 | First manager hired + career ladders written |
| 4 · Scaling | 60+ | C-suite formed + strategy framework deployed |

Each phase unlocks new framework templates and checklists. Completed phases are archived and surfaced as context when patterns repeat.

### DACI decision log
- Create a decision with Driver, Approver, Contributors, Informed pre-filled
- Status tracking: draft → in progress → decided
- Searchable decision history with filter by owner or topic
- Templates for common founding decisions (hiring, tooling, strategy, compensation)
- Export to Notion, Confluence, or PDF

### DRI ownership table
- List of company functions/areas mapped to a single named owner
- Public within the team (shareable link)
- Review prompt every 60 days
- Gaps highlighted — areas with no DRI show as warnings
- Auto-populated from org chart when a team member joins

### Org chart builder
- Manual input (drag-and-drop) or CSV import
- Phase-aware: Phase 1 defaults to flat, Phase 2 shows functional areas
- Each node links to the person's DRI areas
- Export to PNG/SVG for decks
- Scenario mode: plan a future org state without publishing it

### Meeting hub
- Three pre-built meeting templates (weekly all-hands, 1:1, monthly retro)
- Agenda editor with phase-appropriate defaults
- Meeting notes with auto-capture of decisions and action items
- Action items sync to the task view
- Calendar integration (Google Calendar, Outlook)

### Phase readiness check
- Real-time dashboard of Phase 2 trigger conditions
- Each condition shows current state vs. required threshold
- "What changes when I advance" preview — shows which templates unlock
- Founder must confirm readiness manually — no auto-advance
- Sends a team notification when a phase transition is confirmed

### Frameworks library
Pre-built, editable templates for every framework in the product:
- DACI decision log (Google Doc, Notion, and in-app)
- DRI ownership table
- Working agreement
- Values workshop facilitation guide
- Weekly all-hands agenda
- 1:1 agenda (employee-led)
- Monthly retrospective agenda
- Hiring rubric (Phase 1 generalist)
- Onboarding doc template

### AI guidance layer *(v2)*
- Proactive nudges: "You have 6 team members — check your Phase 2 readiness"
- Framework recommendations based on team profile
- Decision log drafting: describe a decision in natural language, Groundwork structures it as a DACI
- Meeting summary generation from notes

---

## User flows

### Flow 1: Onboarding (new user)
1. Sign up with email or Google
2. Answer 4 questions: team size, stage, biggest current challenge, industry
3. Groundwork assigns Phase 1 (or 2 if 7+ people)
4. Dashboard loads with pre-populated checklist and 3 recommended first actions
5. Prompt to invite team members

### Flow 2: Logging a decision
1. User clicks "+ New decision" from dashboard or DACI log
2. Fills in: title, context (free text), options considered, decision made
3. Assigns DACI roles from team member dropdown
4. Sets due date (for in-progress decisions)
5. Decision appears in log with status badge
6. "Informed" list members receive a Slack/email notification (optional)

### Flow 3: Phase transition
1. Phase readiness check shows all green triggers
2. Founder clicks "Advance to Phase 2"
3. Confirmation modal: summary of what's changing, what unlocks
4. Founder confirms → Phase 2 activates
5. New checklist loads; Phase 1 archive saved
6. Optional team announcement drafted by Groundwork

### Flow 4: Onboarding a new hire
1. Admin adds person to team (name, role, start date)
2. Org chart updates automatically
3. New hire gets a personalized onboarding doc (from the template, pre-filled with their role and DRI areas)
4. Checklist item "Send onboarding doc" marked complete

---

## Screen inventory

| Screen | Route | Primary action |
|---|---|---|
| Dashboard | `/dashboard` | Weekly focus, phase progress, quick metrics |
| Roadmap | `/roadmap` | View all 4 phases, triggers, current position |
| DACI log | `/frameworks/daci` | Create and manage decisions |
| DRI table | `/frameworks/dri` | Assign and review ownership |
| Working agreement | `/frameworks/working-agreement` | Edit and publish team norms |
| Values | `/frameworks/values` | Run workshop, publish values |
| Org chart | `/org-chart` | View and edit team structure |
| Meeting hub | `/meetings` | View cadence, access templates, log notes |
| Meeting detail | `/meetings/:id` | Agenda, notes, action items |
| Phase check | `/phase-check` | Readiness triggers for next phase |
| Settings | `/settings` | Team, integrations, notifications |

---

## Technical considerations

### Architecture (recommended for MVP)
- **Frontend:** React (Next.js) — SSR for initial load speed, client-side for interactive views
- **Backend:** Node.js + PostgreSQL — simple relational model fits well
- **Auth:** Clerk or Auth0 — fastest path to team auth with invites
- **Real-time:** Polling is fine for MVP; WebSockets for v2 live editing
- **AI (v2):** Anthropic API (Claude) for guidance nudges and decision drafting

### Data model (simplified)

```
teams { id, name, phase, created_at }
users { id, team_id, name, role, avatar }
decisions { id, team_id, title, status, driver_id, approver_id, due_date }
dri_areas { id, team_id, area_name, owner_id, last_reviewed }
meetings { id, team_id, type, scheduled_at, notes }
checklist_items { id, team_id, phase, text, completed, completed_by }
```

### Integrations (prioritized)
1. **Slack** — decision notifications, phase transition announcements
2. **Google Calendar / Outlook** — meeting scheduling
3. **Notion** — export DACI log and working agreement
4. **Google/Microsoft SSO** — auth
5. **BambooHR / Rippling** — org chart sync *(v2)*

---

## MVP scope

The minimum viable product focuses on the founding-phase use case (Phase 1, 1–6 people). Everything a solo founder or tiny team needs in their first 90 days.

### In MVP
- Dashboard with phase progress and weekly focus
- Phase 1 + Phase 2 roadmap (Phase 3 and 4 visible but locked)
- DACI decision log (create, track, mark decided)
- DRI ownership table
- Working agreement editor
- Org chart (manual input)
- 3 meeting templates with agendas
- Phase readiness check (Phase 1 → Phase 2 triggers)
- Team invite and multi-user access
- Notion and PDF export

### Out of MVP (v2)
- AI guidance layer and proactive nudges
- Calendar integration
- Values workshop in-app
- Meeting notes with action item sync
- Phase 3 and Phase 4 full support
- HRIS integration
- Mobile app

---

## Success metrics

| Metric | Target (6 months post-launch) |
|---|---|
| Teams signed up | 500 |
| Week 2 retention | 50% |
| DACI decisions logged per active team | 5+ |
| Phase transitions completed | 30% of Phase 1 teams |
| NPS | 45+ |
| Paid conversion (from free) | 15% |

**Leading indicator to watch:** If teams log at least 3 decisions in their first 7 days, they're 3× more likely to still be active at 30 days. The DACI log is the activation moment.

---

## Pricing model

| Plan | Price | Seats | Features |
|---|---|---|---|
| Free | $0 | Up to 5 | Phase 1 only, DACI log, DRI table, 1 org chart |
| Starter | $29/mo | Up to 15 | All phases, meeting hub, exports, Slack |
| Growth | $79/mo | Up to 50 | AI guidance, calendar integration, advanced reporting |
| Scale | Custom | 50+ | HRIS sync, SSO, dedicated support |

**Model rationale:** Free tier captures founding teams at exactly the right moment (1–5 people). They convert to Starter when they hit 7 people and unlock Phase 2 — a natural, value-driven upgrade moment.

---

## Build roadmap

| Milestone | Timeline | What ships |
|---|---|---|
| M0 — Foundation | Weeks 1–2 | Auth, team setup, dashboard shell, Phase 1 checklist |
| M1 — Core frameworks | Weeks 3–5 | DACI log, DRI table, working agreement |
| M2 — Org + meetings | Weeks 6–8 | Org chart builder, 3 meeting templates, meeting notes |
| M3 — Phase system | Weeks 9–10 | Phase readiness check, Phase 1→2 transition, roadmap view |
| M4 — Collaboration | Weeks 11–13 | Team invite, Slack integration, Notion export |
| Beta launch | Week 14 | 50 beta teams, feedback cycle |
| v2 planning | Week 16+ | AI layer, calendar, Phase 3/4 depth |

---

*Groundwork product spec v1.0*
