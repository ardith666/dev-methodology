<p align="center">
<pre align="center">
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@=-..-...=@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@#-.-@@=.#-.=@@@@@@@=.=@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@=..#--@=....@@@@@@@--#=.=@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@=..-@#.=-...-.#@@@@@@@#--.-#@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@#...-@@=...-...@@@#---...===-..=@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@-=.-.-#@@#...--.=@@@=.=@@-......-#@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@# ...===#@@@-.....-#@@#..-#@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@#.....-=###@@@=.....-==###-.-@@#=@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@--@@#-.-=-..-=#@@@@@@@=-. .-==##..@=.#@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@-..-##....-========##@@@@@=..-=##.---#@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@-.-....-....----=---.-#@@@@-.-==#.-.=@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@#...-==-..... . ..=#@@@@@@#..#=#....#@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@-....####@@@@@@@@@@@@@@#-.-###....#@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@#-..--===#######@@#=-..-###-.  -@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@##=......---....-=#==-.  .-#@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@=. ...-.............. ..---.-@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@-.=.............-------..#@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@=..-.-@@#####@@#....--..#@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@#-........-#@@@@@@#......=@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@####=..=#@@@@@@@@@@@#-=@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
</pre>
</p>

<p align="center" style="margin-top: -20px;">
  <b>Structured workflow + minimal code + persistent knowledge</b><br>
  <i>For AI coding agents that forget nothing.</i>
</p>

<p align="center">
  <a href="#quick-start">Quick Start</a> •
  <a href="#the-workflow">Workflow</a> •
  <a href="#installation">Installation</a> •
  <a href="#knowledge-portability">Knowledge</a>
</p>

---

## Why This Exists

AI coding agents are powerful but make predictable mistakes:

```
 ❌ Over-engineering      → building abstractions nobody asked for
 ❌ Silent assumptions    → picking interpretations without asking
 ❌ Scope creep           → refactoring adjacent code during changes
 ❌ Skipping understanding→ jumping straight to code
 ❌ Context loss          → forgetting everything between sessions
```

**Dev Methodology** fixes all five — with one workflow.

---

## The DNA

Five sources, five problems solved:

```
 ┌─────────────────────────────────────────────────────────────────┐
 │                        DEV METHODOLOGY                         │
 ├──────────────┬──────────────┬──────────────┬────────────────────┤
 │ SUPERPOWERS  │  PONYTAIL    │  ANTHROPIC   │     KARPATHY      │
 │              │              │   SKILLS     │                    │
 │  🕐 WHEN     │  📏 HOW MUCH │  🏗️ HOW      │  🔪 WHERE          │
 │              │              │              │                    │
 │  Workflow    │  Minimal     │  Decision    │  Surgical          │
 │  order       │  code        │  trees +     │  changes —         │
 │  (gates at  │  philosophy  │  checklists  │  touch only        │
 │  every phase)│              │              │  what's needed     │
 └──────────────┴──────────────┴──────────────┴────────────────────┘
                                    +
                        ┌───────────────────┐
                        │  📚 KNOWLEDGE     │
                        │                   │
                        │  Persistent       │
                        │  project context  │
                        │  across sessions  │
                        └───────────────────┘
```

---

## The Workflow

```
  ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
  │          │    │          │    │          │    │          │    │          │    │          │    │          │
  │ 1.UNDER- │───▶│ 2.SPEC   │───▶│ 3.PLAN   │───▶│ 4.IMPLE- │───▶│ 5.TEST   │───▶│ 6.REVIEW │───▶│ 7.KNOW-  │
  │  STAND   │    │          │    │          │    │  MENT    │    │          │    │          │    │  LEDGE   │
  │          │    │          │    │          │    │          │    │          │    │          │    │          │
  └────┬─────┘    └────┬─────┘    └────┬─────┘    └────┬─────┘    └────┬─────┘    └────┬─────┘    └────┬─────┘
       │               │               │               │               │               │               │
       ▼               ▼               ▼               ▼               ▼               ▼               ▼
  ┌─────────┐    ┌─────────┐    ┌─────────┐    ┌─────────┐    ┌─────────┐    ┌─────────┐    ┌─────────┐
  │  GATE:  │    │  GATE:  │    │  GATE:  │    │PONYTAIL │    │VERIFY   │    │  SELF-  │    │ CAPTURE │
  │ approve │    │ approve │    │ approve │    │ minimal │    │ all     │    │ CRITIQUE│    │ context │
  │ before  │    │ before  │    │ before  │    │ code +  │    │ tests   │    │ + low   │    │ to file │
  │ next    │    │ next    │    │ next    │    │ commit  │    │ pass    │    │ LOC     │    │         │
  └─────────┘    └─────────┘    └─────────┘    └─────────┘    └─────────┘    └─────────┘    └─────────┘
       │               │               │               │               │               │               │
       ▼               ▼               ▼               ▼               ▼               ▼               ▼
   📚 Vision      📚 Arch +      📚 Progress    📚 Progress    📚 Progress    📚 Next        ✅ Done
                   Decisions      (unchecked)    (check done)   (results)      (follow-ups)
```

> Every phase auto-updates `knowledge/KNOWLEDGE.md`. New sessions read it first → **zero context loss**.

---

## Quick Start

```bash
# Clone the skill
git clone https://github.com/ardith666/dev-methodology.git

# Copy to your project
cp dev-methodology/SKILL.md your-project/

# Or install globally (OpenCode)
cp dev-methodology/SKILL.md ~/.agents/skills/dev-methodology/SKILL.md
```

Then just say: **"dev mode"** or ask to build something.

---

## Knowledge Portability

Your `knowledge/KNOWLEDGE.md` is **plain markdown** — own the data, export anywhere:

```
 knowledge/
 ├── knowledge/KNOWLEDGE.md  ← single source of truth
 │
 ├──▶ Obsidian    → copy folder into vault (wikilinks work instantly)
 ├──▶ Notion      → import as page (tables + checklists render natively)
 ├──▶ GitHub      → commit with code (renders in repo)
 ├──▶ GitBook     → add to docs folder (structure compatible)
 └──▶ Any editor  → it's just markdown
```

**No vendor lock-in. No export scripts.**

---

## What Each Phase Does

### Phase 1: Understand 🤔
```
 Ask questions → Identify problem → Confirm with user
 └─ 📚 Create knowledge/KNOWLEDGE.md with Vision section
```

### Phase 2: Spec 📝
```
 Write minimal spec → Show in chunks → Get approval
 └─ 📚 Add Architecture + Decisions sections
```

### Phase 3: Plan 📋
```
 Break into tasks → Mark dependencies → Identify test cases
 └─ 📚 Add Progress checklist (all unchecked)
```

### Phase 4: Implement ⚡
```
 Check existing → Implement minimal → Test → Commit
 └─ 📚 Update Progress, add Learnings + Files
```

### Phase 5: Test ✅
```
 Run all tests → Manual smoke test → Report pass/fail
 └─ 📚 Update Progress with test results
```

### Phase 6: Review 🎯
```
 Summarize → Count LOC → Self-critique checklist
 └─ 📚 Add Next section with follow-ups
```

---

## Core Principles

### 🎯 Minimal Code (Ponytail)
```
 Before writing ANY code:
   1. Does this need to exist at all?
   2. Does a library/tool already solve this?
   3. Does the platform have it natively?
   4. Can it be one line?
   5. Only then write code.
```

### 🔪 Surgical Changes (Karpathy)
```
 When editing existing code:
   ✗ Don't "improve" adjacent code
   ✗ Don't refactor things that aren't broken
   ✓ Match existing style
   ✓ Every changed line traces to user's request
```

### 🚦 Phase Gates (Superpowers)
```
 Each phase requires user approval.
 No skipping ahead (without a warning).
```

---

## Installation

<details>
<summary><b>Claude Code</b></summary>

```bash
# Option A: Project root
curl -o CLAUDE.md https://raw.githubusercontent.com/ardith666/dev-methodology/main/SKILL.md

# Option B: Append to existing
echo "" >> CLAUDE.md
curl https://raw.githubusercontent.com/ardith666/dev-methodology/main/SKILL.md >> CLAUDE.md

# Option C: Plugin
/plugin install dev-methodology@ardith666/dev-methodology
```
</details>

<details>
<summary><b>OpenCode</b></summary>

```bash
# Project-level
cp SKILL.md .opencode/instructions.md

# Global
cp SKILL.md ~/.agents/skills/dev-methodology/SKILL.md
```
</details>

<details>
<summary><b>Cursor</b></summary>

```bash
mkdir -p .cursor/rules
cp SKILL.md .cursor/rules/dev-methodology.mdc
```
</details>

<details>
<summary><b>GitHub Copilot</b></summary>

```bash
mkdir -p .github
cp SKILL.md .github/copilot-instructions.md
```
</details>

<details>
<summary><b>Hermes</b></summary>

```bash
curl -o .hermes/skills/dev-methodology.md https://raw.githubusercontent.com/ardith666/dev-methodology/main/SKILL.md
```
</details>

<details>
<summary><b>Pi Agent</b></summary>

```bash
cp SKILL.md ~/.pi/skills/dev-methodology.md
```
</details>

<details>
<summary><b>Factory Droid / Kimi / Codex / Other</b></summary>

```bash
# Factory Droid
droid plugin install https://github.com/ardith666/dev-methodology

# Kimi Code
/plugins → Search: dev-methodology → Install

# Codex
/plugins → Search: dev-methodology → Install

# Any tool: copy SKILL.md to system prompt / AGENTS.md / .cursorrules
```
</details>

---

## Quality Checklist

After every implementation:

```
 [ ] Uses native/existing solutions where possible
 [ ] Is it minimum code needed?
 [ ] Any "just in case" additions?
 [ ] Could any part be a one-liner?
 [ ] Does it solve actual problem (not imagined)?
 [ ] Is it the simplest thing that works?
 [ ] Every changed line traces to user's request
 [ ] Would a senior engineer say this is overcomplicated?
```

---

## License

MIT
