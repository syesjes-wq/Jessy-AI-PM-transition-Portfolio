# Product Requirements Document — HabitlyKids V1

**Status:** Personal app, actively in use
**Platform:** iOS, Android (PWA)
**Users:** One family — two parents, two children aged 4 and 6

---

## What this is

HabitlyKids is a habit-tracking and reward app I built for my own home. Parents define daily habits for their children, assign star values, and curate a reward store. Children complete their habits, earn stars, and redeem them for rewards they have chosen themselves.

The product is two-sided: a parent management layer and a separate child-facing experience, each purpose-built for their user.

---

## The problem it solves

See: [Jobs to Be Done](./habitlykids-job-to-be-done.md)

The short version: daily routines with young children were a constant struggle. The goal was to give children their own motivation to complete habits — so the parent is no longer the one doing the enforcing.

---

## Who it is for

**Primary user — the parent**
Sets up habits, manages the reward store, monitors progress, and fulfils rewards. Needs a fast, frictionless management experience — most interactions happen in under 30 seconds.

**Secondary user — the child (ages 4–8)**
Completes daily tasks, checks their star balance, and works toward a reward they have chosen. Needs a simple, exciting experience with large touch targets, clear visual progress, and a reason to open the app every day.

---

## V1 goals

1. A child can see their habits for the day and mark them complete independently
2. A parent can create, assign, and manage habits across two children from one screen
3. A child can choose a reward target and see their progress toward it
4. A parent can fulfil a reward in one tap

---

## What is in V1

| Epic | What it covers |
|---|---|
| Onboarding & profiles | Family account, two child profiles, parent PIN, multi-device sync |
| Habit management | Create, edit, assign, activate/deactivate, silent observation (0-star) mode |
| Reward store | Parent-curated rewards, four categories, one-tap fulfilment |
| Parent home | Child summary cards, star management, activity journal |
| Child experience | Daily task cards, star balance, streak, reward progress bar, daily micro-moment |
| Progress & journal | Completion history, parent journal |

---

## What is out of V1

- **AI-generated insights** — parent home surfaces one insight card per child generated from the child's completion history via the Anthropic API. Designed and partially built, not yet in V1
- **Mastery indicators** (Day X of 21 on habit cards) — designed, not yet built
- **Age-appropriate habit suggestions** — designed, not yet built
- **Functional PIN** — designed, not yet built
- **Streak display on child home screen** — designed, not yet built
- **Shared rewards** — where both children must reach their own star target before a family experience is redeemed. Validated by real family behaviour, scoped to V2
- **Joint savings goal** — where two children pool stars toward one reward. Validated by real family behaviour, scoped to V2
- **Relapse detection** — early warning when a child's completion rate drops after a streak. V2

---

## Success metric

One benchmark drives every product decision:

> *Would this feature create the 6am morning?*

See: [Origin and Research](./habitlykids-origin-and-research.md) — the moment on day 14 when both boys woke up, got dressed, and were ready for school before being asked. That outcome — a child acting on their own motivation without a parent prompt — is what V1 is built to produce.
