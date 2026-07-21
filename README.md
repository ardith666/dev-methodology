# 🧠 Dev Methodology

> A structured software development workflow for AI coding agents — combining the best patterns from four proven frameworks into one cohesive methodology.

## Why This Exists

AI coding agents are powerful but prone to specific failure modes:
- **Over-engineering** — building abstractions nobody asked for
- **Silent assumptions** — picking interpretations without asking
- **Scope creep** — refactoring adjacent code during unrelated changes
- **Skipping understanding** — jumping straight to code

Dev Methodology addresses all four with a single, battle-tested workflow.

## What It Combines

| Source | What We Took | Why |
|--------|-------------|-----|
| [**Superpowers**](https://github.com/obra/superpowers) | Phase-gated workflow (ask → spec → plan → implement → test → review) | Prevents building the wrong thing. Each phase requires user approval before proceeding. |
| [**Ponytail**](https://github.com/DietrichGebert/ponytail) | Minimal code philosophy ("best code is code you never wrote") | Reduces code volume ~54%, cost ~20%, while staying 100% safe. |
| [**Anthropic Agent Skills**](https://github.com/anthropics/skills) | Decision trees, self-critique checklists, progressive disclosure | Structured branching logic instead of linear instructions. Quality gates at every phase. |
| [**Karpathy Guidelines**](https://github.com/multica-ai/andrej-karpathy-skills) | Surgical changes — touch only what you must | Prevents orthogonal edits, drive-by refactoring, and unintended side effects. |

## Why Combine Instead of Pick One?

Each framework solves a **different** problem:

- **Superpowers** tells you **when** to do things (workflow order)
- **Ponytail** tells you **how much** to build (as little as possible)
- **Anthropic Skills** tells you **how to structure** instructions (decision trees + quality gates)
- **Karpathy** tells you **where** to touch (only what's needed, nothing else)

Together they form a complete system. Alone, each has blind spots.

## The Workflow

```
Understand → Spec → Plan → Implement → Test → Review
     ↑          ↑       ↑        ↑          ↑       ↑
   Gate       Gate    Gate    Ponytail   Verify   Self-Critique
```

### Phase 1: Understand
Ask clarifying questions BEFORE writing any code. Never assume.

### Phase 2: Spec
Write minimal spec. Show in digestible chunks. Get explicit approval.

### Phase 3: Plan
Break into small tasks. Mark dependencies. Identify test cases.

### Phase 4: Implement (Ponytail Mode)
Check existing solutions → Implement minimal → Test → Commit. One logical change per commit.

### Phase 5: Test
Run all tests. Report pass/fail per task.

### Phase 6: Review + Self-Critique
Celebrate low LOC. Run quality checklist. Suggest improvements.

## Three Core Principles

### 🎯 Minimal Code (Ponytail)
Before writing ANY code:
1. Does this need to exist at all?
2. Does a library/tool already solve this?
3. Does the platform have it natively?
4. Can it be one line?
5. **Only then write code.**

### 🔪 Surgical Changes (Karpathy)
When editing existing code:
- Don't "improve" adjacent code
- Don't refactor things that aren't broken
- Match existing style
- Every changed line traces to user's request

### 🚦 Phase Gates (Superpowers)
Each phase requires user approval. No skipping ahead (without a warning).

## Installation

### 🦜 OpenClaw

```bash
cp SKILL.md ~/.openclaw/workspace/skills/dev-methodology/
```

Or via ClawHub (coming soon):
```bash
clawhub install dev-methodology
```

### 🤖 Claude Code

**Option A:** Project root
```bash
curl -o CLAUDE.md https://raw.githubusercontent.com/ardith666/dev-methodology/main/SKILL.md
```

**Option B:** Append to existing CLAUDE.md
```bash
echo "" >> CLAUDE.md
curl https://raw.githubusercontent.com/ardith666/dev-methodology/main/SKILL.md >> CLAUDE.md
```

**Option C:** Claude Code Plugin
```bash
/plugin install dev-methodology@ardith666/dev-methodology
```

### 🔥 Hermes

Add to your Hermes project config or paste into system prompt:
```bash
curl -o .hermes/skills/dev-methodology.md https://raw.githubusercontent.com/ardith666/dev-methodology/main/SKILL.md
```

Or reference in your Hermes config:
```json
{
  "skills": [".hermes/skills/dev-methodology.md"]
}
```

### 🐍 OpenCode

Place as project-level instruction:
```bash
cp SKILL.md .opencode/instructions.md
```

Or add to global config:
```bash
cp SKILL.md ~/.opencode/instructions.md
```

### 🤗 Pi Agent

Add to your Pi workspace:
```bash
cp SKILL.md ~/.pi/skills/dev-methodology.md
```

### 💻 Cursor

Create project rule:
```bash
mkdir -p .cursor/rules
cp SKILL.md .cursor/rules/dev-methodology.mdc
```

### 🐙 GitHub Copilot

Add to `.github/copilot-instructions.md`:
```bash
mkdir -p .github
cp SKILL.md .github/copilot-instructions.md
```

### 🏭 Factory Droid
```bash
droid plugin install https://github.com/ardith666/dev-methodology
```

### 🧩 Kimi Code
```
/plugins
→ Search: dev-methodology
→ Install
```

### 🔧 Codex (OpenAI)

**Codex App:** Plugins → Search "dev-methodology" → Install

**Codex CLI:**
```bash
/plugins
→ Search: dev-methodology
→ Install Plugin
```

### 📝 Any Other AI Tool

Copy `SKILL.md` content into:
- System prompt / custom instructions
- Project-level `AGENTS.md` / `CLAUDE.md` / `.cursorrules` / similar
- Any file the AI tool reads as context on startup

The methodology is framework-agnostic — the principles work with any AI coding agent.

## Usage

Just say:
- "dev mode" / "methodology" / "sprint" — activates the workflow
- Or simply ask to build/create something — the methodology triggers automatically

## Quality Checklist

After every implementation:
- [ ] Uses native/existing solutions where possible
- [ ] Is it minimum code needed?
- [ ] Any "just in case" additions?
- [ ] Could any part be a one-liner?
- [ ] Does it solve actual problem (not imagined)?
- [ ] Is it the simplest thing that works?
- [ ] Every changed line traces to user's request?
- [ ] Would a senior engineer say this is overcomplicated?

## License

MIT
