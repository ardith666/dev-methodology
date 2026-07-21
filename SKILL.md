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

## Knowledge Tracking

Setiap agent yang kerja pakai metodologi ini WAJIB baca & tulis knowledge files. Tujuannya:
- Agent lain bisa lanjutin pekerjaan tanpa tanya ulang
- User bisa pakai structured notes buat Obsidian atau workflow lain
- Keputusan & alasan di-skip/delay terdokumentasi

### Knowledge Files

| File | Isi | Wajib? |
|------|-----|--------|
| `knowledge/history.md` | Timeline pekerjaan (implementasi, skip, decision) | ✅ Ya |
| `knowledge/ideas.md` | Ide yg dipertimbangkan tapi belum dikerjakan | ⬜ Opsional |
| `knowledge/external-references.md` | Link/docs/repo yg dibaca | ⬜ Opsional |

### Flow Wajib

**Sebelum mulai kerja:**
1. Baca `knowledge/history.md` — tau state terakhir
2. Baca `knowledge/ideas.md` — cek ide yg mungkin relevan
3. Kalau knowledge menunjukkan progress sebelumnya, skip phase yg udah selesai

**Setelah tiap phase selesai:**
1. Tulis entry ke `knowledge/history.md`
2. Format entri:
   - Timestamp, feature name, status
   - Decision (implement/skip/delay/drop) + alasan singkat
   - Next steps
3. Max 5 baris per entri — ringkas, no filler

### Format Entri

**Implementation log:**
```
- [YYYY-MM-DD HH:MM] [feature/name]: [ringkasan]
  - Code: [X] lines | Tests: [Y] | Commit: [hash]
  - Status: ✅/❌/⚠️
  - Decision: implement/skip/delay
  - Reason: [alasan singkat]
  - Next: [langkah selanjutnya]
```

**Skipped item:**
```
- [YYYY-MM-DD HH:MM] [idea/feature]: dipertimbangkan, di-skip
  - Value: [kenapa sempat dipertimbangkan]
  - Decision: skip/delay
  - Reason: [alasan spesifik]
  - Might revisit: [kapan/kalau]
```

**Decision entry:**
```
- [YYYY-MM-DD HH:MM] Decision: [implement/skip/delay]
  - Problem: [apa yg dicoba dipecahkan]
  - Options: [pilihan yg dipertimbangkan]
  - Chosen: [apa yg dipilih]
  - Why: [alasan spesifik]
```

### Aturan Penulisan

- **Brevity**: Satu entri max 5 baris
- **Akurat**: Timestamp, feature name, status jelas
- **Action-oriented**: Fokus action, bukan deskripsi task
- **No filler**: Hindari "then I", "after that", "finally"
- **Multi-purpose**: Format markdown terstruktur → user bisa copy-paste ke Obsidian, Notion, atau workflow lain

### Integrasi per Phase

| Phase | Action Knowledge |
|-------|-----------------|
| Phase 1 Understand | Baca knowledge dulu sebelum tanya. Skip kalau udah terjawab |
| Phase 2 Spec | Catat decision dari spec |
| Phase 3 Plan | Catat breakdown task + dependencies |
| Phase 4 Implement | Tulis entry setelah tiap commit |
| Phase 5 Test | Catat test results (pass/skip/fail) |
| Phase 6 Review | Tulis summary + lessons learned |

### Example

Agent mulai tugas "Buat JWT auth endpoint":

1. Baca `knowledge/history.md` → belum ada auth work sebelumnya
2. Tulis decision:
```
- [2026-07-21 11:00] Decision: implement JWT auth endpoint
  - Problem: Endpoint perlu authenticated access
  - Options: OAuth2, JWT stateless, session cookie
  - Chosen: JWT stateless
  - Why: Simpel, scalable, stateless
```
3. Implement & tulis:
```
- [2026-07-21 11:30] JWT auth endpoint:
  - Code: 47 lines | Tests: 3 | Commit: abc123
  - Status: ✅
  - Decision: implement
  - Reason: JWT middleware + protected routes
  - Next: Integration test
```
4. Agent selanjutnya langsung tau state & bisa lanjut
