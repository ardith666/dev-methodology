---
name: dev-methodology
description: "Structured software development workflow: ask → spec → plan → implement → test → review. Use when building, creating, or implementing something."
---

# Dev Methodology

Structured development workflow + minimal code philosophy + quality discipline. Inspired by Superpowers, Ponytail, and Anthropic Agent Skills.

## Trigger

User asks to build/create/implement something, or says "dev mode", "methodology", "sprint".

## Core Philosophy

> "The best code is the code you never wrote." — Ponytail

Before writing ANY code, ask:
1. Does this need to exist at all?
2. Does a library/tool already solve this?
3. Does the platform have it natively?
4. Can it be one line?
5. Only then write code — minimum viable implementation

Red flags: installing a package for 3 lines, building when native element exists, abstraction for imaginary problems, "just in case" code.

## Surgical Changes (Karpathy)

Touch only what you must. Clean up only your own mess.

When editing existing code:
- Don't "improve" adjacent code, comments, or formatting
- Don't refactor things that aren't broken
- Match existing style, even if you'd do it differently
- If you notice unrelated dead code, mention it — don't delete it

When your changes create orphans:
- Remove imports/variables/functions that YOUR changes made unused
- Don't remove pre-existing dead code unless asked

The test: Every changed line should trace directly to the user's request.

Anti-patterns to catch:
- No features beyond what was asked
- No abstractions for single-use code
- No "flexibility" or "configurability" that wasn't requested
- No error handling for impossible scenarios
- If 200 lines could be 50, rewrite it
- The test: Would a senior engineer say this is overcomplicated? If yes, simplify.

## Decision Tree

```
User request → Is it a build task?
├─ Yes → Is the problem clearly understood?
│   ├─ Yes → Phase 2: Spec
│   └─ No → Phase 1: Understand
├─ No → Is it a fix/debug?
│   ├─ Yes → Diagnose first, fix minimal
│   └─ No → Handle directly
```

## Workflow

### Phase 1: Understand
- Ask clarifying questions BEFORE writing any code
- Identify: what problem, who uses it, constraints, success criteria
- Confirm understanding back to user
- **Gate:** User approves understanding before proceeding

### Phase 2: Spec
- Write minimal spec using template below
- Show in digestible chunks (not walls of text)
- Get explicit approval before proceeding
- **Gate:** User approves spec before proceeding

### Phase 3: Plan
- Break into small tasks (~15-30 min each)
- Mark dependencies between tasks
- Identify test cases per task
- Present as numbered checklist
- For each task: note existing solutions to check first
- **Gate:** User approves plan before proceeding

### Phase 4: Implement (Ponytail Mode)
- Work through tasks in order
- YAGNI strictly enforced — build only what spec says
- Each task:
  1. Check existing solutions first
  2. Implement minimal code
  3. Test
  4. Commit (atomic: one logical change)
- Prefer: native APIs > stdlib > existing packages > custom code
- Use subagents for parallel independent tasks

### Phase 5: Test
- Run all tests
- Manual smoke test if applicable
- Report pass/fail per task
- Verify against spec requirements

### Phase 6: Review + Self-Critique
- Summarize what was built
- Count lines of code — celebrate low numbers
- List deviations from spec (with reasons)
- Self-critique checklist:
  - [ ] Uses native/existing solutions where possible
  - [ ] Is it minimum code needed?
  - [ ] Any "just in case" additions?
  - [ ] Could any part be a one-liner?
  - [ ] Does it solve actual problem (not imagined)?
  - [ ] Is it the simplest thing that works?
- Suggest next steps or improvements

## Rules
- Never skip Phase 1-2 (understand + spec)
- Each phase requires user approval before next
- If user says "skip to code" — warn once, then comply
- Keep commits atomic
- Test before moving to next task
- Before writing code: "Is there a simpler way?"

## Templates

### Spec Template
```markdown
## Goal
[What are we building]

## Scope
- In: [what's included]
- Out: [what's not included]

## Data Model
[entities and relationships]

## API/UI
[interfaces]

## Constraints
[performance, budget, timeline]
```

### Task Template
```markdown
- [ ] Task 1: [description]
  - Depends on: none
  - Existing solution: [what already exists]
  - Test: [how to verify]
- [ ] Task 2: [description]
  - Depends on: Task 1
  - Existing solution: [what already exists]
  - Test: [how to verify]
```
