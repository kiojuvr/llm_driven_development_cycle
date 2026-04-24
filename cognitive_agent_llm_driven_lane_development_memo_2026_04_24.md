# LLM-Driven Lane Development Memo for cognitive-agent

Date: 2026-04-24  
Status: working practice memo  
Scope: cognitive-agent development workflow  

---

## 1. Purpose

This memo defines a lightweight development procedure for progressing the
`cognitive-agent` repository under LLM-driven development.

The goal is not to slow implementation down.

The goal is to prevent high-speed LLM work from opening unbounded architectural
change, especially around:

- cognitive-model semantics
- world-model semantics
- runtime protocol ownership
- adapter / state boundaries
- shell / flow-control contracts
- observability and trace surfaces

The core rule is:

> Do not open a new implementation lane merely because a change looks useful.
> Open a lane only when current repository evidence shows a concrete trigger.

---

## 2. Core Development Loop

The preferred loop is:

1. **Fix current state**
2. **Form a next-lane hypothesis**
3. **Audit for concrete trigger evidence**
4. **Open one bounded lane only if justified**
5. **Implement within that lane**
6. **Close out the lane**
7. **Return the repository to steady state**

This is a control procedure for architectural change.

It is especially useful when LLMs can generate implementation, refactoring, and
architecture suggestions faster than humans can safely review their boundary
impact.

---

## 3. Key Terms

### Current State

A written statement of the repository posture.

Typical fields:

- `active reorg line`
- `current bounded lane`
- `next bounded lane`
- relevant parked areas
- valid closeout families
- known resume conditions

A current-state document prevents stale or implicit assumptions from driving new
work.

### Audit

A bounded investigation that asks whether a new lane is justified.

An audit should not design the final solution.  
It should answer whether the repository contains enough evidence to proceed.

Useful audit evidence includes:

- blocked consumer
- contract drift
- ownership conflict
- duplicated semantics
- improper regression
- protocol-first / execution gap
- correctness or explainability impact

### Bounded Lane

A constrained implementation or design track with a narrow question, clear
scope, non-goals, and closeout criteria.

A lane is not just a task.  
It is an intentionally bounded change line.

### Closeout

A record of what the lane fixed, what it did not fix, who owns the resulting
semantics, and what would justify reopening the area later.

### Steady State

A valid repository posture where no currently evidenced bounded lane is open.

Steady state is not failure or stagnation.  
It means the repo should not be changed further without new evidence.

---

## 4. When to Use This Procedure

Use the audit/lane/closeout procedure for promotion-sensitive or
phase-opening work.

Examples:

- promoting `minimum_loop` behavior toward canonical surfaces
- changing ownership between `app`, `runtime_protocol`, `world_model`, or
  observability
- introducing reusable runtime control semantics
- modifying world-model lifecycle, update, prediction, or simulation contracts
- changing trace/result surfaces that future consumers may rely on
- turning local behavior into a reusable protocol

Do not require the full procedure for trivial local work.

Examples of local work:

- typo fixes
- test-only additions that do not change semantics
- local helper cleanup
- logging wording changes
- documentation cross-link fixes
- small code cleanup with no ownership or contract impact

---

## 5. Lane-Opening Conditions

Open a bounded lane only when at least one of the following is concrete.

### 5.1 Blocked Consumer

A named current or near-current workflow cannot proceed cleanly without the
change.

Examples:

- a runtime path cannot represent distinct post-turn outcomes
- a trace consumer cannot distinguish required states
- a world-model update path lacks a stable input contract

### 5.2 Contract Drift

Documentation, code, or tests disagree about who owns a meaning or behavior.

Examples:

- `app` treats a semantic as local convenience while docs describe it as a
  reusable protocol
- protocol types exist but runtime code bypasses them with ad hoc behavior

### 5.3 Ownership Conflict

Two layers appear to claim the same responsibility.

Examples:

- `runtime_protocol` appears to own transport while also implying semantic
  lifecycle ownership
- `app` local state begins to encode world-model semantics

### 5.4 Duplicated Semantics

Multiple paths encode similar control or semantic decisions independently.

Examples:

- several orchestration paths choose next actions differently
- multiple trace assembly helpers encode incompatible assumptions

### 5.5 Improper Regression

A previously closed boundary is weakened or bypassed.

Examples:

- a closeout says a behavior is parked, but live code starts depending on it
- a bounded defer becomes an implicit permanent contract

### 5.6 Correctness or Explainability Impact

The issue affects answer correctness, traceability, reproducibility, or review.

Examples:

- runtime behavior cannot explain why it continued, paused, delegated, or wrote
- a state transition cannot be traced back to its semantic owner

---

## 6. Non-Opening Conditions

Do not open a lane for these reasons alone.

- The design would be cleaner.
- The abstraction looks inevitable.
- The area is probably next.
- An LLM suggests a broad refactor.
- A future feature might need it.
- There is only a document-level discomfort with no live path evidence.
- One local convenience patch would be sufficient and honest.

These may justify an evidence packet or audit, but not a bounded implementation
lane by themselves.

---

## 7. Recommended Audit Structure

A good audit document should contain:

```markdown
# <Area> Audit (<date>)

## Purpose
## Current Starting Assumption
## Audit Question
## Scope
## Primary Inputs
## Core Checks
## Evidence Template
## Allowed Outcomes
## Non-Goals
## Completion Criteria
## Final Rule
```

Allowed outcomes should include a valid negative result.

Recommended pattern:

- **Outcome A:** no new lane justified / local handling remains valid
- **Outcome B:** contract pressure emerging / continue watching
- **Outcome C:** concrete trigger found / open one bounded lane

This makes “do not proceed” a first-class result rather than an ambiguous stall.

---

## 8. Recommended Lane Structure

When a lane is opened, the lane packet should state:

```markdown
# <Lane Name> (<date>)

## Status
## Trigger Evidence
## Entry Question
## Scope
## Non-Goals
## Affected Owners
## Expected Artifacts
## Implementation Constraints
## Validation Plan
## Closeout Criteria
## Reopen Conditions
```

The lane should be small enough that it can be closed cleanly.

If closeout criteria are hard to define, the lane is probably too broad.

---

## 9. Closeout Requirements

Every promotion-sensitive lane should end with a closeout.

The closeout should answer:

- What changed?
- What did not change?
- Which layer owns the resulting behavior?
- Which assumptions are now fixed?
- Which assumptions remain deferred?
- Which tests or docs validate the result?
- What would justify reopening this area?

A closeout should return the repo to an explicit steady state.

---

## 10. LLM Worker Usage

This procedure works especially well with LLM workers such as Codex, OpenCode,
or local model agents.

Give the worker a bounded packet, not a vague goal.

A good worker handoff should include:

- exact lane name
- entry question
- allowed files or modules to inspect first
- non-goals
- expected output artifacts
- tests to run
- closeout requirements
- instruction not to broaden the lane without evidence

Bad handoff:

> Improve the runtime architecture.

Better handoff:

> Execute the Runtime Next-Action Workflow Audit. Inspect at least one live
> post-turn call chain. Record evidence-template entries. Select exactly one
> allowed outcome. Do not design a full control plane.

The point is to make the LLM a bounded worker rather than an unbounded
architecture generator.

---

## 11. Practical Heuristics

### If the work touches meaning, audit first.

A change touches meaning when it affects what a state, event, trace, lifecycle,
control result, prediction, or output is supposed to mean.

### If the work only changes mechanics, local work may be fine.

Examples include local cleanup, tests, formatting, or small wiring fixes.

### If the work changes ownership, open a lane.

Ownership changes are high-risk because they affect future extension and review.

### If the work adds a reusable contract, open a lane.

Reusable contracts should not appear accidentally from convenience code.

### If there is no blocked consumer, prefer parking.

A parked area can be reentered later when new evidence appears.

### If an audit returns Outcome A, treat it as progress.

A negative result prevents unnecessary drift.

---

## 12. Anti-Patterns

Avoid these patterns:

### 12.1 Refactor by Momentum

Opening work because the previous lane ended and the repo feels idle.

### 12.2 Architecture by Aesthetic Preference

Changing boundaries because the structure looks cleaner, without a blocked
consumer or drift signal.

### 12.3 Convenience Promotion

Allowing app-local convenience behavior to become a de facto canonical surface.

### 12.4 Document-Only Confidence

Relying only on docs alignment when the question requires live code-path
inspection.

### 12.5 Infinite Discovery

Continuing to write audits after the trigger is already concrete enough to open
a bounded lane.

---

## 13. Minimal Decision Table

| Evidence found | Recommended action |
|---|---|
| No live pressure, docs aligned | Keep parked / steady state |
| Directional pressure only | Evidence packet or watchlist |
| Declared types but no runtime consumption | Audit as protocol-first / execution gap |
| Duplicate semantics across paths | Open or prepare bounded lane |
| Blocked consumer | Open bounded lane |
| Ownership conflict | Open bounded lane |
| Improper regression | Open corrective lane |
| Local cleanup only | Do local task without full lane process |

---

## 14. Why This Matters for cognitive-agent

`cognitive-agent` is not only an application.  
It is an architecture for maintaining and using structured cognition.

Therefore, many changes are not ordinary feature work.  
They are changes to meaning, ownership, memory, prediction, control, or
explainability.

The audit/lane/closeout procedure keeps those changes governed.

The practical benefit is that high-speed LLM implementation can continue
without letting the repository drift into accidental architecture.

---

## 15. Short Form

Use this as the daily operating rule:

> Local mechanics can be fixed locally.  
> Reusable meaning requires evidence.  
> Evidence opens one bounded lane.  
> A bounded lane must close out.  
> After closeout, return to steady state.

