# 🧠 Dev Methodology

> A structured software development workflow for AI coding agents — combining the best patterns from four proven frameworks into one cohesive methodology, with persistent knowledge that follows your project.

## Why This Exists

AI coding agents are powerful but prone to specific failure modes:
- **Over-engineering** — building abstractions nobody asked for
- **Silent assumptions** — picking interpretations without asking
- **Scope creep** — refactoring adjacent code during unrelated changes
- **Skipping understanding** — jumping straight to code
- **Context loss** — agents forget everything between sessions, wasting tokens and hallucinating

Dev Methodology addresses all five with a single, battle-tested workflow.

## What It Combines

| Source | What We Took | Why |
|--------|-------------|-----|
| [**Superpowers**](https://github.com/obra/superpowers) | Phase-gated workflow (ask → spec → plan → implement → test → review) | Prevents building the wrong thing. Each phase requires user approval before proceeding. |
| [**Ponytail**](https://github.com/DietrichGebert/ponytail) | Minimal code philosophy ("best code is code you never wrote") | Reduces code volume ~54%, cost ~20%, while staying 100% safe. |
| [**Anthropic Agent Skills**](https://github.com/anthropics/skills) | Decision trees, self-critique checklists, progressive disclosure | Structured branching logic instead of linear instructions. Quality gates at every phase. |
| [**Karpathy Guidelines**](https://github.com/multica-ai/andrej-karpathy-skills) | Surgical changes — touch only what you must | Prevents orthogonal edits, drive-by refactoring, and unintended side effects. |
| **Knowledge Capture** | Persistent project context via `knowledge/KNOWLEDGE.md` | Eliminates context loss between sessions — no more wasted tokens or hallucinations from re-learning. |

## Why Combine Instead of Pick One?

Each framework solves a **different** problem:

- **Superpowers** tells you **when** to do things (workflow order)
- **Ponytail** tells you **how much** to build (as little as possible)
- **Anthropic Skills** tells you **how to structure** instructions (decision trees + quality gates)
- **Karpathy** tells you **where** to touch (only what's needed, nothing else)
- **Knowledge Capture** tells you **what happened** (persistent context across sessions)

Together they form a complete system. Alone, each has blind spots.

## Knowledge Portability

The `knowledge/KNOWLEDGE.md` file is **plain markdown** — you own the data. Transfer it anywhere:

| Destination | How |
|-------------|-----|
| **Obsidian** | Copy `knowledge/` folder into your vault. Wikilinks and backlinks work instantly. |
| **Notion** | Import `KNOWLEDGE.md` as a page. Markdown tables and checklists render natively. |
| **GitHub** | Commit `knowledge/` with your code. GitHub renders markdown in the repo. |
| **GitBook / Docusaurus** | Add `knowledge/` to your docs folder. Structure is already compatible. |
| **Any text editor** | It's just markdown. Open it anywhere. |

No vendor lock-in. No export scripts. Your project knowledge stays portable and human-readable.

## The Workflow

```
Understand → Spec → Plan → Implement → Test → Review → Knowledge
     ↑          ↑       ↑        ↑          ↑       ↑        ↑
   Gate       Gate    Gate    Ponytail   Verify   Self-Critique  Capture
```

Every phase gate auto-updates `knowledge/KNOWLEDGE.md` — the single source of truth for project context. New sessions read this file first, eliminating context loss and hallucination.

### Phase 1: Understand
Ask clarifying questions BEFORE writing any code. Never assume.
**Knowledge:** Create `knowledge/KNOWLEDGE.md` with Vision section.

### Phase 2: Spec
Write minimal spec. Show in digestible chunks. Get explicit approval.
**Knowledge:** Add Architecture + Decisions sections.

### Phase 3: Plan
Break into small tasks. Mark dependencies. Identify test cases.
**Knowledge:** Add Progress checklist (all unchecked).

### Phase 4: Implement (Ponytail Mode)
Check existing solutions → Implement minimal → Test → Commit. One logical change per commit.
**Knowledge:** Update Progress, add Learnings + Files as they emerge.

### Phase 5: Test
Run all tests. Report pass/fail per task.
**Knowledge:** Update Progress with test results.

### Phase 6: Review + Self-Critique
Celebrate low LOC. Run quality checklist. Suggest improvements.
**Knowledge:** Add Next section with follow-ups and known issues.

## Knowledge Capture

Every project gets a `knowledge/KNOWLEDGE.md` file — append-only, timestamped, single source of truth.

**The problem it solves:** Agents lose context between sessions. Without persistent knowledge, each session starts from zero — wasting tokens re-learning the codebase and hallucinating from incomplete understanding.

**How it works:**
- Created at Phase 1 (Understand)
- Updated at every phase gate (append only, never delete)
- Read first when starting any new session on this project

**What it tracks:**
- Vision — what we're building and why
- Architecture — tech stack, structure, patterns
- Decisions — what was chosen and why (with rejected alternatives)
- Progress — done/blocked/todo checklist
- Learnings — pitfalls, discoveries, what worked
- Files — what was touched and why
- Next — follow-ups, known issues, debt

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
