# FlowState SE - Document Templates
## All Template Files for Framework Implementation

**Version**: 2.5.0
**Last Updated**: 2025-11-24

---

## 📖 Document Purpose

This file contains **all templates** that AI uses to generate FlowState files during initialization.

**For AI**: Copy these templates and populate with project-specific values

**For Users**: Reference to understand what each file contains

---

## Table of Contents

1. [Filename Modes & Git Privacy](#filename-modes--git-privacy)
2. [.git/info/exclude Template](#gitinfoexclude-template)
3. [Universal FlowState Files](#universal-flowstate-files)
   - [FLOWSTATE.md Template](#flowstatemd-template)
   - [TASKS.md Template](#tasksmd-template)
   - [SESSION.md Template](#sessionmd-template)
   - [Master Plan Template](#master-plan-template)
4. [Platform Adapter Files](#platform-adapter-files)
   - [CLAUDE.md Template (Claude Code)](#claudemd-template-claude-code)
   - [AGENTS.md Template (Copilot/Codex)](#agentsmd-template-copilotcodex)
   - [flowstate.mdc Template (Cursor)](#flowstatemdc-template-cursor)
   - [.cursorrules Template (Cursor Legacy)](#cursorrules-template-cursor-legacy)
5. [Supporting Files](#supporting-files)
   - [Plan Document Template](#plan-document-template)

---

## Filename Modes & Git Privacy

### Overview

FlowState v2.2 supports **two filename modes** to balance visibility with privacy:

1. **Standard Mode** (Default) - Clear, descriptive filenames
2. **Obfuscated Mode** - Dotfile-based stealth filenames

### Filename Mapping Table [UPDATED in v2.5]

**v2.5 Default**: All FlowState files live in `.flowstate/` directory

| Standard Mode | Obfuscated Mode | Purpose |
|---------------|-----------------|---------|
| `.flowstate/config.md` | `.flowstate/.config.md` | Project configuration & Meta-Rules |
| `.flowstate/tasks.md` | `.flowstate/.tasks.md` | Task board |
| `.flowstate/session.md` | `.flowstate/.session.md` | Session state tracking |
| `.flowstate/archive/tasks-archive.md` | `.flowstate/archive/.tasks-archive.md` | Completed tasks archive [NEW] |
| `.flowstate/plans/PLAN-*.md` | `.flowstate/plans/.plan-*.md` | Feature plans |
| `.flowstate/logs/*.log` | `.flowstate/logs/.log-*.txt` | Evidence trails |
| `.flowstate/version.txt` | `.flowstate/version.txt` | Framework version |
| `docs/[project]-master-plan.md` | `docs/.master-plan.md` | Phase roadmap (user-facing) |
| `CLAUDE.md` | `.ai-adapter.md` | Platform adapter (Claude Code) - stays at root |
| `AGENTS.md` | `.ai-adapter.md` | Platform adapter (Copilot/Codex) - stays at root |
| `.cursor/rules/flowstate.mdc` | `.cursor/rules/project.mdc` | Cursor rules |
| `.cursorrules` | `.cursorrules` | Cursor legacy (unchanged) |

### Directory Structure [NEW in v2.5]

```
project/
├── .flowstate/                    # FlowState home directory (NEW in v2.5)
│   ├── config.md                  # Project configuration (was FLOWSTATE.md)
│   ├── tasks.md                   # Task board (was TASKS.md)
│   ├── session.md                 # Session state (was SESSION.md)
│   ├── archive/
│   │   └── tasks-archive.md       # Completed tasks archive (NEW)
│   ├── plans/
│   │   └── PLAN-001-feature.md    # Feature plans
│   ├── logs/
│   │   └── feature_2025-11-24.log # Evidence logs
│   └── version.txt                # Framework version (contains "2.5.0")
├── docs/
│   └── project-master-plan.md     # Phase definitions (user-facing, stays in docs/)
├── CLAUDE.md                      # Claude Code adapter (required at root)
├── AGENTS.md                      # Copilot/Codex adapter (required at root)
└── .cursor/
    └── rules/
        └── flowstate.mdc          # Cursor adapter (required location)
```

**Why .flowstate/ Directory?**
1. **Clean project root**: Only adapter files at root (required by platforms)
2. **No conflicts**: User's README.md, etc. never touched
3. **Better organization**: All FlowState state in one place
4. **Easier privacy**: Single directory to gitignore
5. **Consistent**: Same structure across all projects

**Platform Adapter Constraints**:
These files MUST stay at specific locations (platform requirements):
- `CLAUDE.md` — Project root (Claude Code requirement)
- `AGENTS.md` — Project root (Copilot/Codex requirement)
- `.cursor/rules/*.mdc` — .cursor/rules/ directory (Cursor requirement)

Adapters reference `.flowstate/` for actual state files.

### When to Use Each Mode

**Standard Mode (Recommended)**:
- **Use when**: You want clear, self-documenting filenames
- **Pros**: Easy to understand, explicit purpose, great for solo devs
- **Cons**: Visible in file lists (teammates might see them)
- **Privacy**: Configure `.git/info/exclude` for private ignore

**Obfuscated Mode**:
- **Use when**: You want extra stealth in shared repositories
- **Pros**: Looks like standard dotfiles, less conspicuous
- **Cons**: Less descriptive, requires remembering mappings
- **Privacy**: Requires `.git/info/exclude` (works with Private Ignore mode)

### Git Privacy Integration

During initialization (Step 2.5), AI will:
1. Detect if `.git/` exists
2. Offer privacy mode selection:
   - `[1] Private Ignore` (teammates can't see) - **Recommended**
   - `[2] Team Ignore` (visible in `.gitignore`)
   - `[3] Manual` (you handle it)
   - `[4] Skip`
3. If `[1]` selected, offer filename obfuscation: `[y/N]`
4. Configure `.git/info/exclude` automatically
5. Create files with chosen filename mode

**Result**: FlowState files invisible in `git status`, no `.gitignore` changes

---

## .git/info/exclude Template

**Filename**: `.git/info/exclude` (Git-controlled, not FlowState-controlled)

**Purpose**: Private git ignore patterns (teammates cannot see)

```gitignore
# FlowState AI Framework SE v2.5 - Private Ignore
# Added: [YYYY-MM-DD HH:MM]
# Mode: [Standard / Obfuscated]

# Core files (standard mode)
FLOWSTATE.md
TASKS.md
SESSION.md
docs/*-master-plan.md
plans/PLAN-*.md
logs/*.log

# Core files (obfuscated mode)
.project-config.md
.tasks.md
.session-state.md
docs/.master-plan.md
plans/.plan-*.md
logs/.log-*.txt

# Platform adapters (standard)
CLAUDE.md
AGENTS.md
.cursor/rules/flowstate.mdc
.cursorrules

# Platform adapters (obfuscated)
.ai-adapter.md
.cursor/rules/project.mdc

# Framework folder (if used)
.flowstate/

# Upgrade state (per-project, private)
UPGRADE-STATE.md

# FlowState framework docs and release/upgrade bundles
flowstate-ai-*
flowstate-*-release/
flowstate-*-upgrade/

# Note: Both standard and obfuscated patterns included for forward compatibility
# Only files matching your chosen mode will be created
```

**Usage Notes**:
- AI automatically populates this during initialization (if Private Ignore mode selected)
- Includes both standard and obfuscated patterns (future-proofing)
- Only files matching chosen mode are actually created
- `.git/info/exclude` is local-only (not committed to repository)
- Teammates cannot see these patterns or the FlowState files

---

## Platform Adapter Behavior (CLAUDE.md, AGENTS.md, Cursor) [NEW in v2.5]

These rules apply to any platform adapter FlowState creates (for Claude Code, GitHub Copilot/Codex, Cursor, etc.).

**State Loading (Always Required)**:
- Before performing non-trivial work (editing files, running commands, generating code), the AI MUST:
  - Read `FLOWSTATE.md` (or `.project-config.md`) and respect:
    - `Scaffolding Level` (controls explanation/teaching depth)
    - `Quality Mode` (Fast/Balanced/Methodical work rigor)
  - Read `TASKS.md` (or `.tasks.md`) to understand current priorities and ACTIVE STATE
  - Read `SESSION.md` (or `.session-state.md`) to restore session context

**Execution Loop Contract (Meta-Rule 14)**:
- After any response where work is performed, the AI MUST end with the 5-part Execution Loop:
  1. **COMPLETED** — What just finished (1–2 sentences)
  2. **ACTIVE STATE** — 3–7 tasks with status/progress, clearly marking “YOU ARE HERE”
  3. **NEXT RECOMMENDED** — 1–3 prioritized next actions with rationale
  4. **PROCEED WITH** — copy-paste commands (`proceed`, `proceed next`, `proceed all`, `ultrathink`, `pause`)
  5. **NOTES** — optional warnings, blockers, phase/progress updates

**Proceed Commands (Control Surface)**:
- Adapters MUST treat these commands as FlowState control primitives, not generic chat:
  - `proceed` → Execute current task only, then show Execution Loop
  - `proceed next` → Execute current + next task, then show Execution Loop
  - `proceed all` → Execute all P0 tasks with check-ins (Execution Loop) every 3 tasks
  - `ultrathink [optional task]` → Temporarily force Methodical quality mode for that task
  - `pause` → Finish current operation, then stop and wait
- `proceed all` MUST always be bounded:
  - Stop and show Execution Loop after every 3 tasks
  - Stop immediately if a P0 blocker, scope creep, or context-limit issue is detected

These behaviors SHOULD be mentioned or referenced in any adapter templates (CLAUDE.md, AGENTS.md, `.cursor/rules/flowstate.mdc`, `.ai-adapter.md`, etc.) so platform-specific AIs consistently honor FlowState’s core contracts.

---

## Universal FlowState Files

### FLOWSTATE.md Template

**Filename**: `FLOWSTATE.md` (standard) OR `.project-config.md` (obfuscated)

```markdown
# [Project Name] - FlowState Configuration

**Version**: 2.5.0 (Software Engineering Edition)
**Last Updated**: [YYYY-MM-DD HH:MM]
**Current Phase**: Phase 0 – Foundation

---

## 🎯 Phase 0 Mission

**Primary Goals**:
- [Goal 1 from user's Phase 0 success metric]
- [Goal 2]
- [Goal 3]
- Keep everything else explicitly out of scope until Phase 0 complete

**Acceptance Criteria** (see `docs/[project]-master-plan.md` OR `docs/.master-plan.md`):
- [ ] [Criterion 1]
- [ ] [Criterion 2]
- [ ] [Criterion 3]
- [ ] [Criterion 4]

**Target Completion**: [YYYY-MM-DD] ([X] weeks from now)

---

## Custom Templates (User-Owned)

Use this section for any templates you create or modify that are not part of the standard FlowState SE framework.

- Framework upgrades will treat everything under this heading as **user-owned**.
- During upgrades, the AI may replace the main `TEMPLATES.md` content, but it will preserve and, if needed, re-append this section verbatim.
- Do not move standard framework templates into this section; keep it for your own additions.

```markdown
## [Your Custom Template Name]

[Your custom template content goes here...]
```

---

## 🏗️ Technology Stack

### Backend
- **Runtime**: [Node.js v20+ / Python 3.11+ / Go 1.21+]
- **Framework**: [Express/Fastify / FastAPI/Django / Gin]
- **Database**: [PostgreSQL 15+ with Prisma/SQLAlchemy/GORM]
- **Auth**: [Clerk / Auth0 / custom JWT]
- **Caching**: [Redis / Upstash / none yet]

**Rationale**: [Why these choices? From initialization questions]

### Frontend
- **Framework**: [React 18+ / Vue 3+ / Svelte 5+] with TypeScript
- **Build Tool**: [Vite / Next.js / Nuxt]
- **UI Library**: [Shadcn UI + Tailwind / Material UI / Chakra]
- **State**: [Zustand / Context API / Pinia / Svelte stores]

**Rationale**: [Why these choices?]

### Infrastructure
- **Hosting**: [Vercel / AWS / GCP / Railway]
- **CI/CD**: [GitHub Actions / GitLab CI / CircleCI]
- **Monitoring**: [Sentry / DataDog / New Relic / none yet]

**Rationale**: [Why these choices?]

---

## 🔒 Privacy Configuration [NEW in v2.2]

**Privacy Mode**: [Private / Team / Manual / Skip]  
**Filename Mode**: [Standard / Obfuscated]  
**Git Integration**: [.git/info/exclude / .gitignore / Manual]

**About Privacy Controls**:
- **Private**: FlowState files ignored via `.git/info/exclude` (invisible to teammates)
- **Team**: FlowState patterns added to `.gitignore` (shared configuration)
- **Manual**: No automatic git config; you manage ignores yourself
- **Skip**: No git config; FlowState files may appear in `git status`

**Change Process**:
- If you change privacy settings later, update git configuration
  and reflect the new values here so AI can respect your preferences.

---

## 🎓 Scaffolding Configuration [NEW in v2.3]

**Scaffolding Level**: [Learner / Growth / Balanced / Expert]
**Changed**: [YYYY-MM-DD]
**Teaching Focus**: [SE-specific focus based on level]

**About Scaffolding Levels**:
- **Purpose**: Adjusts AI response verbosity to match your learning preferences
- **Change anytime**: Say "Change scaffolding to [Learner/Growth/Balanced/Expert]"
- **Key principle**: Same work quality, different explanation depth

**Level Descriptions**:
- **Learner**: Maximum teaching (explain every orchestration decision) — Best for first time using AI assistants
- **Growth**: Moderate teaching (explain key decisions) [DEFAULT] — Best for leveling up AI collaboration
- **Balanced**: Minimal teaching (explanations when needed) — Best for experienced AI orchestrators
- **Expert**: No teaching (maximum speed) — Best for power users who know FlowState deeply

**What Scaffolding Teaches** (Vibe Coding):
- ✅ Task decomposition (how to break down problems)
- ✅ Strategic sequencing (what to do first, why)
- ✅ Meta-rule application (when to follow which rule)
- ✅ Architectural thinking (system design, not just code)

**What Scaffolding Does NOT Teach** (Implementation):
- ❌ Coding syntax or language features
- ❌ Tool selection (which library to use)
- ❌ Algorithm implementations
- ❌ Performance optimization techniques

**SE Edition Teaching Focus** (when in Learner/Growth mode):
- API design orchestration (RESTful principles, versioning)
- Architecture patterns (MVC, microservices, when to use each)
- Refactoring strategies (when to refactor, how to sequence)
- Testing strategies (unit vs integration vs e2e)
- Deployment orchestration (CI/CD sequencing)

**See**: `REFERENCE.md` § Appendix F for complete scaffolding guide

---

## 🎯 Quality Mode Configuration [NEW in v2.4]

**Quality Mode**: [Fast / Balanced / Methodical]
**Changed**: [YYYY-MM-DD]
**Independent from**: Scaffolding Level (controls work rigor, not explanation verbosity)

**About Quality Modes**:
- **Purpose**: Adjusts rigor of work performed (documentation, validation, review depth)
- **Change anytime**: Say "Change quality mode to [Fast/Balanced/Methodical]"
- **Key principle**: Independent from scaffolding (you can have any combination)

**Mode Descriptions**:
- **Fast**: Minimal ceremony, essential work only — Best for prototyping, quick iterations
- **Balanced**: Standard rigor, selective validation [DEFAULT] — Best for normal development
- **Methodical**: Maximum thoroughness, comprehensive checks — Best for production-critical work, complex systems

**What Quality Mode Controls**:
- ✅ Documentation updates (skip vs selective vs comprehensive)
- ✅ Validation depth (minimal vs standard vs exhaustive)
- ✅ Review checkpoints (none vs occasional vs frequent)
- ✅ Git tagging frequency (milestones only vs every 3 tasks vs every task)
- ✅ Evidence trail detail (minimal vs moderate vs comprehensive)

**What Quality Mode Does NOT Control**:
- ❌ Explanation verbosity (controlled by Scaffolding Level)
- ❌ Teaching depth (controlled by Scaffolding Level)
- ❌ Code quality fundamentals (tests, types, DRY — always enforced)
- ❌ Meta-rules enforcement (always active)

**Mode Behaviors**:

**Fast Mode**:
- Documentation: Update only TASKS.md, SESSION.md (skip DECISIONS.md, PLAN-*.md unless user requests)
- Validation: Run tests, basic checks
- Git tags: Milestone only (phase gates, major features)
- Evidence: Minimal logging (essential findings only)
- Review: No check-ins (proceed to completion)

**Balanced Mode** (DEFAULT):
- Documentation: Update TASKS.md, SESSION.md, DECISIONS.md for major decisions
- Validation: Run tests, type checking, basic edge cases
- Git tags: Every 3 tasks or significant feature
- Evidence: Moderate logging (key findings, edge cases)
- Review: Occasional check-ins (after complex tasks)

**Methodical Mode**:
- Documentation: Update all files (TASKS.md, SESSION.md, DECISIONS.md, relevant PLAN-*.md)
- Validation: Comprehensive testing (unit, integration, edge cases, error scenarios)
- Git tags: Every completed task
- Evidence: Detailed logging (all findings, rationale, alternatives considered)
- Review: Frequent check-ins (every 1-2 tasks)

**SE Edition Quality Focus**:
- Fast: Ship features quickly, iterate based on feedback
- Balanced: Balance speed with maintainability
- Methodical: Production-ready quality, comprehensive testing, architectural documentation

**Quality × Scaffolding Matrix** (9 valid combinations):

| Combination | Behavior |
|-------------|----------|
| **Learner + Fast** | Minimal rigor work, maximum teaching (3x verbosity) |
| **Learner + Balanced** | Standard rigor work, maximum teaching (3x verbosity) |
| **Learner + Methodical** | Maximum rigor work, maximum teaching (3x verbosity) |
| **Growth + Fast** | Minimal rigor work, moderate teaching (2x verbosity) |
| **Growth + Balanced** | Standard rigor work, moderate teaching (2x verbosity) |
| **Growth + Methodical** | Maximum rigor work, moderate teaching (2x verbosity) |
| **Balanced + Fast** | Minimal rigor work, minimal teaching (1x verbosity) |
| **Balanced + Balanced** | Standard rigor work, minimal teaching (1x verbosity) |
| **Balanced + Methodical** | Maximum rigor work, minimal teaching (1x verbosity) |
| **Expert + Fast** | Minimal rigor work, no teaching (0.5x verbosity) |
| **Expert + Balanced** | Standard rigor work, no teaching (0.5x verbosity) |
| **Expert + Methodical** | Maximum rigor work, no teaching (0.5x verbosity) |

**See**: `REFERENCE.md` § Quality Mode Deep Dive for complete guide

---

## 📚 Concept Learning Configuration [NEW in v2.5]

**Concept Level**: [Novice / Apprentice / Practitioner / Fluent]
**Changed**: [YYYY-MM-DD]
**Independent from**: Scaffolding Level (which controls AI orchestration teaching)

**About Concept Levels**:
- **Purpose**: Adjusts how much AI explains language/framework/library concepts
- **Change anytime**: Say "Change concept level to [Novice/Apprentice/Practitioner/Fluent]"
- **Key principle**: Builds domain fluency over time without overwhelming

**Level Descriptions**:
- **Novice**: Maximum concept teaching, explain everything, use analogies
- **Apprentice**: Moderate teaching, introduce concepts gradually [DEFAULT]
- **Practitioner**: Minimal teaching, explain only advanced concepts
- **Fluent**: No concept teaching, use full technical vocabulary

**What Concept Levels Teach** (Domain Knowledge):
- ✅ Language syntax and idioms (e.g., "Dart uses `final` for immutable variables")
- ✅ Framework patterns (e.g., "Flutter widgets rebuild when state changes")
- ✅ Library APIs (e.g., "Riverpod's `ref.watch()` subscribes to provider changes")
- ✅ Technical vocabulary (e.g., "BuildContext provides access to the widget tree")

**What Concept Levels Do NOT Teach** (Handled by Scaffolding):
- ❌ Task decomposition and planning
- ❌ AI orchestration strategies
- ❌ Meta-rule application
- ❌ Architectural decision-making process

**See**: `flowstate-ai-se-framework-v2.5.0.md` § CONCEPT TEACHING PROTOCOL for complete guide

---

## 📖 Tech Stack Learning Profile [NEW in v2.5]

**Purpose**: Tracks which concepts you've learned for each technology in your stack

### [Technology 1 - e.g., Flutter/Dart]
**Concept Level**: Apprentice
**Concepts Learned**: 0
**Priority Concepts**: [Auto-detected based on project usage]
**Learned Concepts Log**:
- (None yet - concepts will be logged as you learn them)

### [Technology 2 - e.g., State Management Library]
**Concept Level**: Novice
**Concepts Learned**: 0
**Priority Concepts**: [Auto-detected]
**Learned Concepts Log**:
- (None yet)

**Note**: AI will introduce ~1 concept per session at natural teaching moments.
Concepts are tracked per-technology so you can be Fluent in one area and Novice in another.

---

## 📋 The 14 Meta-Rules (Configured) [Updated in v2.5]

### Meta-Rule 1: Phase Boundaries
**No Phase 1 work until Phase 0 acceptance criteria met**

Current phase: Phase 0
Deferred to Phase 1: [List of deferred features]

---

### Meta-Rule 2: Work → Right → Fast
**Progressive refinement stages**

- **Work** (make it function): Tests pass, acceptance criteria met
- **Right** (make it clean): Types, DRY, refactoring
- **Fast** (make it performant): Caching, optimization, bundle size

---

### Meta-Rule 3: One Task In-Progress
**Max 1 task per owner**

Current owner: [Dev name or "Solo developer"]
Strict enforcement: Yes

---

### Meta-Rule 4: Keep It Simple
**Delete before abstracting**

Before adding abstraction: Ask "Can I delete duplicate code instead?"

---

### Meta-Rule 5: Ask "Why This Approach?"
**Document rationale for every task**

Required in: `TASKS.md` OR `.tasks.md` (every task), `plans/` (complex tasks)

---

### Meta-Rule 6: Leave Breadcrumbs
**Evidence trails required**

Evidence location: `logs/`
Format: `logs/[feature]_YYYY-MM-DD_HHMM.log` OR `logs/.log-[feature]_YYYY-MM-DD_HHMM.txt`

---

### Meta-Rule 7: Stage Work Visibly
**Label commits with stage**

Format: `[type]([scope]): [description] [Stage]`
Example: `feat(auth): Implement Clerk integration [Work]`

---

### Meta-Rule 8: Small & Focused Files
**Language-adapted size caps**

**Detected Language**: [TypeScript/JavaScript / Python / Swift / Go / etc.]
**File Size Cap**: ≤[400/300/600] LOC (hard limit)
**Proactive Warning Trigger**: [350/270/540] LOC (90% of cap)

**Verification Command**:
```bash
[Language-specific command to find files >cap]
```

**Notes**:
- Config files: Exempt (package.json, tsconfig.json, etc.)
- Generated code: Exempt ([list if applicable])

---

### Meta-Rule 9: Commit Discipline
**Tag rollback points**

Before risky work:
```bash
git tag [feature]-before -m "Safe rollback point"
```

After validation:
```bash
git tag [feature]-after -m "Validated: [outcome]"
```

---

### Meta-Rule 10: Refactor Discipline
**Proactive debt management**

**Triggers**:
- Every 5 completed tasks
- Any file >90% of size cap ([350/270/540] LOC)
- Duplicate code across 3+ files

**Process**: Scan → Propose → Approve → Execute → Evidence

---

### Meta-Rule 11: Subscription Context
**Feature gating by tier**

**Subscription Model**: [Yes/No]

[If Yes:]
**Tiers**:
- **Free**: [Features]
- **Pro**: [Features] ($[X]/mo)
- **Team**: [Features] ($[Y]/mo)
- **Enterprise**: [Features] (custom pricing)

**Implementation Pattern**:
- Backend: Entitlement middleware + 402 responses
- Frontend: Upgrade prompts for gated features

[If No:]
This Meta-Rule is not active for this project.

---

### Meta-Rule 12: Entitlement Testing
**Test enabled AND disabled states**

[If subscription model active:]
Every gated feature requires 2 test suites:
- Enabled state (Pro/Team user can access)
- Disabled state (Free user sees upgrade prompt + 402)

[If not active:]
This Meta-Rule is not active for this project.

---

### Meta-Rule 13: Comprehension Debt
**Optimize for human understanding first**

**Target**: <15 minutes to understand any module
**Triggers**: Phase transitions, files >90% cap, test confusion, onboarding friction

---

### Meta-Rule 14: Execution Loop Contract [NEW in v2.4]
**Every work response ends with 5-part Execution Loop**

**Structure**:
1. **COMPLETED** (1-2 sentences)
2. **ACTIVE STATE** (3-7 visual task list with progress)
3. **NEXT RECOMMENDED** (1-3 prioritized actions)
4. **PROCEED WITH** (copy-paste commands: proceed/proceed next/proceed all/ultrathink/pause)
5. **NOTES** (optional: warnings, blockers, phase progress)

**Purpose**: Solves "AI stopped without guidance" UX problem

**See**: Framework § Meta-Rule 14 for complete specification

---

## 🔧 Tooling & Commands

### Development
```bash
# Install dependencies
[auto-detected: pnpm install / pip install -r requirements.txt / etc.]

# Start dev server
[auto-detected: pnpm dev / python manage.py runserver / etc.]

# Run tests
[auto-detected: pnpm test / pytest / etc.]

# Build for production
[auto-detected: pnpm build / python setup.py build / etc.]

# Lint
[auto-detected: pnpm lint / flake8 / etc.]
```

### Validation
```bash
# Check file sizes (Meta-Rule 8)
[language-specific command]

# List rollback tags (Meta-Rule 9)
git tag --list '*-before'
git tag --list '*-after'

# Run full validation
[project-specific validation command]
```

### Evidence Capture
```bash
# Run tests and save output
[test command] | tee logs/[feature]_$(date +%Y-%m-%d_%H%M).log
# OR (obfuscated mode)
[test command] | tee logs/.log-[feature]_$(date +%Y-%m-%d_%H%M).txt
```

---

## 🚫 Deferred Until Phase 1+

**Phase 1 (Scale & Expand)**:
- [Feature 1 deferred from Phase 0]
- [Feature 2]
- [Feature 3]

**Phase 2 (Enterprise & Polish)**:
- [Feature 1]
- [Feature 2]

**Not Planned** (explicitly out of scope):
- [Feature that will never be built]

---

## 📝 Code Organization Standards

- **File Size**: ≤[cap] lines (enforced by Meta-Rule 8)
- **Single Responsibility**: Each file has one clear purpose
- **Refactoring Triggers**: Files >[90% of cap] LOC, duplicate code 3+ times
- **Documentation**: Inline comments for "why", not "what"

---

## 🔄 Quality Gates

### Before Marking Task "Done"
- [ ] Tests passing
- [ ] Evidence log created in `logs/`
- [ ] Git tags created ([feature]-before, [feature]-after)
- [ ] `TASKS.md` OR `.tasks.md` updated
- [ ] File size caps respected

### Before Phase Transition
- [ ] ALL acceptance criteria met
- [ ] No P0 bugs (bug hunt complete)
- [ ] All files under size cap
- [ ] Test coverage ≥[80]%
- [ ] Documentation complete (README, `SESSION.md` OR `.session-state.md` updated with handoff notes)

---

## 📚 Project-Specific Context

### Critical Paths
[List user-facing workflows that must always work]

### Known Constraints
[List any project-specific constraints or limitations]

### Team Conventions
[List any team-specific coding standards or practices]

---

**Stay focused on Phase 0 acceptance criteria**: [Restate top 3 goals]

**Last Updated**: [Auto-updated by AI during sessions]
```

---

### TASKS.md Template [UPDATED in v2.5]

**Filename**: `.flowstate/tasks.md` (standard) OR `.flowstate/.tasks.md` (obfuscated)

```markdown
# FlowState Task Board

**Project**: [Project Name]
**Phase**: Phase 0 – Foundation (see `docs/[project]-master-plan.md` OR `docs/.master-plan.md`)
**Last Updated**: [YYYY-MM-DD HH:MM]

---

## 📋 Collaboration Guardrails

**Quick Meta-Rules Reference** (see `FLOWSTATE.md` OR `.project-config.md` for full details):
- **Meta-Rule 1**: Phase boundaries — No Phase 1 work until Phase 0 complete
- **Meta-Rule 2**: Work → Right → Fast — Function, quality, performance (in order)
- **Meta-Rule 3**: One task in-progress per owner
- **Meta-Rule 4**: Keep it simple — Delete before abstracting
- **Meta-Rule 5**: Ask "Why?" — Document rationale
- **Meta-Rule 6**: Leave breadcrumbs — Evidence trails required
- **Meta-Rule 7**: Stage work — Label [Work]/[Right]/[Fast]
- **Meta-Rule 8**: Small files — ≤[cap] LOC
- **Meta-Rule 9**: Commit discipline — Tag before/after
- **Meta-Rule 10**: Refactor every 5 tasks
- **Meta-Rule 11-12**: Subscription/entitlement (if applicable)
- **Meta-Rule 13**: Comprehension debt management
- **Meta-Rule 14**: Execution Loop Contract — Structured navigation [NEW v2.5]

---

## 📥 Backlog

- [ ] [Task Name] — Owner: [Name] — Stage: Work — Priority: P0
  DoD: [Measurable criteria for "done"]
  Why this approach? [One sentence rationale or link to plan]
  Quality Gate: [Specific validation criteria]
  Plan: `plans/PLAN-XXX*.md` OR `plans/.plan-XXX*.md` if applicable, or "No plan needed (simple task)"
  Evidence: `logs/[feature]_YYYY-MM-DD_HHMM.log` OR `logs/.log-[feature]_YYYY-MM-DD_HHMM.txt` (pending)
  Rollback: git tag [feature]-before (will create)
  Validation: [Command to verify functionality]
  Dependencies: [Blocks or blocked by other tasks, or "None"]
  Effort: [Hours estimate]

---

## 🏗️ In-Progress

> **Meta-Rule 3**: Max 1 task per owner

- [ ] [Task Name] — Owner: [Name] — Stage: Work — Started: [YYYY-MM-DD]
  Current Status: [X]% complete
  Notes: [Current blockers, progress updates]
  Why this approach? [Rationale]
  Plan: `plans/PLAN-XXX*.md` OR `plans/.plan-XXX*.md` if applicable
  Evidence: [Partial evidence if available]

---

## 🚧 Blocked

- [ ] [Task Name] — Owner: [Name] — Blocked Since: [YYYY-MM-DD]
  Blocker: [Description of blocker with severity P0/P1/P2]
  Impact: [What's blocked? Timeline impact?]
  Unblock Plan: [Steps to resolve + owner]
  Alternative: [Fallback task if blocker >24 hours]

---

## 🧪 Testing

- [x] [Task Name] — Owner: [Name] — Stage: Right — In Testing Since: [YYYY-MM-DD]
  DoD Status: [Check all criteria]
    - [ ] [Criterion 1]
    - [ ] [Criterion 2]
    - [ ] [Criterion 3]
  Quality Gate: Tests passing? ✅/❌
  Plan: `plans/PLAN-XXX*.md` OR `plans/.plan-XXX*.md` if applicable
  Evidence: `logs/[feature]_YYYY-MM-DD_HHMM.log` OR `logs/.log-[feature]_YYYY-MM-DD_HHMM.txt`
  Rollback: git tag [feature]-before

---

## ✅ Done

- [x] [Task Name] — Owner: [Name] — Stage: Work → Right — Completed: [YYYY-MM-DD]
  Evidence: `logs/[feature]_YYYY-MM-DD_HHMM.log` OR `logs/.log-[feature]_YYYY-MM-DD_HHMM.txt`
  Why this approach? [Rationale for future reviewers]
  Plan: `plans/PLAN-XXX*.md` OR `plans/.plan-XXX*.md` if applicable
  Rollback: git tag [feature]-before (validated: ✅)
  Outcome: [What was achieved in plain English]
  Metrics: [Test coverage, LOC changed, performance impact]

---

## 📊 Progress Tracking

**Phase 0 Progress**: [X]% complete ([N]/[M] tasks done)
**Refactor Counter**: [N]/5 tasks (trigger at 5)
**Quality Metrics**:
- Files under cap: ✅/⚠️ ([N] files, [X] approaching limit)
- Test coverage: [X]%
- Evidence coverage: [X]% of done tasks have logs

---

**Last Updated by**: [AI/Human Name]
**Next Review**: [YYYY-MM-DD]
```

---

### ARCHIVED-TASKS.md Template [NEW in v2.5]

**Filename**: `.flowstate/archive/tasks-archive.md` (standard) OR `.flowstate/archive/.tasks-archive.md` (obfuscated)

**Purpose**: Historical record of completed tasks for context and reference

```markdown
# FlowState Task Archive

**Project**: [Project Name]
**Archive Updated**: [YYYY-MM-DD HH:MM]

**📚 Purpose**: Historical record of completed tasks for context and reference
**🔍 Search**: Use `FlowState find task [query]` to search this archive

---

## Phase [N] – [Phase Name] (Archived: [YYYY-MM-DD])

### Completed Tasks ([N] tasks)

- [x] **[Task Name]** — Done: [YYYY-MM-DD]
  - Owner: [Name] | Stage: [Work → Right → Fast]
  - DoD: [Definition of Done that was met]
  - Evidence: `.flowstate/logs/[feature]_[date].log`
  - Why: [Rationale for the approach taken]
  - Rollback: `[tag]-before` → `[tag]-after`
  - Outcome: [What was achieved in plain English]
  - Metrics: [Test coverage delta, LOC changed, performance impact if any]

- [x] **[Task Name 2]** — Done: [YYYY-MM-DD]
  - Owner: [Name] | Stage: [Work]
  - DoD: [Definition of Done]
  - Evidence: `.flowstate/logs/[feature]_[date].log`
  - Why: [Rationale]
  - Outcome: [What was achieved]

[... more tasks ...]

---

## Phase [N-1] – [Phase Name] (Completed: [YYYY-MM-DD])

### Completed Tasks ([N] tasks)

[... tasks from earlier phase ...]

---

## 📊 Archive Statistics

- **Total archived tasks**: [N]
- **Phases archived**: [N]
- **Oldest task**: [YYYY-MM-DD]
- **Most recent**: [YYYY-MM-DD]
- **Archive created**: [YYYY-MM-DD]

---

**Archive maintained by FlowState AI**
```

**Archival Triggers**:
1. Done section exceeds 15 tasks
2. Phase transition occurs
3. User runs `FlowState archive tasks`

**Search Commands**:
- `FlowState find task [query]` — Search active and archived tasks
- `FS find [query]` — Alias
- `Where did we do [query]` — Natural language alias

---

### SESSION.md Template [UPDATED in v2.5]

**Filename**: `.flowstate/session.md` (standard) OR `.flowstate/.session.md` (obfuscated)

```markdown
# FlowState Session State

**Project**: [Auto-detected from package.json or git]
**Last Updated**: [YYYY-MM-DD HH:MM]
**Session Duration**: [hours]h [minutes]min
**FlowState Version**: 2.5.0

---

## 📈 Velocity & Progress [NEW in v2.5 - TOP OF DOC]

### This Week
- **Tasks completed**: [N]
- **Avg completion time**: [X.X] hours
- **Velocity**: [N] points ([up/down/same] from [N] last week)

### Phase [N] Projection
- **At current velocity**: Complete in [N] days
- **Target**: [N] days
- **Status**: ✅ On track / ⚠️ At risk / 🚨 Behind

### Bottlenecks Detected
- [None detected / Category tasks taking Xx longer than estimated]
- Consider: [Suggestion if bottleneck exists]

**Velocity Tracking**: Enabled by default. Disable with "Disable velocity tracking"

---

## 🔄 Quick Actions [NEW in v2.5]

| Action | Command |
|--------|---------|
| Generate handoff document | `FlowState handoff` |
| Sync after off-reservation work | `FlowState sync` |
| Search past tasks | `FlowState find task [query]` |
| View full task board | `show all` |

---

## 📊 Current State

**Phase**: Phase 0 – Foundation ([X]% complete)
**Active Sprint**: Week [N] of [M]
**Phase Target**: [YYYY-MM-DD] ([X] weeks remaining)

**Acceptance Criteria Progress** (from Master Plan):
- [x] [Criterion 1] ([Brief implementation note])
- [x] [Criterion 2] ([Brief implementation note])
- [ ] [Criterion 3] (in progress - [X]% done)
- [ ] [Criterion 4] (not started)
- [ ] [Criterion 5] (not started)

---

## 🏗️ Active Work

**In-Progress Tasks**: [N]
- **[Task Name]** (Owner: [Name], Stage: [Work/Right/Fast], [X]% complete)
  - DoD: [Brief definition of done]
  - Blocker: [None / Description]
  - Next: [Next concrete step to move forward]
  - Evidence: `logs/[file]_YYYY-MM-DD_HHMM.log` OR `logs/.log-[file]_YYYY-MM-DD_HHMM.txt` (pending)

**Backlog (Next 3 Priorities)**:
1. **[P0] [Task Name]** — [Why it's next / Why it's high priority]
2. **[P0/P1] [Task Name]** — [Dependency relationship or strategic importance]
3. **[P1] [Task Name]** — [Strategic importance]

**Blocked Tasks**: [N]
- **[Task Name]** — Blocker: [Description] — Unblock plan: [Steps + ETA]

---

## ✅ Recent Completions (Last 3)

1. **[Feature/Task Name]** (Completed: [YYYY-MM-DD])
   - Stage: [Work → Right / Work / Right → Fast]
   - Evidence: `logs/[feature]_YYYY-MM-DD_HHMM.log` OR `logs/.log-[feature]_YYYY-MM-DD_HHMM.txt`
   - Rollback: git tag [feature]-complete-YYYY-MM-DD
   - Outcome: [What was achieved in plain English]
   - Impact: [Test coverage change, performance improvement, etc.]

2. **[Feature/Task Name]** (Completed: [YYYY-MM-DD])
   - [Same structure as above]

3. **[Feature/Task Name]** (Completed: [YYYY-MM-DD])
   - [Same structure as above]

---

## 📋 Active Plans

1. **PLAN-XXX: [Feature Name]** (Phase [N])
   - Status: [Pending / In-Progress ([X]% done) / Complete]
   - Owner: [Name]
   - ETA: [YYYY-MM-DD] ([X] weeks remaining)
   - Progress: [Brief status update]
   - Related Task: `TASKS.md` OR `.tasks.md` line [N] or task title

---

## 🔑 Key Decisions & Context [ENHANCED in v2.5]

**Purpose**: Critical context that must survive session boundaries. Update this section
whenever you make or discover a decision that a future AI session would need to know.

### Architectural Decisions
| Decision | Rationale | Date |
|----------|-----------|------|
| [Choice 1] | [Why this over alternatives] | [YYYY-MM-DD] |
| [Choice 2] | [Why this over alternatives] | [YYYY-MM-DD] |

### Tech Stack Constraints
- **[Constraint 1]**: [Reason] (e.g., "Can't upgrade Flutter until package X supports it")
- **[Constraint 2]**: [Reason]

### Fragile Areas (Handle with Care)
- **[File/Module]**: [Why it's fragile] (e.g., "auth_provider.dart is complex—test carefully")
- **[File/Module]**: [Why it's fragile]

### User Preferences Discovered
- **[Preference]**: [Context] (e.g., "User prefers explicit error messages")

### Deferred to Future Phases
- **[Feature 1]** → Phase [N] — Reason: [Why deferred]
- **[Feature 2]** → Phase [N+1] — Reason: [Why deferred]

**Phase Scope Lock**:
Last modified: [YYYY-MM-DD]
No Phase [N+1] work until Phase [N] acceptance criteria met (Meta-Rule 1)

---

## 📏 Quality Metrics

**File Size Compliance** (Meta-Rule 8):
- Total files: [N]
- Files >[90% of cap] LOC: [N] files
  - [filename.ts]: [X] LOC (cap: [Y] LOC, warning at [Z] LOC)
  - [filename2.py]: [X] LOC (cap: [Y] LOC, warning at [Z] LOC)
- Files >[cap] LOC: [N] files ✅/❌ (MUST be 0)
- Action needed: [Description or "None"]

**Refactor Cycle Counter**: [N]/5 tasks (trigger at 5 per Meta-Rule 10)

**Evidence Trail Coverage**: [X]% ([N]/[M] completed tasks have logs)

**Test Coverage**: [X]% (target: [80]% before Phase [N+1])

**Git Safety Tags**: [N] rollback tags created (✅ All recent completions tagged / ⚠️ Missing tags)

---

## 📝 Stand-Up Summary

**For Daily Stand-Up on [YYYY-MM-DD]**:

### Yesterday ([YYYY-MM-DD]):
✅ **[Task 1]**
   - [Outcome in plain English]
   - Evidence: `logs/[file].log` OR `logs/.log-[file].txt`

✅ **[Task 2]**
   - [Outcome in plain English]
   - Evidence: `logs/[file].log` OR `logs/.log-[file].txt`

🏗️ **Started [Task 3]** ([X]% complete)
   - [Current status]
   - Next: [What's left to do]

### Today ([YYYY-MM-DD]):
- [Goal 1]
- [Goal 2]
- [Goal 3 if applicable]

### Blockers:
[None / Blocker description with severity P0/P1/P2]

### Notes:
- [On track / X days behind / X days ahead] for Phase [N] ([X] weeks remaining)
- Test coverage: [X]% (need [80]% by Phase [N+1])
- [N] files approaching split trigger ([list filenames])
- [Any other important context: velocity, risks, decisions needed]

---

## ⏱️ Session Metadata

**Last Session**:
- Start: [YYYY-MM-DD HH:MM]
- End: [YYYY-MM-DD HH:MM]
- Duration: [H]h [M]min
- Tasks completed: [N]
- Tasks started: [N]

**Cumulative Stats**:
- Total sessions: [N]
- Total hours: [X]h
- Tasks completed: [N]
- Velocity: [X.Y] tasks/day (target: [Z] tasks/day)
- Days to Phase [N] completion (at current velocity): [X] days

**Next Session Goal** (set for [YYYY-MM-DD]):
"[User's stated goal for next session]"

---

## 🔄 Rollback & Recovery

**Last Known Good State**:
- Commit: [SHA] ([YYYY-MM-DD HH:MM])
- Tag: [tag-name]
- Validation: `[command to verify]` (status: ✅ All green / ⚠️ Issues)

**Emergency Rollback Procedure**:
```bash
git reset --hard [tag-name]
[Any additional steps: pnpm install, db:migrate, etc.]
[Validation command]
```

**Backup State Files**:
- `FLOWSTATE.md` OR `.project-config.md` (backed up at session close)
- `TASKS.md` OR `.tasks.md` (backed up at session close)
- `SESSION.md` OR `.session-state.md` (this file - backed up at session close)
- Master Plan (version controlled)

---

## 🧠 AI Context Hints

**Coding Patterns to Maintain**:
- [Pattern 1: e.g., "Use Prisma for all DB access"]
- [Pattern 2: e.g., "Error handling with custom error classes"]
- [Pattern 3: e.g., "API responses always include request ID"]

**Current Focus**:
Working on Phase [N] acceptance criteria #[X]: "[Description]"
Specifically: [Current workflow or feature being implemented]

**Watch For**:
- [File 1]: [X] LOC (threshold: [Y] LOC, approaching split)
- [Metric 2]: [Current value] (threshold: [X], status: ✅/⚠️)
- Refactor cycle trigger: [N]/5 tasks

**Next Milestones**:
1. **[Milestone 1]** (ETA: [YYYY-MM-DD]) - [Brief description]
2. **[Milestone 2]** (ETA: [YYYY-MM-DD]) - [Brief description]
3. **[Milestone 3]** (ETA: [YYYY-MM-DD]) - [Brief description]

---

*This snapshot auto-generated by FlowState AI Framework at session close.*
*Resume with: "Resume FlowState. Read `SESSION.md` OR `.session-state.md`. Today's goal: [your goal]"*
```

---

### Master Plan Template

**Filename**: `docs/[project]-master-plan.md` (standard) OR `docs/.master-plan.md` (obfuscated)

```markdown
# [Project Name] Master Plan

**Owner**: Product Lead
**Last Updated**: [YYYY-MM-DD]
**Status**: Active
**FlowState Version**: 2.2

---

## 1. Vision & Success Metrics

**Mission**: [One sentence describing the core value proposition]

**Success Metrics**:
- [Metric 1]: [Target] (e.g., 1,000 active users by Q2 2026)
- [Metric 2]: [Target] (e.g., <200ms p95 API latency)
- [Metric 3]: [Target] (e.g., 80% feature adoption for core workflows)

---

## 2. Phase Breakdown

### Phase 0: Foundation (Weeks 1-8)

**Goal**: [From user's initialization: Phase 0 success metric]

**Scope**:
- [Feature 1]
- [Feature 2]
- [Feature 3]
- [Feature 4]

**Out of Scope** (Deferred to Phase 1):
- [Feature A]
- [Feature B]
- [Feature C]

**Acceptance Criteria**:
- [ ] [Criterion 1: Specific, measurable]
- [ ] [Criterion 2: Specific, measurable]
- [ ] [Criterion 3: Specific, measurable]
- [ ] [Criterion 4: Specific, measurable]
- [ ] Tests passing (≥80% coverage on critical paths)
- [ ] Deployment pipeline functional
- [ ] Documentation complete (README, `SESSION.md` OR `.session-state.md` updated with handoff notes)

**Duration**: 4-8 weeks
**Target Completion**: [YYYY-MM-DD]

---

### Phase 1: Scale & Expand (Weeks 9-20)

**Goal**: Add feature depth and handle production load

**Scope**:
- Advanced features ([list 3-5 key features from initialization])
- [Multi-provider support if applicable]
- Observability (logging, monitoring, tracing)
- [Subscription tiers if applicable: Free, Pro, Team]

**Out of Scope** (Deferred to Phase 2):
- [Feature 1]
- [Feature 2]
- [Feature 3]

**Acceptance Criteria**:
- [ ] Advanced features [gated by tier if applicable]
- [ ] Observability dashboard live
- [ ] Load testing validates 10x user growth
- [ ] Public launch documentation complete

**Duration**: 6-12 weeks
**Target Completion**: [YYYY-MM-DD]

---

### Phase 2: Enterprise & Polish (Weeks 21-36)

**Goal**: Enterprise readiness and UX refinement

**Scope**:
- SSO integration (SAML, OAuth)
- Admin controls and audit logs
- Compliance (SOC 2, GDPR if applicable)
- Performance tuning

**Acceptance Criteria**:
- [ ] [SOC 2 compliance in progress if applicable]
- [ ] Enterprise features validated with design partners
- [ ] Performance benchmarks met (p95 latency <[X]ms)

**Duration**: 8-16 weeks
**Target Completion**: [YYYY-MM-DD]

---

## 3. Technology Stack

### Backend
- **Runtime**: [Auto-detected]
- **Framework**: [Auto-detected]
- **Database**: [Auto-detected]
- **Auth**: [Auto-detected or planned]
- **Caching**: [Auto-detected or planned]

**Rationale**: [Why these choices from initialization]

### Frontend
- **Framework**: [Auto-detected] with TypeScript
- **Build Tool**: [Auto-detected]
- **UI Library**: [Auto-detected]
- **State**: [Auto-detected]

**Rationale**: [Why these choices]

### Infrastructure
- **Hosting**: [From initialization: Vercel / AWS / etc.]
- **CI/CD**: [Auto-detected or planned]
- **Monitoring**: [Planned]

**Rationale**: [Why these choices]

---

## 4. Out of Scope (Explicit Deferrals)

- White-label capabilities → Phase 3+
- Mobile apps → Post-PMF
- Custom integrations → Enterprise tier only
- [Add project-specific deferrals from initialization]

---

## 5. Risk Assessment

| Risk | Severity | Mitigation |
|------|----------|------------|
| Third-party API changes | High | Version pinning + adapter pattern |
| Scope creep | Medium | Phase gates + explicit deferrals (Meta-Rule 1) |
| Technical debt | Medium | Meta-Rule 10 refactor cycles + comprehension debt audits |
| [Project-specific risk from context] | [H/M/L] | [Mitigation strategy] |

---

## 6. Subscription Architecture (If Applicable)

[If subscription model selected:]

### Tier Structure
| Tier | Price | Key Features | Target Audience |
|------|-------|--------------|-----------------|
| **Free** | $0 | [Features from initialization] | Hobbyists, trial users |
| **Pro** | $[X]/mo | [Features from initialization] | Power users, professionals |
| **Team** | $[Y]/mo | [Features from initialization] | Small teams (2-10) |
| **Enterprise** | Custom | [Features from initialization] | Large organizations |

[If no subscription model:]
This project uses a single-tier model (no feature gating).

---

## 7. Next Review

**Scheduled**: [YYYY-MM-DD] (Phase 0 completion or +3 months)
**Trigger**: Phase 0 completion or strategic pivot
```

---

## Platform Adapter Files

### CLAUDE.md Template (Claude Code)

**Filename**: `CLAUDE.md` (standard) OR `.ai-adapter.md` (obfuscated)

```markdown
# FlowState AI Framework - Claude Code Instructions

**Version**: 2.5.0 (Software Engineering Edition)
**Project**: [Auto-detected]
**Last Updated**: [Auto-generated timestamp]

---

## 🎯 You Are Operating Under FlowState

This project uses the **FlowState AI Framework** for Software Engineering.

Your role: Autonomous execution of software engineering tasks while maintaining quality, documentation, and phase discipline.

---

## 📚 Framework Files (Your Memory)

### Core References (Read Every Session)
- **`FLOWSTATE.md` OR `.project-config.md`** - All Meta-Rules, current phase, project rules
- **`TASKS.md` OR `.tasks.md`** - Task board with current priorities
- **`SESSION.md` OR `.session-state.md`** - Session state and context restoration

### Supporting Files
- **`docs/[project]-master-plan.md` OR `docs/.master-plan.md`** - Phase definitions and acceptance criteria
- **`plans/PLAN-*.md` OR `plans/.plan-*.md`** - Detailed requirements for complex features
- **`logs/*.log` OR `logs/.log-*.txt`** - Evidence trails from completed work

---

## 🔄 Session Management Protocol

### Recognizing "FlowState SE" Command

When user says **"FlowState SE"**, check if `FLOWSTATE.md` OR `.project-config.md` exists:

**If FLOWSTATE.md OR .project-config.md does NOT exist:**
→ This is initialization. Execute the AI Initialization Protocol from flowstate-ai-se-framework-v2.5.0.md § AI INITIALIZATION PROTOCOL

**If FLOWSTATE.md OR .project-config.md exists:**
→ This is session resume. Execute the session resume protocol below.

---

### Session Resume (When FLOWSTATE.md OR .project-config.md exists)
```
User says: "FlowState SE" or "Resume FlowState"

You should:
1. Read SESSION.md OR .session-state.md (context restoration)
2. Read TASKS.md OR .tasks.md (current priorities)
3. Read FLOWSTATE.md OR .project-config.md (verify phase, rules)
4. Report readiness:
   - Current phase and completion %
   - Active work status
   - Next 3 priorities
   - Ask: "What would you like to work on?"
```

### During Work
- Use **TodoWrite** tool to track progress
- Update `TASKS.md` OR `.tasks.md` as tasks move through stages
- Create plan documents (`plans/PLAN-*.md` OR `plans/.plan-*.md`) for complex tasks
- Capture evidence in `logs/` directory
- Tag git state before/after risky changes

### Session Close
```
User says: "Close session" or "Done for today"

You should:
1. Update SESSION.md OR .session-state.md:
   - Current timestamp
   - Active work status and % complete
   - Completed tasks with evidence links
   - Quality metrics (file sizes, refactor counter)
   - Generate standup summary
2. Update TASKS.md OR .tasks.md (move completed to Done)
3. Create evidence logs (if work completed)
4. Git commit: "FlowState: Update session state"
5. Git tag (if milestone): [feature]-session-end-YYYY-MM-DD
6. Report session summary to user
```

---

## 📋 The 13 Meta-Rules

**Read `FLOWSTATE.md` OR `.project-config.md` for full details.**

1. **Phase Boundaries** - No Phase N+1 work until Phase N complete
2. **Work → Right → Fast** - Make it work, make it right, make it fast
3. **One Task In-Progress** - Max 1 task at a time (use TodoWrite)
4. **Keep It Simple** - Delete before abstracting
5. **Ask Why** - Document rationale for every task
6. **Leave Breadcrumbs** - Evidence trails required (logs, git tags)
7. **Stage Work Visibly** - Tag commits with [Work]/[Right]/[Fast]
8. **Small & Focused Files** - Language-adapted size caps
9. **Commit Discipline** - Tag before/after risky changes
10. **Refactor Discipline** - Every 5 tasks, scan for debt
11. **Subscription Context** - Note tier gating in DoD
12. **Entitlement Testing** - Test enabled AND disabled states
13. **Comprehension Debt** - Optimize for human understanding

---

## 🏗️ Technology Stack

**Backend**: [Auto-detected]
**Frontend**: [Auto-detected]
**Database**: [Auto-detected]
**File Size Cap**: [Auto-adapted to language]

### Development Commands
```bash
# Install
[auto-detected]

# Dev Server
[auto-detected]

# Tests
[auto-detected]

# Build
[auto-detected]
```

---

## 🎨 Coding Standards

**Language**: [Primary language]
**File Size Cap**: ≤[X] LOC (hard limit)
**Proactive Warning**: [90% of cap] LOC

**Verification**:
```bash
[Language-specific verification command]
```

**Style Guidelines**:
[Project-specific from FLOWSTATE.md OR .project-config.md]

---

## 📝 Plan Document System

**When to Create a Plan:**
If you need to ask ≥2 clarifying questions → Create a plan

**Process**:
1. Recognize complexity during task creation
2. Ask strategic questions (2-5 questions)
3. Use Write tool to create `plans/PLAN-XXX-[feature-slug].md` OR `plans/.plan-XXX-[feature-slug].md`
4. Capture ALL context:
   - Requirements (functional & non-functional)
   - Architecture decisions with rationale
   - Constraints and assumptions
   - Acceptance criteria (DoD)
   - Risks and mitigations
   - Implementation phases
5. Cross-reference in `TASKS.md` OR `.tasks.md` and `SESSION.md` OR `.session-state.md`
6. When implementing: Read plan first, full context restored

**Plan Template**: See TEMPLATES.md § Plan Documents

---

## ⚙️ Tool Usage Guidelines

### File Operations
- **Read**: Check file before editing (required)
- **Edit**: Use for modifying existing files
- **Write**: Use for new files only (prefer Edit for existing)
- **Glob**: Find files by pattern
- **Grep**: Search code content

### Task Management
- **TodoWrite**: Track current work (use frequently)
- Sync TodoWrite with `TASKS.md` OR `.tasks.md` at session boundaries

### Git Operations
- **Bash**: For git commands (commits, tags, status)
- Always tag before risky changes: `git tag [feature]-before`
- Tag after validation: `git tag [feature]-after`

### Evidence Capture
- **Bash**: Run tests, capture output to `logs/`
- Format: `logs/[feature]_YYYY-MM-DD_HHMM.log` OR `logs/.log-[feature]_YYYY-MM-DD_HHMM.txt`
- Link in `TASKS.md` OR `.tasks.md` when moving to Done

---

## 🚨 Critical Constraints

### Phase Boundary Enforcement
```
If user requests Phase N+1 work while in Phase N:
  "This is Phase [N+1] work (current: Phase [N]).
   Defer to Phase [N+1] or descope Phase [N]?"
```

### File Size Enforcement
```
When file reaches 90% of cap:
  "Notice: [file].ts is [X] LOC (approaching [cap] trigger).
   Suggest refactor: [split plan]
   Refactor now or defer to next cycle?"
```

### Evidence Requirements
```
When moving task to Done in TASKS.md OR .tasks.md:
  - Evidence log must exist in logs/
  - Git tags must exist ([feature]-before, [feature]-after)
  - Tests must pass (capture output)
  If missing: Complete before marking Done
```

---

## 🔄 Refactor Cycle Protocol

**Triggers**:
- Every 5 completed tasks
- Any file >90% of size cap
- Duplicate code across 3+ files

**Process**:
1. Scan codebase for violations
2. Create refactor proposal (ranked by impact/effort)
3. Wait for user approval
4. Execute refactors with evidence logs
5. Reset task counter in `SESSION.md` OR `.session-state.md`

---

## 🐛 Bug Hunt Protocol

**Triggers**:
- Weekly (Friday)
- Before phase transitions
- After major features

**Categories**:
1. Logic & Edge Cases
2. Integration Issues
3. Security & Validation
4. Performance & Resources

**Output**:
- `logs/bug_hunt_YYYY-MM-DD_HHMM.log` OR `logs/.log-bug_hunt_YYYY-MM-DD_HHMM.txt`
- Tasks created in `TASKS.md` OR `.tasks.md` for P0/P1 bugs
- P0 bugs block phase advancement

---

## 🎯 Success Metrics

**Quality Gates**:
- All files under size cap
- All completed tasks have evidence logs
- All risky changes have git rollback tags
- Session state always up-to-date
- Standup summaries generated daily

**User Experience**:
- Developer can resume work in <30 seconds (read `SESSION.md` OR `.session-state.md`)
- New team members productive in <1 week
- Zero "why did we do this?" moments (rationale documented)
- Phase transitions smooth (acceptance criteria clear)

---

## 📖 Additional Resources

**Framework Docs**:
- flowstate-ai-se-framework-v2.5.0.md (main concepts)
- QUICKSTART.md (getting started)
- REFERENCE.md (detailed rules)
- TEMPLATES.md (all templates)
- CHANGELOG.md (version history)
- TROUBLESHOOTING.md (diagnostics & recovery) [NEW in v2.3.1]

**Troubleshooting**: See [TROUBLESHOOTING.md](TROUBLESHOOTING.md) § AI Bootstrap Protocol

---

## 🆘 Emergency Recovery

**If FlowState stops responding** or you lose framework awareness:

1. **User command**: `Read TROUBLESHOOTING.md and follow its AI instructions to diagnose and restore FlowState SE framework functionality`

2. **Your action**: Read [TROUBLESHOOTING.md](TROUBLESHOOTING.md) and execute the 7-Phase AI Bootstrap Protocol

**This works even when you have ZERO FlowState awareness** - the bootstrap protocol is self-contained and will restore your framework context.

**Never overwrite user data** - All recovery operations preserve `TASKS.md`, `SESSION.md`, and other user state files. Only adapter files (like this one) may be restored.

---

**Remember**: You are an autonomous agent. Make decisions, execute work, maintain quality, document everything. The user trusts you to follow FlowState discipline—earn that trust through consistent execution.
```

---

### AGENTS.md Template (Copilot/Codex)

**Filename**: `AGENTS.md` (standard) OR `.ai-adapter.md` (obfuscated)

```markdown
# FlowState AI Framework - Agent Instructions

**Version**: 2.5.0 (Software Engineering Edition)
**Platform**: GitHub Copilot / OpenAI Codex / Cursor / JetBrains AI / Windsurf
**Last Updated**: [Auto-generated timestamp]

---

## 🎯 Core Principle

This project uses the **FlowState AI Framework** for disciplined, phase-driven development.

**Your role**: Follow the Meta-Rules, respect phase boundaries, leave evidence trails, and maintain code quality.

---

## 📚 Framework Files (Read These First)

### Primary References
- **`FLOWSTATE.md` OR `.project-config.md`** - All Meta-Rules, current phase, project configuration
- **`TASKS.md` OR `.tasks.md`** - Current task board (Backlog → In-Progress → Done)
- **`SESSION.md` OR `.session-state.md`** - Session state, context restoration, standup summaries

### Supporting Files
- **`docs/[project]-master-plan.md` OR `docs/.master-plan.md`** - Phase definitions and success criteria
- **`plans/PLAN-*.md` OR `plans/.plan-*.md`** - Detailed requirements for complex features
- **`logs/*.log` OR `logs/.log-*.txt`** - Evidence trails from completed work

---

## 🚀 Session Workflow

### Recognizing "FlowState SE" Command

When user says **"FlowState SE"**, check if `FLOWSTATE.md` OR `.project-config.md` exists:

**If FLOWSTATE.md OR .project-config.md does NOT exist:**
→ This is initialization. Execute the AI Initialization Protocol from flowstate-ai-se-framework-v2.5.0.md § AI INITIALIZATION PROTOCOL

**If FLOWSTATE.md OR .project-config.md exists:**
→ This is session resume. Execute the session resume protocol below.

---

### When Starting Work (Session Resume)
1. Read `SESSION.md` OR `.session-state.md` to restore context
2. Check `TASKS.md` OR `.tasks.md` for current priorities
3. Verify current phase in `FLOWSTATE.md` OR `.project-config.md`
4. Acknowledge active work or ask for direction

### During Work
1. Follow Work → Right → Fast progression (Meta-Rule 2)
2. Respect phase boundaries (Meta-Rule 1)
3. Keep files under size caps (Meta-Rule 8, adapted by language)
4. Update `TASKS.md` OR `.tasks.md` as you progress
5. Create plan documents for complex tasks (≥2 clarifying questions)

### When Closing Session
1. Update `SESSION.md` OR `.session-state.md` with today's progress
2. Move completed tasks to Done in `TASKS.md` OR `.tasks.md`
3. Generate standup summary in `SESSION.md` OR `.session-state.md`
4. Tag git state for rollback if significant work done
5. Save evidence logs to `logs/` directory

---

## 📋 The 13 Meta-Rules (Quick Reference)

**Read `FLOWSTATE.md` OR `.project-config.md` for full details.** Here's the quick version:

1. **Phase Boundaries** - No Phase N+1 work until Phase N complete
2. **Work → Right → Fast** - Function first, quality second, performance third
3. **One Task In-Progress** - Limit WIP to prevent context switching
4. **Keep It Simple** - Delete before abstracting
5. **Ask Why** - Every task needs documented rationale
6. **Leave Breadcrumbs** - Provide evidence trails (logs, tests, git tags)
7. **Stage Work Visibly** - Label commits with [Work], [Right], [Fast]
8. **Small & Focused Files** - Stay under size cap (language-adapted)
9. **Commit Discipline** - Tag rollback points before risky changes
10. **Refactor Discipline** - Proactively pay down complexity debt
11. **Subscription Context** - Note tier gating for features (if applicable)
12. **Entitlement Testing** - Test enabled AND disabled states (if applicable)
13. **Comprehension Debt** - Optimize for human understanding first

---

## 🏗️ Build & Test Commands

[Auto-populated during initialization based on package.json/detected stack]

```bash
# Development
[dev command]

# Testing
[test command]

# Build
[build command]

# Linting
[lint command]
```

---

## 🎨 Code Style

**Language**: [Auto-detected]
**File Size Cap**: [Auto-adapted based on language]
**Proactive Warning Trigger**: [90% of cap]

[Additional project-specific style guidelines from FLOWSTATE.md OR .project-config.md]

---

## 🔄 Plans System

**Trigger**: If you need ≥2 clarifying questions → Create a plan document

**Process**:
1. Ask clarifying questions (2-5 questions)
2. Create `plans/PLAN-XXX-[feature-slug].md` OR `plans/.plan-XXX-[feature-slug].md`
3. Document all context (requirements, architecture, constraints, risks)
4. Cross-reference in `TASKS.md` OR `.tasks.md`: `Plan: plans/PLAN-XXX-*.md` OR `plans/.plan-XXX-*.md`
5. When implementing, read plan first for full context

---

## ⚠️ Critical Constraints

- **Never violate phase boundaries** - Check current phase before starting work
- **Always provide evidence** - Test output, logs, screenshots for completed tasks
- **Always tag git state** - Before/after tags for risky changes
- **Always ask for rationale** - If task lacks "Why this approach?", ask user

---

## 🤖 Platform-Specific Notes (GitHub Copilot / Codex)

### For GitHub Copilot Agent Mode:
- Use autonomous execution for multi-step tasks
- Self-heal on errors (iterate until tests pass)
- Submit PRs with evidence and updated `TASKS.md` OR `.tasks.md`

### For OpenAI Codex:
- Use @FLOWSTATE.md OR @.project-config.md, @TASKS.md OR @.tasks.md, @SESSION.md OR @.session-state.md syntax for direct reference
- Leverage 7+ hour sessions for complex multi-day features
- Sync internal to-do with `TASKS.md` OR `.tasks.md` at session boundaries

---

## 📖 Additional Resources

**Quick Start**: See QUICKSTART.md in framework directory
**Detailed Reference**: See REFERENCE.md in framework directory
**Troubleshooting**: See REFERENCE.md § Troubleshooting
**Templates**: See TEMPLATES.md for all document templates

---

**Remember**: FlowState exists to make you more effective and the developer's life easier. Follow the rules, ask questions when uncertain, and always leave things better than you found them.
```

---

### flowstate.mdc Template (Cursor)

**Filename**: `.cursor/rules/flowstate.mdc` (standard) OR `.cursor/rules/project.mdc` (obfuscated)

```markdown
---
description: FlowState AI Framework rules for software engineering
globs:
  - "**/*.{ts,tsx,js,jsx,py,go,rs,java,kt,swift}"
  - "**/FLOWSTATE.md"
  - "**/.project-config.md"
  - "**/TASKS.md"
  - "**/.tasks.md"
  - "**/SESSION.md"
  - "**/.session-state.md"
  - "**/plans/*.md"
alwaysApply: true
---

# FlowState AI Framework - Cursor Integration

**Version**: 2.5.0 (Software Engineering Edition)
**Last Updated**: [Auto-generated]

---

## 🎯 Core Principle

This project uses **FlowState** for disciplined, phase-driven development.

Before any code changes:
1. Read **`FLOWSTATE.md` OR `.project-config.md`** (rules and current phase)
2. Read **`TASKS.md` OR `.tasks.md`** (current priorities)
3. Read **`SESSION.md` OR `.session-state.md`** (session context)

---

## 📚 Framework Files

### Primary
- **`FLOWSTATE.md` OR `.project-config.md`** - All Meta-Rules, phase definitions, project config
- **`TASKS.md` OR `.tasks.md`** - Task board (Backlog → In-Progress → Done)
- **`SESSION.md` OR `.session-state.md`** - Session state, standup summaries

### Supporting
- **`docs/[project]-master-plan.md` OR `docs/.master-plan.md`** - Phase acceptance criteria
- **`plans/PLAN-*.md` OR `plans/.plan-*.md`** - Detailed requirements for complex features
- **`logs/*.log` OR `logs/.log-*.txt`** - Evidence trails

---

## 🔄 Workflow

### Recognizing "FlowState SE" Command

When user says **"FlowState SE"**, check if `FLOWSTATE.md` OR `.project-config.md` exists:

**If FLOWSTATE.md OR .project-config.md does NOT exist:**
→ This is initialization. Execute the AI Initialization Protocol from flowstate-ai-se-framework-v2.5.0.md § AI INITIALIZATION PROTOCOL

**If FLOWSTATE.md OR .project-config.md exists:**
→ This is session resume. Read `FLOWSTATE.md` OR `.project-config.md`, `TASKS.md` OR `.tasks.md`, `SESSION.md` OR `.session-state.md` and report current state.

---

### Before Editing Files
1. Check current phase in `FLOWSTATE.md` OR `.project-config.md`
2. If plan exists for task (`plans/PLAN-*.md` OR `plans/.plan-*.md`), read it first
3. Verify task is in `TASKS.md` OR `.tasks.md`

### After Completing Work
1. Run tests, save output to `logs/[feature]_YYYY-MM-DD_HHMM.log` OR `logs/.log-[feature]_YYYY-MM-DD_HHMM.txt`
2. Update `TASKS.md` OR `.tasks.md` (move task to Testing/Done)
3. Notify user to update `SESSION.md` OR `.session-state.md`

### For Complex Tasks
If ≥2 clarifying questions needed:
1. Ask questions
2. Create plan document: `plans/PLAN-XXX-[feature].md` OR `plans/.plan-XXX-[feature].md`
3. Reference in `TASKS.md` OR `.tasks.md`
4. Implement from plan

---

## 📋 The 13 Meta-Rules (Quick Ref)

1. **Phase Boundaries** - No Phase N+1 work
2. **Work → Right → Fast** - Progressive refinement
3. **One Task In-Progress** - Limit WIP
4. **Keep It Simple** - Delete before abstracting
5. **Ask Why** - Document rationale
6. **Leave Breadcrumbs** - Evidence trails required
7. **Stage Work** - Label [Work]/[Right]/[Fast]
8. **Small Files** - Language-adapted caps
9. **Commit Discipline** - Tag before/after
10. **Refactor Discipline** - Every 5 tasks
11. **Subscription Context** - Note tier gating
12. **Entitlement Testing** - Test both states
13. **Comprehension Debt** - Human understanding first

**Full details**: `FLOWSTATE.md` OR `.project-config.md`

---

## 🏗️ Code Standards

**File Size Cap**: [Auto-adapted] LOC
**Proactive Warning**: [90% of cap] LOC

### Verification
```bash
[Language-specific verification command from FLOWSTATE.md OR .project-config.md]
```

---

## 🎨 Git Discipline

### Before Risky Changes
```bash
git tag [feature]-before -m "Safe rollback point"
```

### After Validation
```bash
git tag [feature]-after -m "Validated: [outcome]"
```

### Commit Format
```
[type]([scope]): [description] [Stage]

Examples:
feat(auth): Implement Clerk integration [Work]
refactor(api): Extract validation logic [Right]
perf(db): Add query caching [Fast]
```

---

## ⚠️ Critical Constraints

- Check phase before starting work (`FLOWSTATE.md` OR `.project-config.md`)
- Provide evidence for completed tasks (`logs/`)
- Create plans for complex tasks (≥2 questions)
- Respect file size caps (proactive warnings at 90%)

---

## 📖 Resources

**Framework**: See flowstate-ai-se-framework-v2.5.0.md
**Quick Start**: QUICKSTART.md
**Reference**: REFERENCE.md
**Templates**: TEMPLATES.md
**Troubleshooting**: TROUBLESHOOTING.md [NEW in v2.3.1]

---

**Remember**: Cursor gives you control. Review proposals before accepting. FlowState provides the discipline—you provide the judgment.
```

---

### .cursorrules Template (Cursor Legacy)

**Filename**: `.cursorrules` (unchanged in both modes)

```markdown
# Cursor Rules - FlowState AI Framework

## Context
This project uses the FlowState AI Framework (Software Engineering Edition v2.5.0).

**IMPORTANT**: Migrating to new .cursor/rules/*.mdc format. This file provides backward compatibility.

## Core Rules

### Read Framework Files First
Before any work:
- `FLOWSTATE.md` OR `.project-config.md` (all Meta-Rules and current phase)
- `TASKS.md` OR `.tasks.md` (current task priorities)
- `SESSION.md` OR `.session-state.md` (session context)

### Phase Boundaries (Meta-Rule 1)
No Phase N+1 work until Phase N complete. Check current phase in `FLOWSTATE.md` OR `.project-config.md`.

### Work → Right → Fast (Meta-Rule 2)
Function first, quality second, performance third. Label commits with stage.

### File Size Discipline (Meta-Rule 8)
Stay under [X] LOC cap (language-adapted). Warn at 90% of cap.

### Evidence Trails (Meta-Rule 6)
Always provide test output, logs, or validation for completed work.

### Plans System
If ≥2 clarifying questions needed → Create plan document in `plans/PLAN-XXX-*.md` OR `plans/.plan-XXX-*.md`

### Recognizing "FlowState SE" Command
When user says **"FlowState SE"**, check if `FLOWSTATE.md` OR `.project-config.md` exists:
- If `FLOWSTATE.md` OR `.project-config.md` does NOT exist → Execute AI Initialization Protocol from flowstate-ai-se-framework-v2.5.0.md
- If `FLOWSTATE.md` OR `.project-config.md` exists → Resume session (read `FLOWSTATE.md` OR `.project-config.md`, `TASKS.md` OR `.tasks.md`, `SESSION.md` OR `.session-state.md`, report status)

## Before Editing Files
1. Check current phase in `FLOWSTATE.md` OR `.project-config.md`
2. If plan exists for this task, read it first
3. Tag rollback point: git tag [feature]-before

## After Completing Work
1. Run tests, save output to `logs/[feature]_YYYY-MM-DD_HHMM.log` OR `logs/.log-[feature]_YYYY-MM-DD_HHMM.txt`
2. Update `TASKS.md` OR `.tasks.md` (move task to Testing/Done)
3. Tag success: git tag [feature]-after
4. Notify user to update `SESSION.md` OR `.session-state.md`

## File References
- **Rules**: `FLOWSTATE.md` OR `.project-config.md`
- **Tasks**: `TASKS.md` OR `.tasks.md`
- **Session**: `SESSION.md` OR `.session-state.md`
- **Plans**: `plans/PLAN-*.md` OR `plans/.plan-*.md`
- **Framework**: flowstate-ai-se-framework-v2.5.0.md

## Migration Note
Please upgrade to new .cursor/rules/flowstate.mdc OR .cursor/rules/project.mdc format for enhanced features. See .cursor/rules/ directory.
```

---

### .github/copilot-instructions.md Template (GitHub Copilot)

**Filename**: `.github/copilot-instructions.md`

```markdown
# FlowState AI Framework - Copilot Instructions

**Version**: 2.5.0 (Software Engineering Edition)
**Project**: [Auto-detected]
**Last Updated**: [Auto-generated timestamp]

---

## 🎯 Purpose

These instructions configure **GitHub Copilot** (including the Coding Agent) to
work under the **FlowState AI Framework** for this repository.

Copilot should:
- Read the core FlowState files before multi-step work
- Respect FlowState meta-rules and phase boundaries
- Use FlowState commands to manage tasks and sessions

---

## 📚 Read These Files First

- `FLOWSTATE.md` OR `.project-config.md` — Meta-Rules and current phase
- `TASKS.md` OR `.tasks.md` — Task board and priorities
- `SESSION.md` OR `.session-state.md` — Session state and recent work

Whenever the user invokes the Copilot Coding Agent for non-trivial work,
Copilot should read these files (or refresh them if already loaded) before
executing a plan.

---

## 🔄 Session Commands

Recognize and support these commands:

- **"FlowState SE"**
  - If `FLOWSTATE.md`/`.project-config.md` missing → Initialization
  - If present → Session resume (read SESSION/TASKS/FLOWSTATE, then report state)

- **"FlowState status"**
  - Run a read-only health check:
    - Framework: core files exist and parse
    - Runtime: FLOWSTATE/TASKS/SESSION look consistent
    - Platform adapters: present for this platform (see AGENTS.md)
    - Git/privacy: report high-level status if available

- **"FlowState doctor"**
  - Run diagnostics (similar to TROUBLESHOOTING.md) and offer fixes
  - Do not modify user code without explicit confirmation

---

## 🧠 Behavior Guidelines

- Prefer following the workflows described in `AGENTS.md`
- When planning larger changes:
  - Read any relevant `plans/PLAN-*.md` files
  - Update `TASKS.md` as work progresses
  - Capture evidence in `logs/`
- When in doubt about FlowState behavior, refer the user to `TROUBLESHOOTING.md`.
```

---

### .github/instructions/flowstate.instructions.md Template (Copilot Coding Agent)

**Filename**: `.github/instructions/flowstate.instructions.md`

```markdown
# FlowState AI Framework - Copilot Coding Agent Mode

**Version**: 2.5.0 (Software Engineering Edition)
**Scope**: Copilot Coding Agent tasks that use FlowState

---

## 🎯 Role

You are the **Copilot Coding Agent** operating under the **FlowState AI Framework**.

Your responsibilities:
- Follow FlowState meta-rules (see FLOWSTATE.md/.project-config.md)
- Respect the current phase and task priorities
- Keep TASKS.md and SESSION.md in sync with actual work

---

## 📚 Always Load Context From

Before starting any multi-step task:

1. Read `FLOWSTATE.md` OR `.project-config.md`
2. Read `TASKS.md` OR `.tasks.md`
3. Read `SESSION.md` OR `.session-state.md`
4. If a plan exists for the task, read `plans/PLAN-*.md`

---

## 🧭 Commands You Should Support

- `"FlowState SE"` → run the initialization/resume protocol as described in
  flowstate-ai-se-framework-v2.5.0.md.

- `"FlowState status"` → summarize project state using FLOWSTATE/TASKS/SESSION.

- `"FlowState doctor"` → run diagnostics using TROUBLESHOOTING.md and offer
  non-destructive fixes (adapter restoration, configuration suggestions).

---

## 🔌 Adapters

This repository also contains FlowState adapters for other platforms
(CLAUDE.md, .cursor/rules/*.mdc, etc.). Do not modify those files unless
explicitly asked; treat them as project configuration.
```

---

### JetBrains AI Rules Template

**Filename**: `.aiassistant/rules/flowstate.md`

```markdown
# FlowState AI Framework - JetBrains AI Rules

**Version**: 2.5.0 (Software Engineering Edition)
**Project**: [Auto-detected]
**Last Updated**: [Auto-generated timestamp]

---

## 🎯 Rule Purpose

These rules configure **JetBrains AI Assistant** to operate under the
**FlowState AI Framework** when working in this project.

---

## 📚 Always Read Before Major Changes

- `FLOWSTATE.md` OR `.project-config.md`
- `TASKS.md` OR `.tasks.md`
- `SESSION.md` OR `.session-state.md`

When the user asks for non-trivial work (new features, refactors, bug hunts),
JetBrains AI should read these files and follow their guidance.

---

## 🔄 FlowState Commands

Recognize and support:

- `"FlowState SE"` / `"Resume FlowState"` / `"FlowState status"` /
  `"FlowState doctor"`.

For semantics, follow the descriptions in `TROUBLESHOOTING.md`.

---

## 🧠 Behavior

- Respect phase boundaries and meta-rules from FLOWSTATE.md
- Keep tasks and session state consistent when performing work
- Prefer small, focused changes with evidence (tests/logs) when possible
```

---

### Windsurf Rules Template

**Filename**: `.windsurfrules`

```markdown
# FlowState AI Framework - Windsurf Rules

**Version**: 2.5.0 (Software Engineering Edition)

---

## 📚 Project Rules

This project uses the **FlowState AI Framework**. When running in Windsurf:

1. Read `FLOWSTATE.md` OR `.project-config.md`
2. Read `TASKS.md` OR `.tasks.md`
3. Read `SESSION.md` OR `.session-state.md`

Use these files to:
- Understand current phase and priorities
- Decide which tasks to work on
- Keep a consistent log of changes and evidence

---

## 🔄 Commands

Support the following commands:
- `"FlowState SE"` / `"Resume FlowState"` / `"FlowState status"` /
  `"FlowState doctor"`

Behavior for these commands should mirror the descriptions in
`TROUBLESHOOTING.md` for this edition.
```

---

## Supporting Files

### Plan Document Template

**Filename**: `plans/PLAN-[XXX]-[feature-name].md` (standard) OR `plans/.plan-[XXX]-[feature-name].md` (obfuscated)

```markdown
# PLAN-[XXX]: [Feature Name]

**Created**: [YYYY-MM-DD HH:MM]
**Owner**: [Name]
**Status**: Pending (not started)
**Related Tasks**: `TASKS.md` OR `.tasks.md` ("[task name]")
**Phase**: Phase [N]

---

## Context & Rationale

**Why**: [Why this feature exists? Business goal?]

**Business Goal**: [Revenue, retention, competitive advantage?]

**Success Metric**: [How do we measure success?]

---

## Requirements

### Functional Requirements
1. **[Requirement 1 Name]**
   - [Specific functionality description]
   - [User story or use case]

2. **[Requirement 2 Name]**
   - [Specific functionality description]
   - [User story or use case]

3. **[Requirement 3 Name]**
   - [Specific functionality description]
   - [User story or use case]

### Non-Functional Requirements
- [Performance: Response time, throughput, etc.]
- [Security: Auth, data protection, compliance]
- [Usability: UX requirements, accessibility]
- [Scalability: User load, data volume]

---

## Architecture Decisions

### [Decision 1 Name]
**Choice**: [Technology/Pattern chosen]

**Rationale**: [Why this vs alternatives?]

**Pros**:
- [Pro 1]
- [Pro 2]

**Cons**:
- [Con 1 with mitigation]
- [Con 2 with mitigation]

### [Decision 2 Name]
[Same structure as above]

### [Decision 3 Name]
[Same structure as above]

### Deferred Decisions (Phase [N+1]+)
- [Decision 1] → Phase [N+1] (Reason: [Why deferred])
- [Decision 2] → Phase [N+1] (Reason: [Why deferred])

---

## Constraints & Assumptions

**Constraints**:
- [Constraint 1: e.g., "Free tier users cannot access this feature"]
- [Constraint 2: e.g., "Must work with existing auth system"]
- [Constraint 3: e.g., "API response must be <200ms"]

**Assumptions**:
- [Assumption 1: e.g., "Users understand 'workspace' concept"]
- [Assumption 2: e.g., "Email invites don't get spam-filtered"]
- [Assumption 3: e.g., "Existing users want to stay on current plan"]

---

## Acceptance Criteria (DoD)

- [ ] [Criterion 1: Specific, testable]
- [ ] [Criterion 2: Specific, testable]
- [ ] [Criterion 3: Specific, testable]
- [ ] [Criterion 4: Specific, testable]
- [ ] Tests pass ([Specific test suites])
- [ ] Evidence captured (`logs/[feature]_*.log` OR `logs/.log-[feature]_*.txt`)
- [ ] Git tags created ([feature]-before, [feature]-after)
- [ ] Documentation updated (README, `SESSION.md` OR `.session-state.md` if applicable)

---

## Risks & Mitigations

| Risk | Impact (H/M/L) | Probability (H/M/L) | Mitigation |
|------|----------------|---------------------|------------|
| [Risk 1] | [H/M/L] | [H/M/L] | [Mitigation strategy] |
| [Risk 2] | [H/M/L] | [H/M/L] | [Mitigation strategy] |
| [Risk 3] | [H/M/L] | [H/M/L] | [Mitigation strategy] |

---

## Implementation Plan

### Phase 1: [Phase Name] (Week [N])
1. [Step 1]
2. [Step 2]
3. [Step 3]
4. [Validation: How to verify this phase complete]

### Phase 2: [Phase Name] (Week [N+1])
5. [Step 4]
6. [Step 5]
7. [Step 6]
8. [Validation: How to verify this phase complete]

### Phase 3: [Phase Name] (Week [N+2])
9. [Step 7]
10. [Step 8]
11. [Validation: How to verify complete]

**Estimated Effort**: [X] weeks ([Y] developer(s) full-time)

---

## Open Questions

1. **Q**: [Question 1]
   **A**: [Answer or "Deferred to Phase [N]" or "TBD"]

2. **Q**: [Question 2]
   **A**: [Answer or "Deferred to Phase [N]" or "TBD"]

3. **Q**: [Question 3]
   **A**: [Answer or "Deferred to Phase [N]" or "TBD"]

---

## References

- [External documentation link 1]
- [External documentation link 2]
- [Related PLAN-XXX link if applicable]

---

*This plan auto-generated by FlowState AI Framework during task creation.*
*Reference: `TASKS.md` OR `.tasks.md` | PLAN-[XXX]*
```

---

## 📝 Usage Notes for AI

### When Initializing FlowState

1. **Read these templates** from TEMPLATES.md
2. **Copy template text** for each file
3. **Replace placeholders** with project-specific values:
   - `[Project Name]` → Detected from package.json or git
   - `[YYYY-MM-DD]` → Current timestamp
   - `[Auto-detected]` → Scan project and detect values
   - `[From initialization]` → Use user's answers from strategic questions
4. **Adapt content** based on context:
   - File size caps → Language-specific
   - Subscription rules → Enable if user selected "Yes"
   - Tech stack → Detected frameworks and libraries
   - **Filename mode** → Use standard OR obfuscated based on Step 2.5 choice
5. **Create files** in correct locations:
   - Universal files: Project root
   - Adapters: Project root (.cursor/ subdirectory for Cursor)
   - Supporting: docs/, plans/, logs/ directories

### Template Customization

**Users can customize templates** by:
1. Editing `FLOWSTATE.md` OR `.project-config.md` after initialization
2. Adding project-specific sections
3. Removing non-applicable sections (e.g., subscription rules if no tiers)

**AI should preserve customizations** when updating files.

### Filename Mode Selection (v2.2)

During initialization (Step 2.5), AI will:
1. Detect if `.git/` exists
2. Offer privacy mode options
3. If "Private Ignore" selected, offer obfuscation choice
4. Store choice in memory for file creation
5. Use correct filenames throughout initialization

**Consistency**: Once mode is chosen, ALL FlowState files use that mode.

---

## 🎓 Scaffolding Response Templates [NEW in v2.3]

**Purpose**: These templates show AI assistants how to adjust response verbosity across different scaffolding levels.

**For AI**: Study these templates to internalize the "feel" of each scaffolding level
**For Users**: See examples of what each scaffolding level looks like in practice

**Coverage**: 10 common scenarios showing all 4 levels (Learner, Growth, Balanced, Expert)

---

### Scenario 1: Session Resume

**Context**: User says "Resume FlowState". TASKS.md has 1 in_progress task ("Implement user authentication"), Prove stage.

#### Learner Response (300-500 words)

```
I'm going to resume your FlowState session. Let me explain my approach:

**Why I'm starting with TASKS.md**: At the start of every session, I need to check our task list to understand context. This is part of the Session Resume Protocol (see framework file § AI Initialization Protocol).

**What I'm looking for**:
- Current task status (in_progress tasks show what we were working on)
- Completed tasks (to avoid redoing work)
- Pending tasks (to understand overall project state)

Reading TASKS.md...

[Reads TASKS.md]

Found 3 tasks total:
- 1 in_progress: "Implement user authentication" (60% complete per last session)
- 2 pending: "Add password reset", "Implement rate limiting"

**Stage check**: We're in Prove stage (based on FLOWSTATE.md). This means I should focus on production-readiness for the auth system, not just getting it working.

**What "Prove stage" means for this task**:
- ✅ Tests must pass (unit + integration)
- ✅ Error handling must be comprehensive
- ✅ Security best practices must be followed
- ✅ Documentation must be complete

**Next step**: I'll read SESSION.md to see exactly where we left off and what was accomplished in the last session.

Reading SESSION.md...

[Reads SESSION.md]

Last session summary:
- Completed: Login/signup flows using Clerk
- Next: Add session management + protected routes
- Blockers: None

**My recommendation**: Let's continue with session management (storing session tokens, handling refresh). This is the logical next step to complete the authentication system.

Ready to continue? I'll start by reading the current auth implementation to understand what's already there.
```

---

#### Growth Response (150-250 words)

```
Resuming FlowState session.

**Approach**: Read TASKS.md → Check SESSION.md → Understand current state

Reading TASKS.md...

[Reads TASKS.md]

Current status:
- 1 in_progress: "Implement user authentication" (60% complete)
- Stage: Prove (production-readiness focus)

**Meta-Rule check**: We're in Prove stage, so I'll focus on tests, error handling, and security for the auth system.

Reading SESSION.md...

[Reads SESSION.md]

Last session:
- Completed: Login/signup flows (Clerk integration)
- Next: Session management + protected routes

**Recommendation**: Continue with session management (the next logical step to complete auth).

Ready to proceed. I'll read the current auth implementation first to understand what's there.
```

---

#### Balanced Response (100-150 words)

```
Resuming FlowState session.

[Reads TASKS.md]

Current task: "Implement user authentication" (in_progress, 60% complete, Prove stage)

[Reads SESSION.md]

Last session: Completed login/signup flows (Clerk)
Next: Session management + protected routes

Recommendation: Continue with session management.

Reading current auth implementation...
```

---

#### Expert Response (50-100 words)

```
[Reads TASKS.md → 1 in_progress: auth (60%, Prove)]
[Reads SESSION.md → Last: login/signup done, Next: session mgmt]

Continuing with session management.

[Reads current auth implementation]
```

---

### Scenario 2: Adding Error Handling

**Context**: User asks "Add error handling to the login endpoint"

#### Learner Response

```
I'll add comprehensive error handling to the login endpoint. Let me break down my approach:

**Why error handling matters in Prove stage**: We're currently in Prove stage (per FLOWSTATE.md), which means production-readiness is critical. Error handling prevents crashes and provides useful feedback to clients.

**Orchestration strategy** (my sequence of actions):
1. Read current login endpoint code (understand what's there)
2. Identify failure points (where errors can occur)
3. Add try/catch blocks (handle errors gracefully)
4. Add input validation (prevent bad data)
5. Add appropriate HTTP status codes (4xx for client errors, 5xx for server errors)
6. Update tests (verify error handling works)
7. Update TASKS.md (mark subtask complete)

**Meta-Rule application**: This aligns with Meta-Rule 3 (One Task In-Progress) because error handling is part of our current in_progress auth task. It's also part of Meta-Rule 2 (Work → Right → Fast) - we're in the "Right" stage, making the auth system clean and robust.

Let me start by reading the current login endpoint implementation...

[Reads file]

I can see the endpoint at `src/auth/login.ts:45-78`. Currently it has:
- ✅ Basic Clerk authentication
- ❌ No try/catch (will crash on errors)
- ❌ No input validation (accepts any payload)
- ❌ Generic error responses (not helpful for debugging)

**Failure points I've identified**:
1. Clerk authentication could fail (invalid credentials, network error)
2. Database lookup could fail (connection error)
3. Input could be malformed (missing email/password)

I'll add error handling for all three cases...

[Implements with detailed explanations for each change]
```

---

#### Growth Response

```
Adding error handling to login endpoint.

**Approach**: Read current code → Identify failure points → Add try/catch → Update tests

**Meta-Rule check**: This is part of our in_progress auth task (Meta-Rule 3: One Task In-Progress) and aligns with Prove stage requirements (production-ready error handling).

Reading current endpoint...

[Reads file]

Current state (src/auth/login.ts:45-78):
- Basic Clerk auth ✅
- No try/catch ❌
- No input validation ❌

**Failure points**:
1. Clerk auth failures
2. Database errors
3. Malformed input

Adding error handling...

[Implements]

Added:
- Try/catch for Clerk auth (returns 401 on invalid credentials)
- Input validation (returns 400 on malformed data)
- Database error handling (returns 500 on connection errors)
- Appropriate HTTP status codes

Updating tests...

[Updates tests]

Error handling complete. Tests passing.

Marking subtask complete in TASKS.md.
```

---

#### Balanced Response

```
Adding error handling to login endpoint.

[Reads current endpoint at src/auth/login.ts:45-78]

Current issues:
- No try/catch
- No input validation
- Generic errors

[Implements error handling]

Added:
- Try/catch for Clerk auth (401 on failure)
- Input validation (400 on bad data)
- Database error handling (500 on connection errors)

[Updates tests to cover error cases]

Tests passing. TASKS.md updated.
```

---

#### Expert Response

```
[Reads login endpoint → Adds try/catch (auth, validation, db errors) → Updates tests → TASKS.md updated]
```

---

### Scenario 3: Refactoring for DRY

**Context**: User says "Refactor the duplicate validation logic across auth endpoints"

#### Learner Response

```
I'll refactor the duplicate validation logic. Let me explain why this matters and how I'll approach it:

**Why refactoring now**: We've completed 5 tasks (checked TASKS.md § Refactor Counter: 5/5). This triggers Meta-Rule 10 (Refactor Discipline), which says we should proactively pay down complexity debt every 5 tasks. This prevents technical debt from accumulating.

**What I'm refactoring**: I've noticed that login, signup, and password reset endpoints all have similar validation code (checking email format, password requirements, etc.). This violates the DRY principle (Don't Repeat Yourself).

**Orchestration strategy**:
1. Search for all auth endpoints (find the duplicated code)
2. Read each endpoint (understand what's being validated)
3. Extract common validation logic (create a shared validator function)
4. Update all endpoints to use shared validator (remove duplication)
5. Add tests for the validator (ensure it works correctly)
6. Run existing tests (ensure nothing broke)
7. Git commit with [Right] tag (this is "Right" stage work per Meta-Rule 7)
8. Reset refactor counter in TASKS.md (back to 0/5)

Let me start by searching for auth endpoints...

[Searches for auth endpoints]

Found 3 endpoints with duplicate validation:
- src/auth/login.ts:52-65 (email validation, password validation)
- src/auth/signup.ts:48-61 (same validation logic)
- src/auth/reset.ts:55-68 (same validation logic)

**Duplication detected**: All three validate email format with regex and password length. This is exactly what DRY helps us fix.

Creating shared validator...

[Creates src/auth/validators.ts with validateEmailPassword function]

Now I'll update each endpoint to use the shared validator...

[Updates endpoints one by one with explanations]
```

---

#### Growth Response

```
Refactoring duplicate validation logic across auth endpoints.

**Meta-Rule 10 triggered**: Refactor counter at 5/5, time to pay down complexity debt.

**Approach**: Search for auth endpoints → Extract common validation → Update endpoints → Test

Searching for endpoints...

[Searches]

Found duplication in:
- src/auth/login.ts
- src/auth/signup.ts
- src/auth/reset.ts

All three validate email/password identically (DRY violation).

Creating shared validator (src/auth/validators.ts)...

[Creates validators.ts]

Updating endpoints to use shared validator...

[Updates all 3 endpoints]

Running tests...

[Tests pass]

Committing with [Right] tag (Meta-Rule 7: Stage Work Visibly).

Refactor counter reset to 0/5 in TASKS.md.
```

---

#### Balanced Response

```
Refactoring duplicate auth validation (Meta-Rule 10: 5/5 tasks complete).

[Searches for auth endpoints]

Found duplication: login, signup, reset all validate email/password identically.

[Creates src/auth/validators.ts with shared validation]

[Updates 3 endpoints to use shared validator]

[Tests pass]

Committed with [Right] tag. Refactor counter reset (0/5).
```

---

#### Expert Response

```
[Refactoring duplicate validation (Meta-Rule 10)]
[Creates src/auth/validators.ts → Updates login/signup/reset → Tests pass → Committed [Right] → Counter reset]
```

---

### Scenario 4: Investigating a Bug

**Context**: User reports "Users getting 500 errors on login sometimes"

#### Learner Response

```
I'll investigate the intermittent 500 errors on login. Let me explain my debugging approach:

**Why this is tricky**: "Sometimes" means the error is non-deterministic - it doesn't happen every time. This usually indicates a race condition, external dependency failure, or environment-specific issue.

**Orchestration strategy for debugging**:
1. Read the login endpoint code (understand the flow)
2. Check logs for recent errors (see the actual error messages)
3. Identify the failure point (which line is throwing 500?)
4. Form hypotheses (what could cause this intermittently?)
5. Test hypotheses (reproduce if possible)
6. Fix the root cause (not just the symptom)
7. Add monitoring/alerting (catch it early in production)

**Meta-Rule application**: This is part of our in_progress auth task (Meta-Rule 3), and since we're in Prove stage, fixing production issues is priority.

Let me start by reading the login endpoint...

[Reads login code]

The endpoint at src/auth/login.ts:45-92 does these steps:
1. Validate input (lines 52-56)
2. Call Clerk auth (lines 60-65)
3. Look up user in database (lines 70-75)
4. Create session token (lines 78-82)
5. Return success (lines 85-90)

**Hypothesis formation**: A 500 error (server error) could come from:
- Clerk API timeout (external dependency)
- Database connection pool exhausted (resource issue)
- Session token signing failure (crypto issue)

Let me check the logs...

[Checks logs/auth*.log]

Found it! logs/auth_2026-01-15_0830.log shows:
```
Error: connect ETIMEDOUT - Database connection failed
at src/auth/login.ts:73
```

**Root cause identified**: The database connection is timing out intermittently. This happens when:
- The connection pool is full (all connections in use)
- The database is under heavy load
- Network latency spikes

**The fix**: We need to:
1. Add connection pool monitoring
2. Increase pool size if needed
3. Add retry logic with exponential backoff
4. Return better error to user (503 Service Unavailable instead of 500)

Implementing fix...

[Implements with detailed explanations]
```

---

#### Growth Response

```
Investigating intermittent 500 errors on login.

**Approach**: Read login code → Check logs → Identify failure point → Fix root cause

Reading login endpoint...

[Reads code]

Login flow:
1. Validate input
2. Clerk auth
3. Database lookup ← Likely failure point (DB errors often intermittent)
4. Create session
5. Return success

Checking logs...

[Checks logs/auth*.log]

Found error in logs/auth_2026-01-15_0830.log:
```
Error: connect ETIMEDOUT - Database connection failed
at src/auth/login.ts:73
```

**Root cause**: Database connection timeouts (connection pool exhausted or high latency).

**Fix**:
1. Add connection pool monitoring
2. Add retry logic (exponential backoff)
3. Return 503 (Service Unavailable) instead of 500

Implementing...

[Implements]

Added:
- Connection pool size increased (10 → 20)
- Retry logic (3 attempts, exponential backoff)
- Proper HTTP status (503 on DB timeout)

Testing with simulated DB latency...

[Tests]

Fixed. Monitoring added to catch this early next time.
```

---

#### Balanced Response

```
Investigating intermittent 500 errors on login.

[Reads login endpoint]

Flow: validate → Clerk auth → DB lookup → session → response

[Checks logs]

Error found in logs/auth_2026-01-15_0830.log:
```
Database connection timeout at src/auth/login.ts:73
```

Root cause: Connection pool exhaustion.

[Implements fix]

Added:
- Increased pool size (10 → 20)
- Retry logic (3 attempts, exponential backoff)
- 503 status on timeout

[Tests with simulated latency]

Fixed. Monitoring added.
```

---

#### Expert Response

```
[Login 500s → Checks logs → DB timeout at :73 → Pool exhaustion]
[Fixes: pool size 10→20, retry logic, 503 on timeout → Tested → Fixed]
```

---

### Scenario 5: Planning a Complex Feature

**Context**: User says "Add OAuth integration for Google and GitHub"

#### Learner Response

```
OAuth integration for Google and GitHub is a complex feature that needs a plan. Let me explain why and how I'll approach this:

**Why this needs a plan**: This touches multiple parts of the system (auth endpoints, user model, frontend flows). Per Meta-Rule 5 (Ask "Why This Approach?"), complex tasks require documented rationale in a plan document.

**What makes this complex**:
- Multiple OAuth providers (Google, GitHub have different APIs)
- Database schema changes (need to store provider + provider ID)
- Frontend changes (need social login buttons)
- Security considerations (CSRF protection, state validation)
- Error handling (what if OAuth provider is down?)

**Orchestration strategy for planning**:
1. Ask clarifying questions (understand requirements)
2. Create PLAN document (document approach and decisions)
3. Break into subtasks (make it manageable)
4. Get user approval (ensure alignment)
5. Then implement (once plan is approved)

Let me ask some clarifying questions:

**Question 1: OAuth scope**
- What user data do we need from Google? (email, profile photo, name?)
- What about from GitHub? (email, username, repositories?)

**Question 2: Account linking**
- If user has email/password account, can they link Google/GitHub to same account?
- Or are these separate accounts?

**Question 3: Priority**
- Which provider should we implement first? (Google, then GitHub? Or both together?)
- Is this blocking other work?

**Question 4: Existing users**
- Do existing users need to migrate to OAuth? Or is this just for new signups?

Once you answer these, I'll create a detailed plan document in `plans/PLAN-004-oauth-integration.md` that outlines:
- Architecture decisions (how OAuth flows work)
- Database schema changes (new columns, migrations)
- Security measures (state validation, CSRF tokens)
- Testing strategy (how to test OAuth without real Google/GitHub accounts)
- Rollout plan (staged release or all at once?)

Ready to answer those questions?
```

---

#### Growth Response

```
OAuth integration for Google and GitHub is complex - needs a plan before implementation.

**Why a plan**: Touches auth, database, frontend. Meta-Rule 5 (Ask "Why This Approach?") requires documented rationale for complex tasks.

**Clarifying questions**:

1. **OAuth scope**: What user data do we need from each provider?
2. **Account linking**: Can users link OAuth to existing email/password accounts?
3. **Priority**: Implement Google first, then GitHub? Or both together?
4. **Existing users**: Do they need to migrate to OAuth?

Once you answer, I'll create `plans/PLAN-004-oauth-integration.md` with:
- Architecture decisions (OAuth flows)
- Database changes (migrations)
- Security measures (CSRF, state validation)
- Testing strategy
- Rollout plan

Your answers?
```

---

#### Balanced Response

```
OAuth integration for Google + GitHub needs a plan (complex, multi-component feature).

**Questions**:
1. OAuth scope for each provider?
2. Account linking strategy?
3. Implementation priority (both together or sequential)?
4. Existing user migration?

Will create `plans/PLAN-004-oauth-integration.md` after your input.
```

---

#### Expert Response

```
[OAuth for Google+GitHub → Needs plan]

Questions:
1. Scope per provider?
2. Account linking?
3. Priority?
4. User migration?

Will create PLAN-004 after answers.
```

---

### Scenario 6: Approaching Stage Gate (Explore → Prove)

**Context**: User's project is nearing Explore → Prove transition

#### Learner Response

```
I notice we're approaching the Explore → Prove stage gate. Let me explain what this means and what we need to do:

**What is a stage gate**: A stage gate is a checkpoint before moving to the next development stage. It ensures we've validated our approach before investing in production-readiness. This is part of Meta-Rule 1 (Phase Boundaries) - we don't move forward until we've met the criteria.

**Current situation**:
- We're in Explore stage (building to understand the problem)
- We've completed the basic auth flow (login, signup work)
- Next stage: Prove (validate on fresh data, ensure production-readiness)

**Why the gate exists**: Explore stage is about rapid iteration and learning. If we jump straight to Prove without validation, we might build the wrong thing really well. The gate forces us to ask: "Does this actually work?"

**What we need to do before transitioning**:

**1. Validation on fresh data**
- Have we tested login/signup with real user flows (not just our test account)?
- Have we validated error cases (wrong password, network failures)?
- Have we checked edge cases (special characters in email, long passwords)?

**2. Evidence gathering**
- Do we have logs proving the auth flow works? (Check logs/ directory)
- Do we have test coverage? (Run test suite)
- Do we have user feedback? (Even if it's just you trying it)

**3. Decision point**
- Is the current approach viable? (Should we proceed to production-readiness?)
- Or do we need to pivot? (Maybe OAuth is better than email/password?)

Let me check our readiness...

[Checks TASKS.md, logs/, test coverage]

**Current readiness assessment**:
- ✅ Basic auth flow works (login, signup implemented)
- ✅ Tests exist (12 tests in src/auth/__tests__/)
- ✅ Logs show successful logins (logs/auth_2026-01-15_1430.log)
- ❌ No edge case testing (haven't tested invalid inputs systematically)
- ❌ No error monitoring (no Sentry or equivalent)

**My recommendation**: We're 80% ready for Prove stage, but need:
1. Add systematic error testing (invalid emails, SQL injection attempts, etc.)
2. Add basic error monitoring (at least console logs for now)

Once we complete those 2 items, we can confidently move to Prove stage and focus on production-readiness (security hardening, performance optimization, comprehensive error handling).

Want me to add those 2 items as tasks before we transition?
```

---

#### Growth Response

```
Approaching Explore → Prove stage gate (Meta-Rule 1: Phase Boundaries).

**Gate purpose**: Validate approach before investing in production-readiness.

**Gate requirements**:
1. Validation on fresh data (real user flows tested?)
2. Evidence gathering (logs, tests, feedback)
3. Decision point (proceed or pivot?)

Checking readiness...

[Checks TASKS.md, logs/, tests]

**Current status**:
- ✅ Basic auth flow works
- ✅ Tests exist (12 tests)
- ✅ Logs show successes
- ❌ No systematic edge case testing
- ❌ No error monitoring

**Recommendation**: 80% ready. Need:
1. Systematic error testing (invalid inputs, attacks)
2. Basic error monitoring (console logs minimum)

Add these tasks before transition? Then we can confidently move to Prove.
```

---

#### Balanced Response

```
Approaching Explore → Prove gate.

[Checks readiness: TASKS.md, logs/, tests]

Status:
- ✅ Auth flow works
- ✅ 12 tests
- ✅ Success logs
- ❌ Edge case testing
- ❌ Error monitoring

Recommendation: Add systematic error testing + monitoring before transition.

Add these tasks?
```

---

#### Expert Response

```
[Explore → Prove gate check]
[Status: 80% ready, need error testing + monitoring]

Add 2 tasks before transition?
```

---

### Scenario 7: Handling Scope Creep

**Context**: User says "Also add two-factor authentication while we're working on auth"

#### Learner Response

```
Two-factor authentication (2FA) is a great feature, but let me explain why we should defer it for now:

**Current context**:
- Phase: Phase 0 – Foundation (check FLOWSTATE.md)
- Current task: Implement user authentication (basic login/signup)
- Stage: Prove (production-readiness focus)

**Why 2FA should be deferred** (Meta-Rule 1: Phase Boundaries):

**1. Phase 0 scope**: Our Phase 0 acceptance criteria (from FLOWSTATE.md) are:
- [ ] Users can sign up with email/password
- [ ] Users can log in
- [ ] Sessions persist across page refreshes
- [ ] Basic error handling

Notice that 2FA is NOT in this list. Adding it now violates Meta-Rule 1 (Phase Boundaries), which says "No Phase N+1 work until Phase N complete."

**2. Complexity explosion**: 2FA adds:
- SMS or authenticator app integration (Twilio? TOTP?)
- Database schema changes (store 2FA secret, recovery codes)
- Frontend changes (2FA enrollment flow, verification UI)
- Security considerations (backup codes, account recovery)
- Testing complexity (how to test 2FA flows?)

This could easily double our auth timeline.

**3. Risk to current work**: If we add 2FA now:
- Current auth task remains in_progress longer (violates Meta-Rule 3: One Task In-Progress)
- We might introduce bugs in basic auth (more code = more surface area)
- We delay getting to other Phase 0 work (whatever's in TASKS.md backlog)

**What I recommend** (proper orchestration):

**Option 1: Defer to Phase 1** (Recommended)
1. I'll add "Two-factor authentication" to FLOWSTATE.md § Deferred Items (Phase 1+)
2. We finish current basic auth (login, signup, sessions)
3. We complete remaining Phase 0 work
4. Then we circle back to 2FA in Phase 1 (when we can give it proper attention)

**Option 2: Replace current scope** (Only if 2FA is truly critical)
1. We abandon basic email/password auth
2. We implement OAuth + 2FA from the start
3. This resets our timeline (probably adds 1-2 weeks)
4. We update Phase 0 acceptance criteria

**My strong recommendation**: Option 1 (defer). 2FA is important, but it's not a blocker for Phase 0 completion. We can add it in Phase 1 when we have a solid foundation.

Which option do you prefer?
```

---

#### Growth Response

```
2FA is a good idea, but should be deferred (Meta-Rule 1: Phase Boundaries).

**Current scope (Phase 0)**:
- Basic login/signup ✅
- Session persistence ✅
- Error handling 🔄

2FA is NOT in Phase 0 acceptance criteria.

**Why defer**:
1. Violates Phase Boundaries (Phase N+1 work)
2. Adds complexity (SMS/TOTP, schema changes, recovery codes)
3. Delays Phase 0 completion

**Recommendation**:
- Defer to Phase 1 (proper attention when foundation is solid)
- Add to FLOWSTATE.md § Deferred Items

Or, if 2FA is critical:
- Replace current scope (OAuth + 2FA from start)
- Reset timeline (+1-2 weeks)

Your preference?
```

---

#### Balanced Response

```
2FA should be deferred (not in Phase 0 scope).

Current: Basic auth (login/signup/sessions)
2FA: Adds complexity (SMS/TOTP, schema, recovery), delays Phase 0

Recommendation: Add to FLOWSTATE.md § Deferred Items (Phase 1)

Or replace scope if critical (adds 1-2 weeks)?
```

---

#### Expert Response

```
[2FA → Defer to Phase 1 (not in Phase 0 scope)]
[Add to Deferred Items or replace scope?]
```

---

### Summary: Key Differences Across Levels

**Learner Mode**:
- Explains WHY (orchestration reasoning)
- Teaches patterns (stage gates, meta-rules)
- High verbosity (3-5x baseline)
- Patient, pedagogical tone

**Growth Mode**:
- Explains key decisions
- Mentions meta-rules briefly
- Medium verbosity (2x baseline)
- Collaborative tone

**Balanced Mode**:
- Minimal explanations (only when needed)
- Brief meta-rule mentions
- Baseline verbosity
- Professional tone

**Expert Mode**:
- No explanations (action-focused)
- No meta-rule mentions (unless unusual)
- Minimal verbosity (0.5x baseline)
- Terse tone

---

**For AI**: These templates are guidelines, not scripts. Adapt to context, but maintain the verbosity and teaching level appropriate to the user's scaffolding setting.

**For Users**: If responses don't match your expected scaffolding level, say "Check your scaffolding level" to remind AI to verify FLOWSTATE.md configuration.

---

## 📞 Support

**For questions about templates:**
- Email: abe@flowstateai.dev
- Discord: https://discord.gg/FWx5swdCMK

---

**Version**: 2.5.0
**Last Updated**: 2025-11-24
**Framework Created By**: Abe Burnett, Mythgate
