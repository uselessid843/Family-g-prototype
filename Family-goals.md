# Family Financial Goals Tracker — Product Requirements Document

## Overview

A personal finance goal-tracking web app for a family with two active financial goals. The app displays two independent "savings tickers" — each with its own progress bar, milestone tracking, and motivational feedback. Built to be fun, celebratory, and easy to update manually.

---

## Goals

### Goal 1: Family Savings — $120,000 Target

**Sub-goals (shown as nested progress):**

| Sub-goal | Target |
|---|---|
| Emergency Fund | $50,000 |
| House Down Payment | $70,000 |
| Combined Target | $120,000 |

**Behavior:**

- On first load, prompt the user to enter their current savings balance (one-time setup, editable anytime)
- Display a single combined progress bar toward $120k, with two visual markers showing the $50k and $70k milestones
- Show dollar amount saved, dollar amount remaining, and percentage complete
- Allow manual "Add Savings" updates (e.g. user enters $500 → balance updates)
- Celebrate milestone moments:
  - Crossing $50k → emergency fund complete celebration (confetti or fun visual)
  - Crossing $120k → both goals hit celebration (big win animation)
- Persist balance in local storage so it survives page refreshes

---

### Goal 2: Lauren's Loan Paydown

**Configuration:**

| Field | Value |
|---|---|
| Target balance | User-defined (editable; defaults to $21,458 placeholder until set) |
| Monthly payment | $2,200/month |

**Behavior:**

- On first load, prompt user to enter the current loan balance (editable anytime)
- Display a countdown progress bar (starts full, drains toward zero as payments are made)
- Show:
  - Current balance remaining
  - Total paid so far
  - Months remaining at $2,200/month pace
  - Estimated payoff date based on $2,200/month cadence
- Allow manual "Log Payment" updates (user enters payment amount → balance decreases)
- Celebrate when balance hits $0 — big win animation
- Persist in local storage

---

## Shared UI/UX Requirements

- **Single-page app** — both goals visible on one screen, side by side or stacked
- **Fun & motivating aesthetic** — bold progress bars, bright colors, friendly typography, emoji-friendly
- **Milestone badges or checkmarks** when sub-goals are completed
- **Mobile-friendly layout** (responsive design)
- **No backend** — all state managed in local storage
- **Tech stack** — React (JSX artifact) or plain HTML/CSS/JS, chosen based on simplicity

---

## User Flows

### First Load — Savings Goal Setup
1. App detects no saved balance in local storage
2. Modal or inline prompt: "What is your current savings balance?"
3. User enters value → stored in local storage → progress bar renders
4. Prompt dismisses; main dashboard shown

### First Load — Loan Goal Setup
1. App detects no saved loan balance in local storage
2. Modal or inline prompt: "What is Lauren's current loan balance?"
3. User enters value → stored in local storage → countdown bar renders
4. Prompt dismisses; main dashboard shown

### Add Savings
1. User clicks "Add Savings" button
2. Input field appears: "How much did you save?"
3. User enters amount → current balance increments
4. Progress bar updates; milestone check fires
5. Confetti animation triggers if $50k or $120k threshold is crossed

### Log Loan Payment
1. User clicks "Log Payment" button
2. Input field appears: "How much did you pay?"
3. User enters amount → loan balance decrements
4. Countdown bar updates; payoff date recalculates
5. Win animation triggers if balance reaches $0

### Edit Starting Values
- Both goals expose an "Edit" option to re-enter the base balance at any time
- Editing does not reset progress history display, only the current balance figure

---

## Milestone & Celebration Spec

| Event | Trigger | Celebration |
|---|---|---|
| Emergency Fund complete | Savings balance crosses $50,000 | Confetti burst + badge unlocked |
| All savings goals complete | Savings balance crosses $120,000 | Full-screen confetti + "You did it!" message |
| Loan paid off | Loan balance reaches $0 | Full-screen animation + "Debt free!" message |

---

## Data Model (Local Storage)

```json
{
  "savings": {
    "currentBalance": 0,
    "target": 120000,
    "milestones": [50000, 120000],
    "milestonesReached": []
  },
  "loan": {
    "currentBalance": 21458,
    "originalBalance": 21458,
    "monthlyPayment": 2200
  }
}
```

---

## Out of Scope (v1)

- User authentication
- Bank sync / API integrations
- Multi-user access
- Historical charts or transaction logs
- Push notifications or reminders

---

## Success Criteria

- Both goals render correctly from local storage on page refresh
- Progress bars accurately reflect entered balances
- Milestone celebrations fire at correct thresholds
- Payoff date estimate updates after each loan payment logged
- Layout is usable on mobile (320px+) and desktop
