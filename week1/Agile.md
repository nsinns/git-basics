# Agile Concepts, Sprint Planning & PI/Release Planning

Most bootcamps teach Agile as a slide with definitions. Here, students *run* it — every week is a real sprint with a real backlog, and the program itself is structured as two Program Increments (PIs), which is exactly the language they'll hear on day one of a corporate job that uses SAFe (extremely common at the mid-to-large companies your grads are targeting).

## Why PI Planning specifically (not just Scrum)

Plain Scrum teaches sprint-level thinking. But most enterprises — especially the ones running "AI/ML, Data Engineering, MLOps at scale" that this program targets — operate multiple teams inside a **SAFe (Scaled Agile Framework)** structure, where sprints roll up into a **Program Increment (PI)**, typically 8–12 weeks of aligned work across teams. Giving students hands-on exposure to *both* levels — sprint and PI — is a real differentiator: most junior candidates have only ever heard the word "sprint" in an interview, never "PI Objectives" or "program board."

---

## Part 1: Core Concepts (taught Week 1, reinforced all program)

### Roles
| Role | In a real team | In this program |
|---|---|---|
| Product Owner | Owns the backlog, prioritizes value | Instructor/mentor for Foundation weeks; **the student themselves** for capstone |
| Scrum Master | Facilitates ceremonies, removes blockers | Mentor, rotating to student-facilitated by Month 2 |
| Development Team | Builds the increment | The student (or small team, for capstone) |

### Events (Ceremonies)
- **Sprint Planning** — decide what gets built this sprint and how
- **Daily Stand-up** — compressed to twice-weekly here (Wed live session + Sat office hours) given part-time format
- **Sprint Review** — demo the working increment to stakeholders (peers/mentors)
- **Sprint Retrospective** — reflect on process, not just output

### Artifacts
- **Product Backlog** — the full list of everything that could be built (for Foundation: the curriculum itself; for capstone: the student's own feature list)
- **Sprint Backlog** — what's committed to *this* sprint
- **Increment** — the actual working, demoable output at sprint's end

### User Stories
Format: **"As a [role], I want [goal], so that [benefit]."**
Example: *"As a data analyst, I want a cleaned and validated dataset, so that I can trust the dashboard numbers."*

Good stories are **INVEST**: Independent, Negotiable, Valuable, Estimable, Small, Testable.

### Estimation
Use **story points**, not hours — a relative-effort scale (commonly Fibonacci-like: 1, 2, 3, 5, 8, 13). Introduce lightweight "planning poker": each student silently picks a number for a task, reveals simultaneously, discusses outliers, re-votes once.

### Definition of Ready (DoR) / Definition of Done (DoD)
- **DoR** — a story is ready to be pulled into a sprint if: it has a clear acceptance criteria, no unresolved blocking dependency, and is estimated.
- **DoD** — a story is done if: code is merged via reviewed PR, tests pass, it's demoed, and documentation/README is updated. (Ties directly into the Git workflow already established.)

---

## Part 2: How Sprints Work in This Program

**Every single week is one sprint.** This maps directly onto the weekly rhythm already in place:

| Ceremony | When | Where in the existing schedule |
|---|---|---|
| Sprint Planning | Monday | First 15 min of Live Session 1 |
| Stand-up | Wednesday & Saturday | Start of Live Session 2 + Saturday office hours |
| Sprint Review (Demo) | Saturday | The existing Saturday demo slot |
| Sprint Retrospective | Saturday | Immediately after the demo, 10–15 min |

Nothing new needs to be added to the calendar — this just gives the existing rhythm its proper names and a bit more ceremony structure, which is the point: students should leave saying "I ran 24 real sprints," not "I did 24 weekly assignments."

---

## Part 3: Sprint Planning — Ceremony Walkthrough

**Duration:** 15 minutes, folded into Monday's Live Session 1.

**Agenda:**
1. **Sprint Goal** (2 min) — one sentence: what does "done" look like by Saturday's demo? (For Foundation weeks, this is largely pre-set by the curriculum; for capstone, the student defines it themselves.)
2. **Review backlog items** (5 min) — this week's lab broken into 2–4 user stories.
3. **Estimate** (3 min) — quick story-point pass, especially useful once students hit the capstone and are estimating their own work for the first time.
4. **Commit** (3 min) — move stories from Product Backlog → Sprint Backlog.
5. **Risks/dependencies** (2 min) — anything blocking (e.g., "waiting on cloud account approval").

### Sprint Backlog Template
```
Sprint: Week 5 — ETL Pipeline
Sprint Goal: Working ETL job that extracts, transforms, and loads into Postgres with basic error handling.

| Story                                              | Points | Owner | Status      |
|-----------------------------------------------------|--------|-------|-------------|
| As a student, I want an extract step from a public API | 3    | Me    | To Do       |
| As a student, I want a transform step cleaning the data | 3    | Me    | To Do       |
| As a student, I want a load step with upsert logic      | 5    | Me    | To Do       |
| As a student, I want retry/error handling on failure    | 2    | Me    | To Do       |

Definition of Done: PR merged, ETL runs end-to-end without manual intervention, logs show retry behavior on simulated failure.
```

---

## Part 4: Sprint Review & Retrospective

### Sprint Review (Demo) — Saturday
- 2–3 minutes per student: show the working increment (not slides — the actual running thing).
- Peers/mentor give quick feedback: what would a real stakeholder ask about this?

### Sprint Retrospective — right after, 10–15 min total
Use **Start / Stop / Continue**, fastest format for a time-boxed part-time cohort:
```
START:    What should we start doing?
STOP:     What should we stop doing?
CONTINUE: What's working and should continue?
```
Each student writes 1 line per category in the shared board (or a simple shared doc); mentor picks 1–2 recurring themes to address the following Monday. This is what makes the retro real rather than symbolic — it should visibly change something.

---

## Part 5: PI / Release Planning

A **Program Increment (PI)** is a larger planning horizon — typically 8–12 weeks / 4–6 sprints — where the "team" aligns on a bigger set of objectives before diving back into sprint-level execution. Your 6-month program maps naturally onto **two PIs**:

```
PI 1 — "Foundation & Core Skills"           PI 2 — "Capstone Delivery"
Weeks 1–16 (4 iterations of 4 sprints)      Weeks 17–24 (8 sprints)
├─ Iteration 1 (Wk 1–4):  Eng. Foundations  ├─ Sprint 0 (Wk17): PI Planning + kickoff
├─ Iteration 2 (Wk 5–8):  Data Engineering  ├─ Sprints 1–6 (Wk18–23): build increments
├─ Iteration 3 (Wk 9–12): AI/ML Core        └─ Sprint 7 (Wk24): Demo Day / Inspect & Adapt
└─ Iteration 4 (Wk13–16): MLOps/Cloud/Design
        ↓
  PI 1 System Demo = existing Week 16 Sprint Demo #4
```

### PI Planning Session — Agenda (compressed to ~2 hours, vs. SAFe's typical 2-day event)
Run this once at Day 1 (kicking off PI 1) and again at the Week 16→17 transition (kicking off PI 2).

1. **Business context** (15 min) — instructor presents the "roadmap": what roles this program prepares students for, and why each iteration exists (tie explicitly back to job-readiness, not just topics).
2. **Roadmap walkthrough** (15 min) — show the iteration breakdown above; for PI 2, walk through capstone track options.
3. **Draft PI Objectives** (30 min) — each student writes 3–5 personal objectives for the PI, each with a **business value score (1–10)**, e.g.:
   - *"Deploy a monitored ML model to the cloud" — Business Value: 9*
   - *"Get comfortable with SQL window functions" — Business Value: 6*
4. **Identify risks — ROAM the board** (20 min) — every identified risk gets sorted:
   - **R**esolved, **O**wned (someone's tracking it), **A**ccepted (living with it), **M**itigated (plan in place)
   Example: *"I don't have a laptop that can run Docker well" → Owned by mentor, mitigation: cloud-based dev environment.*
5. **Confidence vote** (5 min) — each student gives a 1–5 fist-of-five on "how confident are you in hitting your PI objectives?" Anything below 3 gets a follow-up conversation immediately, not after it becomes a crisis.
6. **Commit** (5 min) — objectives are locked in and posted publicly (cohort Slack/Notion) for the PI.

### PI Objectives Template
```
Student: _______        PI: PI 1 (Weeks 1–16)

| Objective                                          | Business Value (1-10) | Stretch? |
|-----------------------------------------------------|------------------------|----------|
| Deploy a monitored ML model to the cloud            | 9                      | No       |
| Build a working RAG app over my own documents        | 8                      | No       |
| Contribute a dbt model with passing tests            | 6                      | No       |
| Get an Airflow DAG running with alerting             | 7                      | Yes      |

Confidence (1-5): ____
```

### PI System Demo & Inspect & Adapt (I&A)
At the end of each PI, run a slightly bigger version of the normal Sprint Review:
- **System Demo** — every student shows their *cumulative* PI output (not just this week's), roughly 5 min each.
- **Quantitative review** — how many objectives were actually hit vs. committed (this is a real SAFe metric called PI Predictability, and it's a great thing for students to see tracked about their own work).
- **Retrospective + problem-solving workshop** — the group looks at any objective that was missed across multiple students and root-causes it together (e.g., "half the cohort struggled with cloud IAM setup" → fix the curriculum or add a support session before PI 2).

This "Inspect & Adapt" naming is deliberate — it's the exact term used in real SAFe organizations, and being able to say "I've participated in PI Planning and an I&A workshop" is a small but real signal in an interview at a company that runs this way.

---

## Appendix: Full Templates (copy-paste ready)

### User Story
```
As a [role], I want [goal], so that [benefit].
Acceptance Criteria:
- [ ] ...
- [ ] ...
Story Points: __
```

### Sprint Retro
```
Sprint: ____
START:
- 
STOP:
- 
CONTINUE:
- 
Action item for next sprint: ____
```

### ROAM Risk Board
```
| Risk                              | Status (R/O/A/M) | Owner    | Notes                        |
|------------------------------------|-------------------|----------|-------------------------------|
| Laptop can't run Docker well       | Mitigated          | Mentor   | Provided cloud dev environment|
| Unfamiliar with cloud IAM concepts | Owned              | Student  | Extra office-hours slot booked|
```

### PI Confidence Vote
```
Fist of Five:
5 - Very confident       2 - Low confidence
4 - Confident            1 - Not confident, need help now
3 - Somewhat confident
```