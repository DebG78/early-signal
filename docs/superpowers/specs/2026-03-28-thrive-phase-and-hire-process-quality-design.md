# Thrive Phase & Hire Process Quality — Design Spec

## Context

The Early Success app tracks the employee journey across three phases: Hire, Land, and Thrive. Currently, the Thrive phase contains the Signal Radar and Pattern Engine screens — but these are cross-phase detection tools, not Thrive-specific content. The Thrive phase has no dedicated screens showing the factors that predict whether a 6-12 month employee continues to grow and engage.

Additionally, the Hire phase's Interviewer Quality screen only tracks TA interviewers, missing process-level signals like scorecard usage and interview structure that also impact hire quality.

This spec addresses both gaps.

---

## 1. Navigation Restructure

Move Signal Radar and Pattern Engine out of Thrive into a new top-level section. Add two new Thrive screens.

### New sidebar structure:

```
HIRE
  Funnel & Sources
  Interviewer Quality        (expanded — see section 4)

LAND
  Onboarding & Ramp
  Retention Signals

THRIVE
  Thrive Factors             (NEW)
  Thrive Watchlist           (NEW)

INSIGHTS                     (NEW section)
  Signal Radar               (moved from Thrive)
  Pattern Engine             (moved from Thrive)
```

**Implementation notes:**
- Update sidebar nav data structure to reflect the four sections
- Signal Radar and Pattern Engine screens remain unchanged in content — only their navigation placement moves
- The INSIGHTS section header follows the same styling as HIRE / LAND / THRIVE

---

## 2. Thrive Factors Screen

**Purpose:** Show org-level patterns about what predicts thriving at 6-12 months, with individual drill-down.

**Design approach:** Three narrative-led factor cards, each expandable. One story at a time — lead with insight text, numbers as supporting evidence.

### Factor 1: Manager Quality

- **Lead insight** (example): *"Employees with weekly 1:1s and structured feedback are 1.8x more likely to be rated 'exceeding' at 12 months"*
- **Metrics:**
  - 1:1 frequency (weekly / biweekly / monthly / none)
  - Feedback cadence — how often formal feedback is given
  - Goal-setting completion rate — whether the employee has documented goals
  - Skip-level check-in rate — whether the employee has had a skip-level conversation
- **Drill-down:** Manager leaderboard showing which people managers have the best/worst retention and performance outcomes for their 6-12 month reports. Similar layout to the interviewer quality leaderboard.
- **Sample data:** 6-8 managers with varying metrics and outcomes

### Factor 2: Growth & Development

- **Lead insight** (example): *"New hires given a stretch project in months 4-8 show 23% higher engagement scores at 12 months"*
- **Metrics:**
  - Project complexity trajectory — are they getting increasingly complex work?
  - Stretch project assignment — has a non-routine/challenging project been assigned?
  - Skill development milestones — evidence of learning (training, certifications, new tool adoption)
  - Career conversation frequency — how often career growth is discussed
- **Drill-down:** Individual employees and their growth trajectory (project timeline, whether stretch work was assigned, skill milestones hit)
- **Sample data:** Trend data showing the correlation between stretch assignments and outcomes

### Factor 3: Team & Environment

- **Lead insight** (example): *"Teams with >20% new-hire concentration have 2x the 12-month attrition rate"*
- **Metrics:**
  - Team tenure mix — ratio of new hires (<12mo) to tenured members
  - Collaboration breadth — how many distinct colleagues the person works with
  - Peer feedback signals — frequency and sentiment of peer interactions
  - Team stability — turnover rate within the person's team during their tenure
- **Drill-down:** Teams ranked by their new-hire thriving indicators, with ability to see individual team members
- **Sample data:** 5-6 teams with varying compositions and outcomes

### Layout principles:
- Each factor is a collapsible card — only one expanded at a time (accordion)
- Collapsed state shows: factor name, lead insight snippet, a health indicator (green/amber/red)
- Expanded state shows: full insight narrative, key metrics with context, drill-down table
- Follow the existing app's card/expand pattern used in Pattern Engine deep dives

---

## 3. Thrive Watchlist Screen

**Purpose:** Flag individual employees in the 6-12 month window who are showing signs of disengagement or stalling, with systemic analysis of what's driving risk.

### Section A: Lead Narrative

A summary headline: e.g., *"Of 214 employees in the 6-12 month window, 18 are showing early signs of disengagement across 3 or more thrive factors"*

### Section B: At-Risk List

Modeled on the existing Land phase at-risk hires list.

Each entry shows:
- Employee name, role, team, office
- Months since hire (6-12 range)
- Risk score (0-100)
- Firing factors: specific signals like "No 1:1 in 4 weeks", "No stretch project assigned", "Team has 35% new-hire concentration"

Sorted by risk score descending. Aim for 5-8 at-risk individuals + 3-4 on the monitoring watchlist (mirroring Land's structure).

### Section C: Factor Heatmap

A compact visualization showing which of the three factor categories (Manager, Growth, Team) is contributing most to risk across the population. This answers "what's the systemic issue?" rather than "who's at risk?"

Format: Three horizontal bars or a simple breakdown showing the relative contribution of each factor to the total risk signals firing.

### Section D: Strongest Predictors of 12-Month Thriving

Ranked list of correlations, same format as the "Strongest Predictors of 12-month Retention" in the Land phase:
- 1:1 frequency (r = 0.68) — Strong
- Stretch project assignment (r = 0.59) — Strong
- Goal clarity score (r = 0.53) — Moderate
- Team stability (r = 0.44) — Moderate
- Collaboration breadth (r = 0.38) — Moderate
- Career conversation frequency (r = 0.31) — Weak

---

## 4. Hire Phase: Interview Process Quality

**Purpose:** Add process-level quality signals to the existing Interviewer Quality screen.

### New section: "Interview Process Quality"

Added below the existing interviewer leaderboard on the Interviewer Quality screen.

- **Lead insight** (example): *"Hires assessed with structured scorecards show 18% higher 12-month retention than unscored interviews"*
- **Metrics:**
  - **Scorecard usage rate** — % of interviews using a structured scorecard, broken down by role family
  - **Interview structure score** — consistency of rubric usage vs. freeform interviews
  - **Round count impact** — reinforces existing pattern (rounds >3 add no value) shown as a process metric with outcome correlation
  - **Time between rounds** — average days between interview stages; long gaps correlate with lower offer acceptance
  - **Candidate experience score** — post-interview satisfaction rating from candidates
- **Format:** Narrative-led card with a summary table showing each metric, its current value, benchmark, and trend

### Sample data structure:

| Metric | Current | Benchmark | Trend |
|---|---|---|---|
| Scorecard usage | 64% | 85% | Improving |
| Structured rubric | 58% | 80% | Stable |
| Avg rounds to hire | 3.4 | 3.0 | Stable |
| Avg days between rounds | 8.2 | 5.0 | Worsening |
| Candidate experience | 3.8/5 | 4.2/5 | Stable |

---

## 5. Sample Data Requirements

All data is static/hardcoded (matching the existing app pattern). New data needed:

- **Managers:** 6-8 people managers with 1:1 frequency, feedback cadence, goal completion, skip-level rates, and outcomes (retention, performance ratings of their reports)
- **Thrive employees:** ~8-12 individuals in the 6-12 month window with varying risk profiles and factor signals
- **Teams:** 5-6 teams with tenure mix, stability, and collaboration metrics
- **Process quality metrics:** Aggregate numbers for scorecard usage, structure, timing, and candidate experience by role family

---

## 6. Files to Modify

- **`index.html`** — This is the single-file app. All changes go here:
  - Sidebar navigation data/markup (add INSIGHTS section, move items, add Thrive screens)
  - New render functions: `renderThriveFactorsScreen()`, `renderThriveWatchlistScreen()`
  - New data structures for thrive factors, watchlist employees, manager data, team data
  - Extend `renderInterviewersScreen()` with process quality section
  - Update `renderPatternsScreen()` and `renderActivityScreen()` navigation references
  - CSS for new card layouts (reuse existing patterns where possible)

---

## 7. Verification

- Navigate all sidebar links — all four sections (Hire, Land, Thrive, Insights) should work
- Signal Radar and Pattern Engine should render identically to current behavior, just under the Insights section
- Thrive Factors: all three factor cards expand/collapse, drill-down tables render
- Thrive Watchlist: at-risk list renders with risk scores and firing factors, heatmap and predictors display
- Interviewer Quality: new process quality section appears below existing leaderboard
- Mobile responsive: new screens follow existing responsive patterns
- No broken links or orphaned screen references
