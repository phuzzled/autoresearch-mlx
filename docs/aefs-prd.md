# Product Requirements Document
## Adaptive Executive Function System

**Working name:** To be determined
**Previous working names:** Orbit, Synchwell
**Version:** 0.3
**Status:** Product Definition / Pre-MVP
**Primary audience:** Founders, Product, Engineering, Investors, Clinical/Advisory
**Reference products:** Tiimo, Routinery, Structured, Llama Life, Goblin Tools, Habi, Inflow

---

## How to read this document

This PRD has two halves.

**Part A (sections 1-20)** is the product thesis: why this exists, what it does, and why it is defensible. Read this if you are assessing the opportunity.

**Part B (sections 21-34)** is the specification: what gets built, in what order, under what constraints, and how we will know whether it worked. Read this if you are building it or funding it.

Appendices cover naming, brand and competitive detail.

Anything marked **[OPEN]** is an unresolved decision with an owner and a deadline. Anything marked **[ASSUMPTION]** is unvalidated and carries risk. These markers are deliberate. A PRD that hides its uncertainty is a sales document.

---

# PART A: THESIS

---

# 1. Executive Summary

A neurodivergent-first adaptive executive-function system that reduces the cognitive work required to organise and move through everyday life.

Four core capabilities, connected by a Transition Engine:

**PLAN → DO → ADAPT → UNSTICK**

The central proposition:

> **Most productivity tools remember your tasks. This system learns how you function.**

The system progressively learns the user's actual behaviour (task duration, initiation difficulty, routines, transitions, postponement patterns, successful recovery strategies) and uses that understanding to reduce future executive-function demand.

The governing principle:

> **The system adapts to the person. The person does not have to adapt to the system.**

The intended experience resembles an exceptional personal butler: it knows what matters, understands the person's commitments and patterns, anticipates what is likely to be needed, prepares quietly, and intervenes only when useful.

**The wedge.** Of the four capabilities, one is unserved by every competitor: automatic recovery when the day collapses. Tiimo, Structured and Routinery all assume the plan mostly holds. For the target user it frequently does not. UNSTICK is the entry point, the demo that sells the product, and the first thing we should build to a high standard.

**What we must prove.** That automatic day-repair measurably increases the probability a user resumes purposeful activity after disruption, compared with a static plan. Everything else in this document is scaffolding around that claim. See section 22.

---

# 2. The Problem

Most productivity systems assume the primary problem is organisation. For many ADHD, autistic and AuDHD people, it is not.

A person may understand exactly what needs to happen while struggling with:

- deciding where to begin
- estimating how long something will take
- breaking large or ambiguous tasks into executable actions
- remembering something at the appropriate moment
- initiating a task
- transitioning between activities
- maintaining attention
- recognising the passage of time
- recovering after interruption
- recognising that the original plan is no longer realistic
- reorganising the remainder of the day
- restarting after becoming stuck
- maintaining the productivity system itself

Traditional productivity software transfers this executive-function burden back onto the user. The user creates the tasks, prioritises them, estimates duration, schedules, decomposes, remembers to look, notices failure, reschedules everything, and maintains the system.

The tool intended to reduce cognitive load becomes a source of cognitive load. This creates **maintenance fatigue**: the productivity system itself becomes another unfinished task.

**Evidence position.** The bullet list above is drawn from established executive-function literature and from competitor review patterns, not from our own research. Before Release 2 we require primary evidence: structured interviews (n≥20) and a diary study (n≥8, two weeks) to confirm which of these frictions are most acute and most under-served. See section 30. **[ASSUMPTION]**

---

# 3. Product Thesis

This is not primarily a better to-do list. It is an **Adaptive Executive Function System**: an intelligent layer between intention and action that carries as much organisational and executive-function burden as reasonably possible while preserving user agency.

The system should understand what needs doing, what matters, what is fixed, what can move, what the user is doing now, what should happen next, how long things actually take this person, which activities create friction, when transitions fail, when the user becomes stuck, what has changed, and how to recover when reality breaks the plan.

The system forms around the user's actual life rather than requiring the user to conform to a methodology.

---

# 4. Core Product Principles

Each principle below carries a **test**. A principle without a falsifiable test is decoration.

## 4.1 The system adapts to the human
The user should not have to change how their brain works to satisfy the methodology.
*Test:* No feature requires the user to maintain a structure whose only purpose is keeping the system accurate.

## 4.2 Anticipate, don't interrupt
A good butler does not repeatedly ask "what would you like me to do now?"
*Test:* Median notifications per active day ≤ 6, and ≥ 60% of delivered notifications are acted on within 10 minutes.

## 4.3 Reduce decisions
Every unnecessary decision consumes executive capacity. Continually ask: does this require executive function the system could reasonably carry instead?
*Test:* Every screen has a measured decision count. Do Mode presents at most one primary decision at a time.

## 4.4 No failure state
Missing a task is information. Being late is information. Losing three hours is information. None is a moral or product failure.
*Test:* No red overdue counts, no streak loss, no backlog gate. The system's response to any disruption is "this is where we are now, here is what happens next."

## 4.5 Zero-maintenance by default
The system should require less management the longer it is used.
*Test:* Median manual scheduling actions per active week declines month over month for a retained cohort.

## 4.6 Trustworthy automation (new)
Automation that is confidently wrong is worse than no automation. The system must be reversible, explainable and appropriately hesitant.
*Test:* Every automated change to the user's day is undoable in one action, carries a plain-language reason, and respects the act/ask thresholds in section 26.

---

# 5. Core Product Architecture

# PLAN → DO → ADAPT → UNSTICK

Connected by: **TRANSITION**

These are not necessarily five screens. They describe how the system thinks and behaves.

| Layer | Question it answers | Primary failure it addresses |
|---|---|---|
| PLAN | What realistically needs to happen? | Overwhelm, unrealistic planning |
| DO | What do I do now? | Initiation, decision paralysis |
| TRANSITION | When do I move? | Time blindness, task switching |
| ADAPT | How does this person actually function? | Generic, degrading personalisation |
| UNSTICK | The plan broke. Now what? | Abandonment after disruption |

---

# 6. PLAN

Plan turns commitments, intentions, routines and tasks into a realistic executable day.

The user should be able to provide poorly structured information:

> Doctor Tuesday 10:30.
> Need to sort Centrelink stuff this week.
> Clean house.
> Finish report before Friday.
> Remember to call Mum.

The system determines what additional structure is required and asks only for what it genuinely cannot infer.

**Inputs.** Calendar appointments, recurring routines, tasks, deadlines, personal commitments, priorities, estimated duration, location where relevant, dependencies, historical duration, preferred working periods, capacity, previous completion behaviour, transition requirements.

The system constructs the plan around reality rather than creating an idealised schedule.

---

# 7. Commitment Types

## Anchored
Must happen at or around a particular time: appointments, meetings, school pickup, flights, medication. These form the skeleton of the day and are protected during replanning.

## Planned
Important activities the system places into the available day: report writing, shopping, administration, exercise. These can move.

## Available
Useful activities with no required time: return library books, non-urgent phone call, organise files, buy household item. An intelligent task bank the system can draw from when unexpected capacity appears.

**Specification note.** These are states on a single task entity, not three separate types. A task moves between states through user action or system inference. The data model must make this transition cheap and reversible.

---

# 8. Calendar Assimilation

Calendar integration is foundational. The system should not merely display calendar events; it should assimilate them into the executive-function model.

> 10:00 GP appointment

may imply preparation, travel, the appointment, return travel, transition/recovery, and the next activity.

Existing commitments become anchors and the adaptive system builds around them.

Targets: Google Calendar, Microsoft Outlook Calendar, Apple Calendar where platform integration permits.

The product should complement the user's existing calendar rather than replace it.

**Reality check on two-way sync.** Two-way calendar synchronisation is one of the most expensive and defect-prone features in this category. Recurrence exceptions, timezone handling, delete semantics, concurrent edits and provider rate limits each generate a long tail of bugs. Apple Calendar has no usable server-side API; support means CalDAV or an iOS-local integration, which fragments the architecture. Sequencing in section 28 reflects this: read-only ingest first, write-back for system-created events second, full bidirectional reconciliation last. **[OPEN: Apple strategy. Owner: Eng lead. Decision required before Release 2.]**

---

# 9. Intelligent Task Breakdown

Task decomposition is a first-class capability. Every meaningful task supports **Break this down**.

> Prepare presentation

becomes:

1. Open existing presentation
2. Review brief
3. Identify three key messages
4. Create slide outline
5. Draft slides
6. Add visuals
7. Review
8. Export final version

The user can request **more detail** or **less detail**.

The decomposition engine considers available time, task complexity, current context, dependencies, previous behaviour, likely initiation friction and current capacity.

The objective is not a checklist. It is: **what is the smallest useful thing I can do next?**

Generated steps become executable actions inside the plan. The user never manually transfers AI output into another system. This is the specific gap Goblin Tools leaves open.

---

# 10. DO

Plan answers *what should happen*. Do answers **what do I do now**. This distinction is fundamental.

Traditional interfaces expose the entire workload precisely when an overwhelmed user needs less information. Do Mode deliberately reduces the field of view.

## Now + Next

**NOW:** the current action.
**NEXT:** the immediate following action.

Supporting controls: visual timer, elapsed time, expected remaining time, pause, complete, skip, need more time, break this down, I'm stuck.

The entire day's workload must not dominate the execution interface.

---

# 11. Routines

Routines combine guided execution with the adaptive system.

## Morning Routine
1. Wake
2. Medication
3. Shower
4. Dress
5. Breakfast
6. Check today's commitments
7. Leave

Each step may have expected duration, timer, instruction, optional status, dependency and transition prompt.

Routines are not rigid scripts. If a 40-minute morning routine starts 20 minutes late, the system determines what can shorten, move, disappear or happen later. The application should not simply announce that the user is twenty minutes behind.

---

# 12. Timers

Timers are contextual execution tools, not standalone Pomodoro functionality. They operate at task, task-step, routine-step, transition and focus-session level.

The system compares expected against actual duration and feeds that into Adapt.

**Reliability is a product-defining constraint, not a quality goal.** Timer freezing, sync lag, unexpected pauses and cross-device state inconsistency are severity-1 defects. Competitor reviews suggest timer unreliability is a primary driver of churn in this category. See NFR-2 in section 25 for the hard numbers.

---

# 13. TRANSITION

Time blindness means knowing what comes next is insufficient if the person does not transition at the necessary moment.

The Transition Engine understands: current activity → preparation → transition → next activity.

> **10 minutes remaining**
> Report writing finishes soon. Your appointment is next.

> **Time to transition**
> Save the report. Grab your keys. Leave by 2:22.

It incorporates travel time, preparation, shutdown steps, context switching, fixed commitments and historical transition behaviour.

Ignored transition prompts become behavioural data. The system does not respond by escalating notification aggression.

---

# 14. ADAPT

Adapt is the learning layer. It answers: **what is this person's actual pattern of functioning?**

Adapt is distinct from Unstick. Unstick repairs disruption. Adapt learns from behaviour over time so future support is better.

## Behavioural signals (subject to consent, section 27)

Actual task duration, estimated versus actual, initiation delays, completion rates, skipped activities, frequently postponed activities, interruption patterns, routine completion, transition difficulty, decomposition frequency, tasks commonly requiring assistance, preferred working periods, higher and lower capacity periods, planning optimism, successful recovery strategies, notification responses.

The system develops a personal working model.

Not: *people with ADHD take 30 minutes to do this.*
But: **you usually need approximately 25 minutes for this kind of task.**

Personalisation emerges from individual behaviour, not stereotypes.

## Understanding behaviour

> You've moved administrative tasks from the afternoon four times this week. You complete them more often before lunch.
> You usually complete this routine when it contains fewer than six steps.
> Large undefined tasks are more likely to start after you break them down.
> Your planned 15-minute transitions usually take approximately 25 minutes.

Observations must be descriptive and useful, never judgemental. The objective is not compliance reporting. It is helping the user answer: **how do I actually function?**

## Capacity

Traditional systems assume every day has equivalent capacity. A lightweight model (Low / Normal / High) may modulate workload, task complexity, decomposition depth, transition allowances and optional activities.

Capacity tracking must earn its place through demonstrated usefulness. We collect it only if it measurably improves scheduling outcomes, not because competitors offer mood tracking. Evaluation gate in section 28.

---

# 15. UNSTICK

Unstick is the deliberate recovery mechanism. It answers **I'm stuck, what now?** and **my day has gone off the rails, what now?**

The user should never manually repair the productivity system. A prominent **UNSTICK** action is always available. Final wording subject to testing.

## Micro Unstick

The user knows what to do but cannot begin or continue.

> Write report introduction.

The system reduces the activation threshold progressively:

> Open the report.
> Find the heading marked Introduction.
> Write one sentence explaining what the report is about.

This is dynamic task decomposition during execution.

## Macro Unstick

The day has substantially departed from plan: waking late, losing time scrolling, hyperfocus, unexpected appointment, interruption, forgotten commitment, task overrun, abandoned routine, overwhelm, hours of non-use, or simply a bad day.

The system determines where we are now, what happened, what did not happen, what remains fixed, what still matters, what can move, shrink, disappear or move to another day. It then rebuilds the remaining day.

## Worked example

Original plan: 9:00 Admin, 10:00 Report, 12:00 Lunch, 1:00 Shopping, 3:00 Appointment, 4:30 Exercise.

The user returns at 12:17 having completed none of it. Traditional software presents six overdue tasks.

This system says:

> **It's 12:17. I've rebuilt the rest of your day.**

It protects the 3:00 appointment, moves non-critical administration, adjusts shopping, creates a realistic report block, retains or moves exercise according to capacity, and rebuilds transitions. Do Mode resumes:

> **NOW: Eat lunch**

The user is back in motion. No calendar repair required.

## No punishment

The product avoids failed-routine messages, shame-based language, punitive streak loss, red walls of overdue tasks, guilt-driven engagement, and requiring yesterday's backlog to be resolved before using today.

Missed activity becomes information. Adapt learns from it. Unstick handles its consequences.

---

# 16. Anticipatory Assistance

If an appointment requires travel, preparation and departure actions appear automatically. If a morning routine consistently overruns, tomorrow becomes more realistic. If complex tasks repeatedly require decomposition, the system offers it before paralysis. If a transition repeatedly fails, preparation begins earlier. If an appointment is cancelled and 35 minutes appears, the system surfaces a fitting Available task.

The system progressively removes unnecessary decisions.

---

# 17. Distraction Defence and Body Doubling

Both are competitive opportunities that must not distract from proving the core loop. Both are Phase 1.5 or later.

**Distraction defence** may include OS focus-mode activation, notification suppression, optional app blocking where platform APIs permit, focus sounds, distraction warnings and temporary interface simplification. Do Mode could initiate an optional Focus Environment: begin task, activate focus settings, start timer, show Now, suppress interruption, restore device state on completion. This is preferable to adding a generic Pomodoro feature.

**Body doubling** need not initially involve another human. An ambient mode ("Start with me") keeps the micro-step visible, maintains the timer, prompts substep transitions, quietly acknowledges progress and offers Unstick when movement stops. Peer or human body doubling may be evaluated later. We should not build an expensive social platform before demonstrating that body doubling materially improves outcomes.

---

# 18. AI Role

AI is an enabling layer, not the product identity.

Useful functions: natural-language capture, task decomposition, schedule construction, schedule repair, routine generation, duration estimation, behavioural pattern recognition, contextual prioritisation, next-action generation, transition preparation, natural-language explanation, Unstick reasoning.

Users should not need to prompt an AI. They use the product. Intelligence operates underneath it.

**Architectural position.** Most of the above are not LLM problems. Schedule construction and repair are constraint-satisfaction problems with hard constraints (anchors, travel, dependencies) and soft constraints (preference, capacity, energy). Duration estimation is regression over the user's own history. The LLM's genuine jobs are language understanding, decomposition and explanation. Building the replanner as a prompt would be slow, expensive, non-deterministic and untestable. See section 24.

---

# 19. Notifications

A neurodivergent productivity application that creates notification fatigue defeats itself.

Priority order: transitions, fixed commitments, meaningful deviations, useful preparation, immediate next actions.

Repeated ignored notifications become Adapt data. The system learns rather than increasing volume.

**Policy (specified, not aspirational).**
- Hard budget: maximum 8 delivered notifications per day, default target 4-6.
- Anchored commitments and active transitions are exempt from the budget only where a missed anchor has real-world consequence.
- No notification may be sent twice for the same event without user-configured repeat.
- Quiet hours default on, user-configurable, learned from device use over time.
- Three consecutive ignored prompts of the same class suppresses that class for 24 hours and logs a learning event. The system never escalates tone or frequency in response to being ignored.

---

# 20. Competitive Positioning

The product is not "Tiimo + Routinery + Goblin Tools". Those products inform the architecture. The differentiator is the adaptive layer.

| Product | Primary strength | Gap we address | Approx. price (AUD/mo) |
|---|---|---|---|
| Tiimo | Neurodivergent visual planning | Maintenance burden, real-time adaptation | ~$10-13 |
| Routinery | Guided routine execution | No adaptive whole-day planning | ~$5-8 |
| Structured | Simple visual timeline | Minimal behavioural adaptation | ~$3-5 |
| Llama Life | Immediate execution, timeboxing | No persistent personal model | ~$5-8 |
| Goblin Tools | Task decomposition | Decomposition disconnected from execution | ~$1 one-off |
| Habi | Distraction defence | Less comprehensive EF layer | ~$8-10 |
| Inflow | Coaching and education | Different intervention layer | ~$30-45 |
| **This product** | **Plan + Do + Adapt + Unstick** | **Progressively carries EF load** | See section 29 |

**Pricing figures are indicative and require verification before any external use. [OPEN: Owner Product, due before first investor conversation.]**

Detailed per-competitor strengths and weaknesses are in Appendix B. Those weaknesses are drawn from public review analysis and are **[ASSUMPTION]** until validated by primary research.

---

# PART B: SPECIFICATION

---

# 21. Users

"Neurodivergent" is a population, not a segment. We build for three primary segments and explicitly not for a fourth.

## P1: The Overloaded Professional (primary)
Diagnosed or self-identifying ADHD/AuDHD adult, 25-45, in knowledge work, managing a full calendar plus domestic load. Already uses a calendar seriously. Has tried and abandoned two or more productivity apps. Has money and is willing to pay for something that works.
*Job to be done:* "When my day falls apart by 11am, help me get something useful done in the hours left, without making me feel like I failed."
*Why they churn from competitors:* maintenance burden exceeds benefit within three weeks.

## P2: The Admin-Overwhelmed Adult (secondary)
Lower structural support, may be unemployed, studying, on benefits or managing chronic illness alongside ADHD. Struggles with bureaucratic tasks with real consequences (Centrelink, medical, tenancy). Price-sensitive.
*Job to be done:* "Help me start the thing I have been avoiding for six weeks."
*Why they matter:* highest-stakes use case, strongest word-of-mouth, most acute unmet need. Also the segment where safety obligations bite hardest.

## P3: The Routine-Dependent (secondary)
Higher autistic profile. Values predictability and explicit structure. Disruption is costly and distressing.
*Job to be done:* "Keep my routine intact, and when it breaks, tell me exactly what happens now."
*Design tension:* P3 wants less automation and more predictability than P1. Automation defaults must be configurable along this axis.

## Explicitly not the initial target
Teams, workplaces, parents managing children's schedules, and clinicians managing caseloads. Each is a plausible later market and each would distort the product now.

**[OPEN: segment weighting for launch. Owner: Product. Decision before Release 2 positioning work.]**

---

# 22. Assumptions and Hypotheses

The product rests on five claims. Each has a validation method and a kill condition. This is the most important section in the document.

## H1: Recovery beats planning (core)
**Claim:** Automatic day-repair after disruption materially increases the probability a user resumes purposeful activity, versus a static plan.
**Test:** Release 1 in-product experiment. Compare resumed-activity rate within 60 minutes of a disruption event, Unstick arm versus control arm shown a plain task list.
**Success:** Unstick arm resumption rate exceeds control by ≥ 15 percentage points.
**Kill condition:** No measurable difference at n≥150 disruption events. If this fails, the moat thesis fails and the product is a better-designed Structured competitor.

## H2: Adaptation is felt, not just measured
**Claim:** Users perceive the system getting better at predicting them, and that perception drives retention.
**Test:** Estimate accuracy improvement over 6 weeks, correlated with retention and with a single perception question at day 30.
**Success:** Median absolute duration error drops ≥ 25% by week 6, and week-6 users rate "it understands how long things take me" ≥ 4/5.
**Kill condition:** Accuracy improves but perception and retention do not. Adaptation then is a cost centre, not a moat, and should be de-emphasised in positioning.

## H3: Willingness to pay
**Claim:** P1 will pay $12-18/month, above the category norm, for a system that removes maintenance.
**Test:** Pricing research pre-Release 2, then live price testing.
**Kill condition:** Conversion at $12 is below half of conversion at $6. Unit economics in section 29 then do not close.

## H4: Cold start is survivable
**Claim:** The product delivers enough value in week one, before it has learned anything, to retain users into the period where adaptation begins to work.
**Test:** D7 retention ≥ 40% and D30 ≥ 20% in the first cohort.
**Kill condition:** D7 below 25%. The adaptation moat is then unreachable, and the day-one experience must be redesigned before anything else is built. See section 23.

## H5: Trust survives automation
**Claim:** Users accept the system rearranging their day automatically rather than finding it unsettling or intrusive.
**Test:** Undo rate on automated replans, plus qualitative interviews.
**Kill condition:** Undo rate above 30%, or interviews reveal loss-of-control anxiety. The act/ask thresholds in section 26 then shift heavily towards ask, which weakens the butler proposition.

---

# 23. The Cold Start Problem

The moat depends on accumulated behavioural data. Behavioural data requires retention. Retention in this category is poor. This is the central strategic tension and it needs a deliberate answer, not "it learns over time."

**Day 1 value must not depend on learning.** Three mechanisms:

1. **Immediate structural value.** Calendar ingest plus assimilation produces a genuinely better day view within minutes of signup, before a single behavioural signal exists.
2. **Decomposition as the hook.** AI breakdown delivers value on first use, needs no history, and is the single most immediately demonstrable capability. It is what gets someone to open the app on day 1 with a task they have been avoiding.
3. **Unstick as the return trigger.** Users return after disruption because the product is useful precisely at the moment other products are punishing. Day 1 onboarding should deliberately show what happens when the day breaks, not just what a good day looks like.

**Priors, not blank slates.** New users start with sensible defaults (population-level duration priors by task category, conservative transition allowances) that are immediately personalised as data arrives. The user should never experience a "learning period" of bad predictions. Priors are transparent and clearly labelled as starting estimates.

**Portability of the model.** Because the adaptation model is the moat, it is also the retention lever and the ethical hazard. Section 27 commits to export. The moat is that the model is *useful*, not that it is *hostage*.

**Non-use is not failure.** A user who plans on Sunday, executes on Wednesday and never opens the app in between is succeeding. Engagement metrics must not treat this as churn. See section 30.

---

# 24. Technical Architecture Constraints

This is not an architecture document. It states the constraints that shape one.

## 24.1 The replanner is a solver, not a prompt
Macro Unstick must be implemented as a deterministic constraint-based scheduler:
- **Hard constraints:** anchored commitments, travel feasibility, dependencies, opening hours, medication timing.
- **Soft constraints:** preferred working periods, capacity, task priority, deadline proximity, transition allowance, learned friction.
- **Objective:** maximise weighted value of the remaining day subject to realistic execution.

An LLM may produce the natural-language framing and may assist with ambiguous prioritisation, but must not be the scheduler. Rationale: determinism, testability, latency, and cost. A replan must be reproducible in tests and identical on retry.

## 24.2 Latency budget
Unstick is invoked at the moment of lowest user patience. If it is slow, the user is gone.
- Macro Unstick replan: p50 ≤ 1.5s, p95 ≤ 3s, to first rendered rebuilt day.
- Micro Unstick next-step generation: p50 ≤ 1.5s, p95 ≤ 4s.
- Any operation exceeding budget must degrade to a deterministic fallback, never a spinner.

## 24.3 Local-first execution
Do Mode and timers must function fully offline. Timer state, step advancement and completion are authoritative on-device and reconcile on reconnect. Network dependency in the execution path is a design defect.

## 24.4 Sync and conflict resolution
Cross-device state requires an explicit conflict model. Default: last-write-wins per field with a monotonic clock, except timer state, which is owned by the device that started the session until explicitly handed off. Handoff must be a first-class, visible action.

## 24.5 Calendar integration is phased
Read-only ingest (Release 1) → write-back of system-created events (Release 2) → full bidirectional reconciliation (Release 3). Each phase is a separate risk. Apple Calendar strategy is **[OPEN]**.

## 24.6 Model strategy
Decomposition, capture and explanation run through a hosted LLM. Requirements: streaming responses, prompt caching to control cost, aggressive caching of repeat decompositions, and a deterministic fallback path for every AI call. Model choice is deferred but cost per user per day is a design constraint from day one. See section 29.

## 24.7 Testability
Every scheduling behaviour must be expressible as a fixture: given this day state and this disruption at this time, the replan is exactly this. A replanner that cannot be regression-tested will silently degrade.

---

# 25. Non-Functional Requirements

| ID | Requirement | Target |
|---|---|---|
| NFR-1 | App cold start to Do Mode visible | ≤ 2.0s p95 on a 3-year-old mid-range device |
| NFR-2 | Timer accuracy | Drift ≤ 500ms over 60 min; survives app kill, device restart, OS background termination; resumes correct elapsed time |
| NFR-3 | Cross-device state propagation | ≤ 3s p95 when both devices online |
| NFR-4 | Offline capability | Full Do Mode, timers, routines, completion, capture. Sync on reconnect with no data loss |
| NFR-5 | Unstick latency | Per section 24.2 |
| NFR-6 | Notification delivery reliability | ≥ 99% of scheduled transition notifications delivered within 30s of target |
| NFR-7 | Accessibility | WCAG 2.2 AA. Full screen reader support. Dynamic type to 200%. Respects reduce-motion |
| NFR-8 | Data durability | Zero user-visible data loss. Point-in-time recovery ≤ 24h |
| NFR-9 | AI availability | Every AI-dependent feature has a deterministic degraded path. Provider outage must not break planning or execution |
| NFR-10 | Crash-free sessions | ≥ 99.5% |

NFR-2 deserves emphasis. Timer unreliability is the most frequently cited failure in competitor reviews and it destroys trust in a way no other defect does. It is a launch blocker, not a polish item.

---

# 26. AI Behaviour and Failure Modes

## 26.1 Act or ask
The system acts autonomously when confidence is high and the change is reversible. It asks when confidence is low or the change is consequential.

| Situation | Behaviour |
|---|---|
| Reordering Planned tasks within the day | Act, notify quietly |
| Moving a task to another day | Act, notify, one-tap undo |
| Dropping a task from today entirely | Ask |
| Touching an Anchored commitment | Always ask |
| Rebuilding the day after explicit Unstick | Act, show full reasoning, one-tap revert to previous plan |
| Suggesting a routine change based on patterns | Ask, with the evidence shown |
| Any change with external consequence (declining a meeting, messaging someone) | Always ask |

P3 users (routine-dependent) get a global setting shifting all defaults towards ask.

## 26.2 Explainability
Every automated change carries a one-sentence plain-language reason. Not "optimised your schedule" but "moved shopping to tomorrow because your appointment leaves 40 minutes and shopping usually takes you 70."

## 26.3 Reversibility
Every automated change is undoable in one action. Every replan can revert to the immediately preceding plan for at least 24 hours.

## 26.4 Failure modes to design for explicitly
- **Bad decomposition.** Steps are wrong, patronising, or too coarse. Mitigation: inline regenerate, more/less detail, per-step edit, and a "this wasn't useful" signal that feeds Adapt.
- **Overconfident replanning.** The system drops something that mattered. Mitigation: Anchored protection, ask thresholds, visible diff of what changed, revert.
- **Condescension.** Micro Unstick reduces a step so far it insults the user. Mitigation: reduction depth is user-controlled and learned; the system starts at the depth that worked last time, not at the bottom.
- **Learned helplessness risk.** A system that carries all decisions may erode self-efficacy. Mitigation: Adapt insights are framed to build self-knowledge (section 14), and the user can always see and override the model. **[OPEN: this deserves clinical advisory input.]**
- **Wrong pattern inference.** The system concludes something false about the user and acts on it. Mitigation: minimum evidence thresholds before any inference influences scheduling, and every inference is visible and dismissable.
- **Provider outage or degradation.** Per NFR-9.

## 26.5 Tone constraints
No praise inflation. No motivational language. No emoji-driven encouragement. No implied judgement about missed work. The system is calm, factual and useful. It states what is, and what happens next.

---

# 27. Data, Privacy and Regulatory Position

This product infers disability-related characteristics about its users from behaviour. That is not an ordinary consumer data posture.

## 27.1 Classification
Behavioural data that permits inference of a neurodevelopmental condition is likely to constitute special-category / sensitive personal information under GDPR Art.9 and Australian Privacy Principles. We treat it as such regardless of how the final legal analysis lands. **[OPEN: formal privacy counsel review. Owner: Founder. Required before first external beta.]**

## 27.2 Commitments
- Explicit, granular, revocable consent for behavioural learning, separate from account creation. The product must be usable with learning disabled.
- No sale of user data. No advertising model. Ever. This is a product constraint, not a policy preference.
- Full export of the personal adaptation model in a human-readable format.
- Deletion means deletion, including derived model state, within 30 days.
- Data residency options for AU, EU and US. **[OPEN: cost and timing.]**
- No behavioural data sent to model providers for training. Zero-retention inference endpoints required.
- Sharing with a clinician or coach is opt-in, scoped, time-limited and revocable, and is never a default.

## 27.3 Regulatory boundary
The product is a **wellness and organisational tool**. It is not a medical device and must not become one by accident.

Prohibited claims: treats, diagnoses, manages or mitigates ADHD, autism or any condition; improves clinical symptoms; substitutes for medication, therapy or clinical care.

Permitted claims: helps organise your day; reduces the effort of planning and switching tasks; learns how long things take you.

Any feature that screens, scores, triages or clinically interprets crosses the line into SaMD territory under TGA and FDA frameworks. Capacity tracking is the nearest hazard: a Low/Normal/High self-report is fine; an inferred mental-state score presented as insight is not. **[OPEN: regulatory counsel review before any capacity feature ships publicly.]**

## 27.4 Marketing constraint
Every piece of marketing copy passes a claims review against 27.3. The temptation to say "clinically informed" or imply therapeutic benefit will be constant and must be resisted.

---

# 28. Safety and Duty of Care

The system observes patterns that may correlate with crisis: sustained total non-function, abandonment of all routines including medication, days of Low capacity, sharp behavioural discontinuity.

## 28.1 Position
We are not a crisis service and must not pretend to be. We also must not ignore what we observe.

## 28.2 Commitments
- The system never diagnoses, never names a mental state, and never says anything resembling "you seem depressed."
- After a defined period of total non-engagement, the re-entry experience is deliberately gentle: no backlog, no accumulated guilt, no catch-up demands. The day starts from now.
- A passive, always-available support resources screen exists (region-appropriate crisis and ADHD support services). It is never pushed in response to inferred state, because inferring state and acting on it is precisely the line we are not crossing.
- Medication-related routine steps are never automatically dropped, shortened or rescheduled by the replanner. They are treated as hard-anchored. **[This is a hard requirement, not a preference.]**
- Gamification that could drive compulsive use is prohibited. No streaks, no points, no loss aversion mechanics.

## 28.3 Advisory input required
Sections 26.4, 27.3 and 28 require review by a clinician with ADHD/autism specialisation before public launch. **[OPEN: advisory board formation. Owner: Founder.]**

---

# 29. Business Model and Unit Economics

## 29.1 Model
Consumer subscription. Monthly and annual. No free tier permanently, but a meaningful free trial: 14 days with full capability, because the value proposition requires the user to experience at least one day falling apart and being repaired.

**Indicative pricing:** $14.99/month or $119/year (AUD). Above Tiimo and well above Structured, justified by the maintenance reduction claim. Validated by H3.

A reduced-price or subsidised tier for P2 (the admin-overwhelmed segment) is ethically indicated and commercially sensible for word-of-mouth. **[OPEN: mechanism and eligibility. Owner: Founder.]**

## 29.2 The cost problem
This is the constraint most likely to be under-estimated.

A user who replans three times a day, decomposes four tasks and captures six items generates meaningful inference volume. If per-user inference cost approaches $2-4/month, gross margin at $15 is acceptable; if heavy users reach $8-10/month, it is not.

**Design responses, required from Release 1:**
- The scheduler is deterministic and costs nothing per invocation (section 24.1). This is the single biggest cost lever and it is an architecture decision, not an optimisation.
- Aggressive caching of decompositions. The same task decomposed twice should cost once.
- Prompt caching on shared system context.
- Smaller models for classification and capture; larger models only for decomposition and explanation.
- Per-user cost telemetry from day one, with alerting on outliers.
- A fair-use ceiling defined before launch, even if never enforced.

**[OPEN: cost model with real numbers. Owner: Eng lead. Required before Release 1 build starts.]**

## 29.3 Metrics that matter to a funder
CAC by channel, D30 / D90 / D180 retention, trial-to-paid conversion, monthly churn, gross margin net of inference, LTV:CAC. None of these have values yet and this document should not pretend otherwise.

---

# 30. Measurement Plan

## 30.1 The observability paradox
Our stated goal is that users need the app less over time. Declining engagement could therefore mean success or churn, and standard telemetry cannot distinguish them.

**Resolution.** The primary health metric is not engagement. It is **useful sessions per week**: sessions containing at least one Do Mode completion, one Unstick, or one capture. A user opening the app twice a week and completing their day is healthy. A user opening it twenty times and completing nothing is not. We report useful sessions and completion outcomes, never raw session count, and we never optimise for time in app.

## 30.2 Metric definitions

| Metric | Definition | Instrument | Target (R1) |
|---|---|---|---|
| Time to first action | Signup to first completed task or routine step | Event timestamps | ≤ 24h for 60% of signups |
| Task initiation rate | Started / scheduled tasks per active day | Do Mode events | Baseline in R1, +10% by R3 |
| Decomposition effectiveness | Completion rate of decomposed vs non-decomposed tasks, matched on complexity | Cohort comparison | Decomposed ≥ +20pp |
| Transition success | Transitions begun within 10 min of prompt | Transition events | ≥ 50% |
| Plan repair rate | Unstick invocations followed by a completed action within 60 min | Event sequence | ≥ 60% |
| Manual rescheduling burden | User-initiated moves per active week | Edit events | Declines month over month |
| Estimate accuracy | Median absolute error, predicted vs actual duration | Timer data | -25% by week 6 (H2) |
| Return after disruption | Users returning within 72h of a ≥24h gap | Session data | ≥ 50% |
| Useful sessions per week | Per 30.1 | Composite | ≥ 4 |
| Decision load carried | Automated scheduling decisions / total scheduling decisions | Replan logs | Rises over time |

"Decision reduction" as previously written was unmeasurable. The ratio above is a workable proxy. It is imperfect and should be treated as directional.

## 30.3 Qualitative programme
Metrics cannot capture whether the product feels like a butler or a nag. Ongoing commitment: 5 user interviews per month minimum, a diary study before each major release, and participatory design sessions with paid neurodivergent participants. Participants are compensated at a fair rate. Designing for this population without them in the room is both a quality failure and an ethical one.

---

# 31. Functional Requirements

Full acceptance criteria live in the tracker. This section states the format and gives worked examples for the highest-risk capabilities. Every requirement in section 32 gets this treatment before build.

**Format:** ID, user story, acceptance criteria, priority (Must/Should/Could), dependencies.

---

**FR-UNSTICK-01 — Macro Unstick replan** *(Must)*

*As a user whose day has collapsed, I want the system to rebuild my remaining day so that I can resume without repairing anything myself.*

Acceptance criteria:
1. Given any day state and a current time, invoking Unstick produces a rebuilt remaining day within the latency budget in 24.2.
2. All Anchored commitments in the remainder of the day are preserved at their original times, or the system asks before altering them.
3. Medication steps are never dropped or moved by the replanner.
4. The rebuilt day is immediately executable: Do Mode shows a valid NOW within one tap.
5. A plain-language summary states what changed and why, in at most three sentences.
6. The previous plan is recoverable in one action for at least 24 hours.
7. No overdue counts, red states or backlog prompts appear at any point.
8. Given identical inputs, the replan is deterministic and reproducible.
9. With no network, a degraded deterministic replan still occurs and is labelled as such.

---

**FR-DO-01 — Now + Next execution view** *(Must)*

*As a user in execution mode, I want to see only what I am doing and what is next so that I am not overwhelmed by the whole day.*

Acceptance criteria:
1. At most one current action and one next action are visible without scrolling.
2. The full day is reachable but never default.
3. Controls present: complete, skip, pause, need more time, break this down, I'm stuck.
4. Timer state persists through app kill, restart and OS termination per NFR-2.
5. Fully functional offline.
6. Completing an action advances to the next within 300ms with no interstitial.

---

**FR-DECOMP-01 — Task decomposition** *(Must)*

*As a user facing an ambiguous task, I want it broken into executable steps so that I can start.*

Acceptance criteria:
1. Available on every task with one action.
2. Returns first step within 2s p95, streaming acceptable.
3. Steps become real executable actions in the plan, never text requiring transcription.
4. More detail / less detail adjusts depth without losing user edits.
5. Steps are individually editable, reorderable and deletable.
6. Identical task text within 30 days returns a cached result at no inference cost.
7. Failure of the AI provider surfaces a clear message and a manual step-entry path.

---

**FR-TRANS-01 — Transition prompting** *(Must)*

*As a user with time blindness, I want to be told when to move so that I arrive at fixed commitments on time.*

Acceptance criteria:
1. Prompts account for preparation, travel and shutdown time.
2. Prompt lead time derives from that commitment's learned transition history once ≥5 observations exist; before that, from a conservative default.
3. Prompt content states the concrete next physical action and the departure time.
4. Ignoring a prompt never triggers escalated repetition or tone.
5. Three consecutive ignores suppress that prompt class for 24h and log a learning event.
6. Delivery reliability per NFR-6.

---

# 32. MVP Scope, Sequenced

The original 30 items are retained in full. They are ordered here by dependency and grouped into releases. Effort is in engineering-weeks for a team of three (2 eng, 1 design), and is indicative only.

**A note on total scope.** The sum below is roughly 60-70 engineering-weeks, approximately 9-12 calendar months for a team of three including QA, iteration and slack. This is a v1, not an MVP in the lean sense. That is a legitimate choice, but it should be a conscious one, and the release boundaries below exist so that value and learning arrive before the whole thing is finished.

## Release 0: Foundations (~12 weeks)
*Nothing user-facing proves anything yet. This is unavoidable platform work.*

| # | Item | Effort | Notes |
|---|---|---|---|
| 1 | Account and basic preferences | 2w | Auth, profile, settings shell |
| 2 | Calendar connection | 3w | OAuth, Google + Microsoft |
| 4 | Calendar assimilation | 3w | Event → anchor model with travel/prep inference |
| 5 | Tasks | 2w | Core entity, CRUD |
| 6 | Anchored / Planned / Available states | 1w | States on the task entity |
| 29 | Cross-device state | 1w (foundation) | Sync primitives; full hardening in R2 |

**Exit criteria:** a user can connect a calendar and see an assimilated day. Internal only.

## Release 1: Prove the loop (~20 weeks) — the learning release
*This release exists to test H1 and H4. Everything in it is in service of that.*

| # | Item | Effort | Notes |
|---|---|---|---|
| 8 | Natural-language capture | 2w | |
| 9 | AI task decomposition | 3w | FR-DECOMP-01 |
| 10 | Adjustable decomposition depth | 1w | |
| 11 | Plan view | 3w | |
| 12 | Do Mode | 3w | FR-DO-01 |
| 13 | Now + Next | (in 12) | |
| 15 | Reliable timers | 3w | NFR-2. Do not under-resource this |
| 16-19 | Complete / Skip / Pause / Extend | 1w | |
| 24 | Micro Unstick | 2w | |
| 25 | Macro Unstick | 4w | FR-UNSTICK-01. The deterministic solver |
| 26 | Automatic remaining-day replanning | (in 25) | |
| 27 | Protection of anchored commitments | (in 25) | |
| 22 | Estimated vs actual duration capture | 1w | Data collection only; no adaptation yet |

**Exit criteria:** H1 experiment run to n≥150 disruption events. H4 measured on the first cohort. Public beta.

**Deliberately deferred from R1:** two-way sync, routines, transition engine, adaptive estimates, push notifications. Each is defensible to defer because none is required to test whether day-repair changes behaviour.

## Release 2: Make it liveable (~18 weeks)
*Without this release the product is a clever demo rather than something people use daily.*

| # | Item | Effort | Notes |
|---|---|---|---|
| 7 | Recurring routines | 4w | |
| 14 | Guided routine execution | 2w | |
| 20 | Basic Transition Engine | 4w | FR-TRANS-01 |
| 28 | Push notifications | 2w | Policy in section 19 |
| 3 | Two-way calendar sync | 5w | Write-back of system-created events only |
| 29 | Cross-device state (hardening) | 1w | Full NFR-3 compliance |

**Exit criteria:** daily-use viable. D30 retention measured against H4.

## Release 3: Make it adaptive (~14 weeks)
*This release delivers the moat. It is last because it needs the data the earlier releases generate.*

| # | Item | Effort | Notes |
|---|---|---|---|
| 21 | Basic behavioural learning | 5w | |
| 23 | Adaptive future duration estimates | 3w | H2 test |
| 30 | Minimal behavioural insights | 3w | Descriptive framing per section 14 |
| 3 | Full bidirectional calendar reconciliation | 3w | The hard half of item 3 |

**Exit criteria:** H2 validated or killed.

## Post-MVP
Deeper behavioural modelling, capacity modelling (gated on demonstrated scheduling improvement), proactive Unstick detection, distraction defence, device focus-mode integration, ambient body doubling, peer body doubling, automatic routine suggestions, richer contextual preparation, smartwatch execution, voice capture, location-aware assistance, widgets, household and shared routines, family support, clinician or coach sharing with consent, long-term goals, workload balancing, broader integrations, conversational interaction where useful.

---

# 33. Risks

| ID | Risk | Impact | Likelihood | Mitigation |
|---|---|---|---|---|
| R1 | Adaptation does not measurably improve outcomes; the moat is imaginary | Critical | Medium | H1 and H2 tested at Release 1 and 3 with explicit kill conditions |
| R2 | Cold start: users churn before adaptation delivers value | Critical | High | Section 23. Day-1 value from assimilation and decomposition, priors not blank slates |
| R3 | Inference cost destroys gross margin | High | Medium | Deterministic solver, caching, per-user cost telemetry, cost model before build |
| R4 | Two-way calendar sync consumes the roadmap | High | High | Phased in three stages across R1-R3; read-only first |
| R5 | Timer or sync unreliability destroys trust | High | Medium | NFR-2 as launch blocker; dedicated 3 weeks in R1 |
| R6 | Scope: the 30-item MVP is a 12-month v1 | High | High | Release boundaries with independent exit criteria; R1 alone tests the core hypothesis |
| R7 | Regulatory drift into medical-device territory | High | Medium | Section 27.3, claims review, counsel before capacity features |
| R8 | Safety incident involving a vulnerable user | High | Low | Section 28, clinical advisory, no inferred-state interventions |
| R9 | Incumbent (Tiimo) ships adaptive replanning first | Medium | Medium | Speed on the wedge; the data model advantage compounds only if we start accumulating early |
| R10 | Automation feels intrusive; users disable it | Medium | Medium | H5, act/ask thresholds, P3 configurability |
| R11 | Category price ceiling sits at ~$8 and $15 does not convert | Medium | Medium | H3 pricing research pre-R2 |
| R12 | Team cannot build a solver, an ML layer, three calendar integrations and four clients | High | Medium | Honest resourcing; consider narrowing to one platform for R1 |

R2 and R6 are the two most likely causes of failure. Neither is a technology problem.

---

# 34. Open Questions

| ID | Question | Owner | Needed by |
|---|---|---|---|
| Q1 | Apple Calendar strategy: CalDAV, iOS-local, or defer | Eng lead | Before R2 |
| Q2 | Per-user inference cost model with real numbers | Eng lead | Before R1 build |
| Q3 | Launch platform: iOS-first or iOS+Android | Product | Before R1 build |
| Q4 | Pricing validation and the P2 subsidised tier mechanism | Founder | Before R2 |
| Q5 | Privacy counsel review and data classification | Founder | Before external beta |
| Q6 | Regulatory counsel review of claims and capacity features | Founder | Before public launch |
| Q7 | Clinical advisory board formation | Founder | Before public launch |
| Q8 | Segment weighting: lead with P1 or P2 | Product | Before R2 positioning |
| Q9 | Final product name | Founder | Before public beta |
| Q10 | Does capacity tracking earn its place | Product | Post-R3 evaluation |
| Q11 | Self-efficacy question: does carrying decisions erode capability over time | Clinical advisory | Ongoing |

---

# APPENDICES

---

# Appendix A: Category, North Star and Brand

## Product category
Strategic: **Adaptive Executive Function System**
Consumer: **A system that organises itself around how you actually work.**
Positioning line: **Most productivity tools remember your tasks. This one learns how you function.**

## Product moat
The defensible asset is not the task list, calendar, timer, AI decomposition, notifications or routine builder. All are reproducible.

The moat is the **Individual Adaptation Model**: how long you take, how you start, when you stall, what overwhelms you, how much decomposition helps, when structure helps, when structure becomes oppressive, which routines survive, when you work well, what gets postponed, which transitions fail, which interventions work, what helps you restart.

Switching means losing an environment that has learned how the person actually functions.

**Caveat.** This moat is real only if H1 and H2 hold. Until then it is a hypothesis, and it should be presented as one.

## North Star Experience
The product succeeds when the user increasingly stops having to ask: *What am I supposed to be doing? Where do I start? How do I break this down? When do I need to stop? What happens next? I've fallen behind, how do I fix today?*

PLAN constructs reality. DO removes decisions. TRANSITION keeps movement going. ADAPT learns the individual. UNSTICK restores movement.

> **The system adapts to the human. Not the human to the system.**
> **The more you use it, the less you have to manage it.**

## Accessibility and neurodivergent-first UX
Designed for cognitive accessibility from inception: low visual clutter, strong information hierarchy, predictable navigation, reduced decision density, configurable visual intensity, accessible typography, WCAG 2.2 AA, minimal unnecessary animation, clear progress, plain language, forgiving interaction, configurable reminders, minimal setup burden, reliable state persistence.

Neurodivergent-first does not mean childish. The product should look sophisticated enough for a professional adult to use openly in a meeting.

## Onboarding
**Start useful. Then learn.** Initial setup captures only calendar, important routines, immediate commitments and basic preferences. The user receives value before completing extensive configuration. Onboarding should explicitly demonstrate Unstick, because that is the moment the product differentiates itself.

## Brand behaviour
Should feel: intelligent, calm, capable, contemporary, human, non-clinical, non-judgemental, sophisticated, quietly confident.

Should not feel: childish, motivational, medicalised, excessively gamified, relentlessly cheerful, corporate-productivity obsessed, like an AI chatbot.

The product is not there to cheer the user into functioning. It removes obstacles preventing functioning.

## Naming
Unresolved. **Orbit** remains the conceptual benchmark but is commercially crowded. **Synchwell** has not achieved the desired response.

Positively received during exploration: Orbit, Radius, Arc, Contour, Helix, Meridian, Concentric, Orbital, Polarity, Northstar, Waypoint, Kinetics, SY-NRG. Most were rejected for commercial crowding rather than conceptual weakness.

Desired characteristics: one word, punchy, memorable, alive, evocative, modern, sophisticated, easy to pronounce, easy to spell, non-clinical, not generic AI terminology, suggestive of movement, alignment, augmentation or support around the person.

The metaphors: **the user is at the centre, the system forms around them**, and **something the person inhabits that quietly augments their capability.**

Naming is Q9. It is not a blocker for R0 or R1 build.

---

# Appendix B: Competitive Detail

All weaknesses below are inferred from public review analysis and are **[ASSUMPTION]** pending primary research.

## Tiimo
*Strengths:* neurodivergent-specific positioning, visual timeline, colour-coded blocks, icons, AI co-planning, task decomposition, focus countdown timers, Apple Watch support, Anytime tasks, mood tracking.
*Reported weaknesses:* setup friction, ongoing maintenance burden, timer reliability complaints, sync issues, limited distraction blocking, calendar integration weaknesses.
*Opportunity:* move from visual planning into behavioural adaptation and automatic recovery.
*Threat:* best-resourced, best-positioned incumbent. Most likely to ship adaptive features. R9.

## Routinery
*Strengths:* guided routine execution, sequential steps, timers, repeatability, reduced decisions during routines.
*Opportunity:* extend guided execution beyond routines into an adaptive whole-day system.

## Structured
*Strengths:* simple linear visual timeline, calendar sync, low price.
*Opportunity:* add behavioural intelligence, execution support and recovery.
*Threat:* sets the category price anchor low. R11.

## Llama Life
*Strengths:* immediate task execution, countdown timers, timeboxing.
*Opportunity:* persistent learning, whole-day planning, automatic adaptation.

## Goblin Tools
*Strengths:* highly accessible AI decomposition, low cost, strong task-paralysis use case.
*Opportunity:* integrate decomposition into planning and execution rather than leaving it isolated.

## Habi
*Strengths:* timeline planning, app blocking, focus sounds, distraction defence.
*Opportunity:* build distraction defence into a broader personalised EF system.

## Inflow
*Strengths:* CBT content, ADHD education, coaching, body doubling, virtual co-working.
*Opportunity:* Inflow addresses education and intervention. This product addresses the real-time operational layer of everyday functioning. Different layer, plausible partner rather than competitor.

---

# Appendix C: Changelog

**v0.3** — Split into thesis and specification halves. Added: users and JTBD (21), assumptions and hypotheses with kill conditions (22), cold start strategy (23), technical architecture constraints (24), non-functional requirements (25), AI behaviour and failure modes (26), data/privacy/regulatory (27), safety and duty of care (28), business model and unit economics (29), measurement plan with the observability paradox resolved (30), functional requirement format with four worked examples (31), sequenced MVP with effort and release exit criteria (32), risk register (33), open questions register (34). Principles given falsifiable tests. Notification policy made concrete. Naming and brand moved to appendix. Competitive detail moved to appendix with assumption markers. Vision sections condensed by roughly a third.

**v0.2** — Initial full product definition.
