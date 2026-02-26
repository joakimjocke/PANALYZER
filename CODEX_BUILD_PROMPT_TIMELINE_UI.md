# Codex Build Prompt – Investigation Timeline UI (Gotham-inspired)

## 1) Mission

Build a desktop-first web UI that matches the attached reference image in spirit:
dark, data-dense, professional “investigation console”.
Focus on buildable, real-world UI (clean panels, typography, spacing),
not cinematic TV effects.

Primary screen: a timeline view with event cards and a highlighted interval.

---

## 2) Inputs (what AI should use)

- Reference image: `docs/reference/timeline-gotham.png`
  (place the attached image here)
- This brief (single source of requirements)

---

## 3) Tech constraints

Choose ONE of these (prefer A unless repo already uses something else):

A) Next.js (App Router) + React + TypeScript + Tailwind
B) Vite + React + TypeScript + Tailwind

UI primitives:
- Prefer shadcn/ui (Radix) OR lightweight headless components.
- Avoid heavy dashboard frameworks.

General rules:
- No inline styles unless unavoidable.
- Componentize the layout (panels, tabs, timeline, cards).
- Data-driven rendering from a JSON fixture (bootstrap data).
- Keep animations subtle or none.

---

## 4) Page to implement

Route/page:
- `/timeline`

Desktop layout target:
- Designed for 1440p and up (works down to ~1280px).
- Responsive behavior can be minimal (stack panels on smaller widths),
but desktop is the priority.

---

## 5) Visual design targets (from the image)

Theme:
- Dark charcoal background
- Blue-gray panels with subtle borders
- Low-noise, low-glow accents (cyan/blue + optional amber for emphasis)

Layout structure:
- Top app bar (left: app name, center/right: search + actions)
- Left panel: “Case Data” (case id, status, lead count, etc.)
- Right panel: “Suspect Info” (name, location, key attributes)
- Center: horizontal timeline with:
  - event markers
  - event cards floating above the line
  - a highlighted time interval band (21:15–21:40)
- Bottom area: tabbed section with 3 tabs:
  - Evidence Log (table/list)
  - Communication Records (table/list)
  - Investigation Notes (notes list + detail)

Typography:
- Clean sans, readable at high density
- Clear hierarchy: timestamps > titles > metadata > body

---

## 6) Timeline behavior (MVP buildable)

Must have:
- Render a horizontal time axis with tick labels.
- Render events at their timestamp position.
- Show 3 example events:
  - 21:00 – Witness Observation
  - 21:17 – Call Registered
  - 21:32 – Vehicle Seen on CCTV
- Each event has a card above the line:
  - timestamp
  - title
  - short description
  - optional thumbnail (use placeholder images)
- Render a highlighted interval band:
  - start 21:15, end 21:40
  - centered label “21:15 – 21:40”

Nice-to-have (but only if time permits):
- Hover: show extra metadata tooltip.
- Click an event: selects it and populates a details panel
  (can be the bottom tabs area or a side drawer).

Non-goals for this pass:
- Infinite zooming
- Dragging/creating events
- Real backend/API
- Complex animations

---

## 7) Data model (fixture-driven)

Create a JSON fixture at:
- `src/data/timeline.sample.json`

Example shape (adapt as needed):
- `case`
- `suspect`
- `events[]`
- `intervals[]`

Events should include:
- id
- type (observation | call | cctv)
- timestamp (HH:MM)
- title
- description
- mediaUrl (optional)

Intervals should include:
- id
- start (HH:MM)
- end (HH:MM)
- label
- emphasis (optional)

---

## 8) Component architecture (suggested)

- `AppShell`
  - `TopBar`
  - `MainGrid`
    - `CaseDataPanel`
    - `TimelinePanel`
      - `TimelineAxis`
      - `TimelineIntervalBand`
      - `TimelineEventMarker`
      - `TimelineEventCard`
    - `SuspectInfoPanel`
  - `BottomTabs`
    - `EvidenceLogTab`
    - `CommunicationRecordsTab`
    - `InvestigationNotesTab`

Keep Timeline logic isolated:
- a small utility to map HH:MM -> minutes -> x-position
- do not hardcode x positions in JSX

---

## 9) Acceptance criteria (definition of done)

- Running app shows `/timeline` page that resembles the reference image.
- Layout matches: top bar, left panel, right panel, center timeline,
  bottom tabs.
- Timeline positions are calculated from time values.
- Interval band is visible and spans correct range.
- Event cards render from JSON fixture (not hardcoded in components).
- Code is clean, readable, and componentized.
- Includes a short README with run instructions.

---

## 10) Run instructions (Codex must ensure)

- Install deps
- Start dev server
- Provide commands in README

Example:
- `npm install`
- `npm run dev`

---

## 11) Codex checklist (do this in order)

1. Scaffold app (if repo doesn’t exist yet).
2. Add Tailwind + base theme tokens (colors, borders, radii).
3. Build the layout grid and panels.
4. Build the timeline axis + mapping utility.
5. Render interval band from fixture.
6. Render events + cards from fixture.
7. Implement bottom tabs with mock tables/lists.
8. Polish spacing and typography to match the reference image.
9. Add README + ensure it runs.

---

## 12) Notes

- Do NOT attempt to replicate Palantir branding or logos.
  Use neutral naming (e.g., “Investigation Console”).
- Keep it implementable with normal web UI patterns.
- Prefer clarity and maintainability over visual theatrics.

