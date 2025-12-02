# FlowState SE - Complete Reference
## Detailed Meta-Rules, Protocols, and Agent Identities

**Version**: 2.5.0
**Last Updated**: 2025-11-24

**🔄 v2.4+**: Quality Mode System + Execution Loop Contract (Meta-Rule 14) + Proceed Commands - see CHANGELOG.md for complete details

**🆘 v2.3.1+**: Emergency Recovery & Diagnostics (enhanced with `FlowState verify` in v2.5) - see [TROUBLESHOOTING.md](TROUBLESHOOTING.md) for complete details

**🎓 NEW in v2.3**: Scaffolding Levels (learn to vibe code) + Git Privacy features - see CHANGELOG.md for complete details

---

## 📖 Document Purpose

This is the **complete reference** for FlowState AI Framework SE v2.5.

**When to use this:**
- Deep dive into any Meta-Rule
- Understand agent identity protocols
- Troubleshoot complex issues
- Customize framework for your needs

**For quick answers**, see [QUICKSTART.md](QUICKSTART.md).

---

## Table of Contents

1. [The 14 Meta-Rules (Detailed)](#the-14-meta-rules-detailed)
2. [Quality Mode System (Complete Guide)](#quality-mode-system-complete-guide)
3. [Proceed Commands (Workflows & Case Studies)](#proceed-commands-workflows--case-studies)
4. [Agent Identity System (Complete Protocols)](#agent-identity-system-complete-protocols)
5. [Session Management Protocols](#session-management-protocols)
6. [Plans System (Full Lifecycle)](#plans-system-full-lifecycle)
7. [Refactor Cycle Procedures](#refactor-cycle-procedures)
8. [Bug Hunt Procedures](#bug-hunt-procedures)
9. [Platform Deep Dives](#platform-deep-dives)
10. [Troubleshooting Guide](#troubleshooting-guide)
11. [FAQ](#faq)

---

## The 14 Meta-Rules (Detailed)

### Philosophy

Rules are **principles, not prescriptions**. AI adapts them to context (language, framework, domain).

**Example**: File size cap (Meta-Rule 8) adapts based on language:
- TypeScript/JavaScript: 400 LOC (terse, expressive)
- Swift/Java/C++: 600 LOC (ceremony overhead)
- Python/Ruby/Go: 300 LOC (extremely terse)

---

### Meta-Rule 1: Phase Boundaries Are Sacred

**Principle**: Never mix future-phase work into current phase (prevents scope creep)

**Default**: No Phase N+1 work until Phase N acceptance criteria met

**AI Adaptation Guidance**:
- Detect current phase from `.flowstate/config.md`
- Block suggestions for deferred features
- When user requests out-of-phase work, remind of Meta-Rule 1 and offer to defer

**Example**:
```
User: "Add multi-tenant support" (Phase 1 feature)

AI: "Multi-tenant support is Phase 1 (current: Phase 0).

     Options:
     A) Defer to Phase 1 (recommended - stays disciplined)
     B) Descope Phase 0 (remove something to make room)
     C) Override (skip phase discipline - not recommended)

     Which do you prefer?"
```

**Enforcement**:
- `.flowstate/config.md` tracks current phase
- `.flowstate/tasks.md` has phase labels for each task
- `.flowstate/session.md` shows deferred items with phase assignment
- Phase transition requires ALL acceptance criteria met

**Benefits**:
- Prevents scope creep (most common project failure mode)
- Enables predictable delivery (you know when Phase 0 is done)
- Reduces context switching (finish current work before starting next)

---

### Meta-Rule 2: Work → Right → Fast (Progressive Refinement)

**Principle**: Build in stages—functional first, quality second, performance third

**Default**: Work (make it function) → Right (make it clean) → Fast (make it performant)

**AI Adaptation Guidance**:
- **Web/API projects**: Work = tests pass, Right = types + DRY, Fast = caching/optimization
- **Mobile projects**: Work = prototype, Right = polish UX, Fast = optimize battery/memory
- **Data Science**: Work = explore data, Right = model training, Fast = deploy/monitor
- **CLI tools**: Work = happy path, Right = error handling, Fast = startup time

**Context Detection**: Check project type during initialization, adapt stage names

**Example (iOS Project)**:
```
Stages: Prototype → Polish → Optimize
- Prototype: UI mockup, basic functionality
- Polish: Design system, animations, accessibility
- Optimize: Battery usage, memory, app size
```

**Commit Tagging**:
```bash
git commit -m "feat(auth): Clerk middleware integration [Work]"
git commit -m "refactor(auth): Extract session validator [Right]"
git commit -m "perf(auth): Cache user entitlements [Fast]"
```

**Why Three Stages?**
- **Work first**: Get feedback early (does this solve the problem?)
- **Right second**: Maintainability matters (you'll edit this code 10x)
- **Fast last**: Optimize what matters (premature optimization wastes time)

---

### Meta-Rule 3: One Task In-Progress Per Owner

**Principle**: Limit work-in-progress to prevent context switching

**Default**: Max 1 task in In-Progress column per owner

**AI Adaptation Guidance**:
- Solo developer: Strict (1 task only)
- Pair programming: Allow 1 task per pair
- Emergency: Suspend rule, document in `.flowstate/session.md` ("Key Decisions & Context" section)

**Exception**: If task blocked >24 hours, start next priority (mark original as Blocked)

**Why**: Context switching kills quality; serial completion builds momentum

**Enforcement**:
- `.flowstate/tasks.md` shows In-Progress section
- AI warns if >1 task in progress
- TodoWrite (Claude Code) enforces 1 active task

**Benefits**:
- Finish faster (serial completion > parallel confusion)
- Better quality (deep focus > shallow multitasking)
- Clear accountability (everyone knows what you're working on)

---

### Meta-Rule 4: Keep It Simple (Delete Before Abstracting)

**Principle**: Prefer deletion over abstraction; solve problems by removing code

**Default**: Before adding abstraction, ask "Can I delete duplicate code instead?"

**AI Adaptation Guidance**:
- When detecting duplication: Suggest deletion first, abstraction second
- When user requests "utility function": Ask if callers can be simplified instead
- When refactoring: Measure before/after LOC (goal: net negative)

**Example**:
```
User: "Extract common validation logic to utility"

AI: "I see 3 instances of email validation. Options:

     A) Delete 2 instances, keep simplest one (recommended)
        - auth/signup.ts: Has regex + domain check
        - profile/update.ts: Has regex only
        - invite/send.ts: Has regex only
        → Keep signup.ts version, delete others, import from there
        Net: -15 LOC

     B) Extract to shared validator
        → Create validators/email.ts
        Net: +8 LOC (new file overhead)

     Which do you prefer? (I recommend A)"
```

**Simplification Checklist**:
- [ ] Can I delete duplicates instead of extracting?
- [ ] Can I use built-in library instead of custom code?
- [ ] Can I remove a feature instead of making it configurable?

**Benefits**:
- Less code = less bugs
- Less code = faster onboarding
- Less code = easier maintenance

---

### Meta-Rule 5: Ask "Why This Approach?"

**Principle**: Every task needs documented rationale for future context

**Default**: Capture one-sentence "why" when task created or completed

**AI Responsibility**: When adding task to `.flowstate/tasks.md` or creating plan:
- Ask user "Why this approach vs alternatives?"
- Document answer in task notes and plan file

**User Responsibility**: Provide rationale (AI will prompt if missing)

**Example in `.flowstate/tasks.md`**:
```markdown
- [x] Implement user authentication with Clerk — Done: 2025-10-26
  Why this approach? Clerk provides hosted auth flows, eliminating custom JWT
  management and reducing security surface area. Faster to MVP than Auth0 ($0 free tier).

  Alternative considered: NextAuth.js (rejected: requires more custom code for providers)
```

**Benefits**:
- 6 months later: "Why did we use Clerk?" → Check `.flowstate/tasks.md`
- New team member: Understands decisions instantly
- Prevents revisiting settled debates

---

### Meta-Rule 6: Leave Breadcrumbs (Evidence Trail)

**Principle**: Prove work was done; memory fails, logs don't

**Default**: Attach evidence when moving task to Testing or Done

**AI Responsibility**: Automatically capture evidence
- Run tests → save output to `logs/[feature]_YYYY-MM-DD_HHMM.log`
- Update `.flowstate/tasks.md` with evidence link
- Update `.flowstate/session.md` with completion details
- Tag git state with rollback point

**User Responsibility**: None (AI handles this)

**AI Adaptation Guidance**:
- **Web projects**: Test output, build logs, API responses
- **Mobile projects**: Screenshots, video recordings, crash logs
- **Data Science**: MLflow run IDs, model metrics, confusion matrices
- **CLI tools**: Command output, performance benchmarks

**Log Naming Convention**:
```
logs/[category]_[YYYY-MM-DD]_[HHMM].log
```

**Categories**:
- `auth_implementation` — Auth feature work
- `api_test` — Backend test runs
- `web_test` — Frontend test runs
- `refactor_cycle` — Refactor findings and actions
- `bug_hunt` — Bug sweep results
- `deployment` — Deploy logs and smoke tests

**Example Evidence Log**:
```
logs/auth_implementation_2025-10-26_1430.log
───────────────────────────────────────────────
Feature: User authentication with Clerk
Started: 2025-10-26 14:30
Completed: 2025-10-26 16:15
Duration: 1h 45min

Tests Run:
✅ auth/signup.test.ts (12 tests, all passing)
✅ auth/login.test.ts (8 tests, all passing)
✅ auth/session.test.ts (6 tests, all passing)

Coverage:
- auth/clerk-provider.ts: 95%
- auth/middleware.ts: 88%
- auth/session-utils.ts: 100%

Git Tags:
- auth-work-before (rollback point)
- auth-work-after (validated state)

Validation Command:
pnpm test auth

Outcome: All acceptance criteria met ✅
───────────────────────────────────────────────
```

---

### Meta-Rule 7: Stage Work Visibly

**Principle**: Label all work with current stage so reviewers understand intent

**Default**: Tag commits with [Work], [Right], [Fast]

**AI Responsibility**: Automatically tag commits with stage

**Example**:
```
git commit -m "feat(auth): Implement Clerk integration [Work]"
git commit -m "refactor(auth): Extract session validator [Right]"
git commit -m "perf(auth): Cache user entitlements [Fast]"
```

**AI Adaptation Guidance**: Adapt stage labels to context (see Meta-Rule 2)

**Benefits**:
- Reviewers know intent (is this done or in progress?)
- History is scannable (see progression from Work → Right → Fast)
- Sets expectations (Work = functionality, Right = quality, Fast = performance)

---

### Meta-Rule 8: Small & Focused Files (Comprehension Limit)

**Principle**: Files should be understandable in <15 minutes

**Default**: ≤400 LOC hard cap

**AI Adaptation Guidance**:
- **Verbose languages** (Swift, Java, C++): Cap = 600 LOC (ceremony overhead)
- **Terse languages** (Python, Ruby, Go): Cap = 300 LOC (extremely concise)
- **Config files**: Exempt (document exception in `.flowstate/config.md`)
- **Generated code**: Exempt (note in `.flowstate/config.md`)

**Context Detection**: Detect language during initialization, set appropriate cap

**Example (Swift Project)**:
```
AI during initialization:
"Detected Swift/iOS project. Setting file size cap to 600 LOC
 (Swift protocols/extensions add ~40% ceremony vs TypeScript)"
```

**Verification Commands**:
```bash
# TypeScript/JavaScript (400 LOC cap)
find src -name "*.ts" -o -name "*.tsx" -o -name "*.js" -exec wc -l {} + | awk '$1 > 400'

# Swift (600 LOC cap)
find . -name "*.swift" -exec wc -l {} + | awk '$1 > 600'

# Python (300 LOC cap)
find . -name "*.py" -exec wc -l {} + | awk '$1 > 300'
```

**Proactive Warning**:
When file reaches 90% of cap (e.g., 350 LOC for 400 cap), AI proactively suggests split

**Example**:
```
AI: "Notice: auth-middleware.ts is now 365 LOC (approaching 400 cap).

     Suggested split:
     - auth-middleware.ts (core middleware, ~180 LOC)
     - session-validators.ts (validation logic, ~120 LOC)
     - types.ts (TypeScript types, ~65 LOC)

     Refactor now or defer to next cycle?"
```

---

### Meta-Rule 9: Commit Discipline (Git Safety)

**Principle**: Always have rollback plan before risky changes

**Default**: Tag git state before major work

**AI Responsibility**: Before risky work (refactors, major features, dependency upgrades):
```bash
git tag -a feature-[name]-before -m "Safe rollback point"
```

After validation passes:
```bash
git tag -a feature-[name]-after -m "Validated: [outcome]"
```

**User Responsibility**: Approve risky changes when AI flags them

**Rollback Procedure**:
```bash
git checkout [feature]-before
# OR
git reset --hard [feature]-before
# Verify
[validation command]
```

**List All Safety Tags**:
```bash
git tag --list '*-before'
git tag --list '*-after'
```

**Benefits**:
- Can undo ANY change in <30 seconds
- Confidence to try risky refactors
- Production incident recovery (rollback to last-known-good)

---

### Meta-Rule 10: Refactor Discipline (Proactive Debt Management)

**Principle**: Pay down complexity debt before it compounds

**Default Triggers**:
- Every 5 completed tasks
- Any file >90% of size cap
- Duplicate code across 3+ files

**AI Responsibility**: Proactively detect triggers and propose refactors
- Scan codebase at task completion
- When trigger hit, create refactor proposal
- Wait for user approval before implementing

**Example**:
```
AI: "Refactor cycle triggered (5 tasks complete).

     Scanning codebase...

     Found violations:
     - 2 files >90% of cap (365 LOC, 370 LOC)
     - 1 duplicate pattern (validation logic 4x)
     - 0 functions >50 lines

     Top 3 improvements (ranked by impact/effort):

     1. websocket-client.ts (385 LOC) → Split into 3 files
        Effort: 45 min | Risk: Low | Impact: High
        Reason: Blocking 2 future features (file too complex to extend)

     2. Validation logic duplicated 4x → Extract to validators.ts
        Effort: 20 min | Risk: Low | Impact: Medium (saves 95 LOC)

     3. user-service.ts (370 LOC) → Extract user-repository.ts
        Effort: 30 min | Risk: Low | Impact: Medium (separation of concerns)

     Proceed with all 3, select subset, or defer?"
```

**Refactor Checklist**:
- [ ] Files >90% of cap identified and split plan created
- [ ] Functions >50 lines broken into smaller units
- [ ] Duplicate code (3+ instances) extracted to shared utilities
- [ ] Import sprawl consolidated (>10 imports)
- [ ] Tests updated and passing

**Evidence**: `logs/refactor_cycle_YYYY-MM-DD_HHMM.log` with before/after metrics

---

### Meta-Rule 11: Subscription Context (Feature Gating)

**Principle**: Build complete features, activate selectively by tier

**Default**: Note which tier gates feature in DoD

**AI Responsibility**: When implementing gated feature:
- Add entitlement check to backend
- Add upgrade prompt to frontend
- Document tier requirement in `.flowstate/tasks.md`

**Example DoD**:
```
DoD: Advanced agents feature gated behind Pro tier;
     Free users see upgrade CTA; API returns 402 when disabled.
```

**Implementation Pattern**:

**Backend Guard**:
```typescript
// Middleware injection
app.use(entitlementsMiddleware);

// Route guard
router.post('/api/advanced', async (req, res) => {
  if (!req.entitlements.canAccess('advanced-features')) {
    return res.status(402).json({
      error: 'upgrade_required',
      tier: 'pro',
      feature: 'advanced-features',
      upgradeUrl: '/upgrade?feature=advanced-features',
    });
  }
  // Feature logic
});
```

**Frontend Enhancement**:
```tsx
const { canAccess } = useEntitlements();

return (
  <>
    {canAccess('advanced-features') ? (
      <AdvancedPanel />
    ) : (
      <UpgradePrompt
        feature="advanced-features"
        tier="pro"
        benefits={['Unlock advanced AI', '10x higher limits', 'Priority support']}
      />
    )}
  </>
);
```

---

### Meta-Rule 12: Entitlement Testing (Both States)

**Principle**: Test features in enabled AND disabled states

**Default**: Every gated feature needs 2 test suites

**AI Responsibility**: Generate tests for both states:
```typescript
describe('Feature (Enabled)', () => {
  it('returns advanced data', async () => {
    const user = await createProUser();
    const res = await request(app)
      .post('/api/advanced')
      .set('Authorization', `Bearer ${user.token}`);
    expect(res.status).toBe(200);
  });
});

describe('Feature (Disabled)', () => {
  it('returns 402 with upgrade metadata', async () => {
    const user = await createFreeUser();
    const res = await request(app)
      .post('/api/advanced')
      .set('Authorization', `Bearer ${user.token}`);
    expect(res.status).toBe(402);
    expect(res.body.error).toBe('upgrade_required');
  });

  it('shows upgrade prompt in UI', async () => {
    const { getByText } = render(<AdvancedFeaturePage />, {
      user: { tier: 'free' }
    });
    expect(getByText(/upgrade to pro/i)).toBeInTheDocument();
  });
});
```

---

### Meta-Rule 13: Comprehension Debt Management

**Principle**: Code optimized for human understanding first, machine execution second

**Target**: <15 minutes to understand any module's purpose, dependencies, failure modes

**Triggers**: Phase transitions, files >90% of cap, test confusion, onboarding friction

**Metrics**:
- Time to Context: <15 min per module
- File Size: ≤cap (context-adapted)
- Layer Count: ≤3 hops for user-facing paths
- Duplication: Zero across ≥3 modules
- Test Discoverability: <2 greps to find test

**AI Responsibility**: Proactively flag comprehension debt and suggest fixes

**Example**:
```
AI: "Comprehension debt detected in auth module:

     Issues:
     1. auth-middleware.ts: 385 LOC (>15 min to understand)
     2. Session types spread across 4 files (hard to trace)
     3. Tests for auth-middleware not in tests/auth/ (discoverability)

     Suggestions:
     1. Split auth-middleware into focused modules
     2. Consolidate types into auth/types.ts
     3. Move tests to tests/auth/middleware.test.ts

     Implement now or add to next refactor cycle?"
```

---

### Meta-Rule 14: Execution Loop Contract [NEW in v2.4]

**Principle**: Every work response must end with structured navigation (solves "AI stopped without guidance")

**Purpose**: Provides persistent task visibility, clear next steps, and copy-paste commands for continuation

**Structure**: 5-part format at end of every response where work was performed

---

#### The 5-Part Structure

**1. COMPLETED** (1-2 sentences)
- What was just finished
- Outcome or status

**2. ACTIVE STATE** (3-7 items, visual format)
- Current task list with priorities and progress
- P0/P1/P2 priority labels
- ✅/🔄/⏸️ status indicators
- Visual arrows showing current position

**3. NEXT RECOMMENDED** (1-3 actions, prioritized)
- What should happen next (in priority order)
- Brief rationale for sequencing
- Any dependencies or prerequisites

**4. PROCEED WITH** (copy-paste commands)
- `proceed` → Current task only
- `proceed next` → Current + next 1 task
- `proceed all` → All P0 tasks (check-ins every 3)
- `ultrathink` → Force Methodical mode for current task
- `pause` → Stop and wait for instruction

**5. NOTES** (optional)
- Warnings or blockers
- Phase progress updates
- Important decisions made
- Quality mode reminders

---

#### Complete Example

```markdown
## ✅ COMPLETED:
Implemented JWT authentication middleware with TypeScript types. Tests passing (12/12).

## 🎯 ACTIVE STATE:
┌─────────────────────────────────────────────┐
│ Phase 0: MVP Authentication System          │
│ Progress: 3 of 7 tasks complete (43%)      │
└─────────────────────────────────────────────┘

  ✅ P0 Task 1: Set up Clerk SDK integration
  ✅ P0 Task 2: Create auth middleware
  ✅ P0 Task 3: Add JWT validation logic
  🔄 P0 Task 4: Implement protected routes ← YOU ARE HERE
  ⏳ P0 Task 5: Add error handling for auth failures
  ⏳ P0 Task 6: Write integration tests
  ⏳ P1 Task 7: Add refresh token rotation (deferred)

## 🎯 NEXT RECOMMENDED:
1. **Complete Task 4** (protected routes) → Unblocks frontend integration
2. **Then Task 5** (error handling) → Critical for production
3. **Then Task 6** (integration tests) → Validation before deploy

## PROCEED WITH:
- `proceed` → Complete Task 4 only, check in
- `proceed next` → Complete Tasks 4-5, check in
- `proceed all` → Complete all P0 tasks (check-ins every 3)
- `ultrathink Task 6` → Force Methodical mode for test coverage
- `pause` → Stop and wait for instruction

## 📝 NOTES:
⚠️  Task 5 error handling is critical—recommend reviewing security patterns before implementing.
Phase Progress: 43% complete, on track for Phase 0 gate (target: 5 more days).
```

---

#### Quality Mode Interaction

Execution Loop **structure** remains identical across quality modes. **Content depth** varies:

**Fast Mode:**
- COMPLETED: Terse (1 sentence)
- ACTIVE STATE: Standard 3-7 items
- NEXT RECOMMENDED: Brief rationale
- PROCEED WITH: Standard commands
- NOTES: Minimal or omitted

**Balanced Mode:**
- COMPLETED: Clear statement (1-2 sentences)
- ACTIVE STATE: Standard 3-7 items with context
- NEXT RECOMMENDED: Moderate rationale
- PROCEED WITH: Standard commands
- NOTES: Occasional important items

**Methodical Mode:**
- COMPLETED: Detailed outcome (2 sentences + key findings)
- ACTIVE STATE: Comprehensive 5-7 items with dependencies
- NEXT RECOMMENDED: Detailed rationale with alternatives considered
- PROCEED WITH: Standard commands + ultrathink suggestions
- NOTES: Comprehensive (warnings, decisions, phase progress, quality checkpoints)

---

#### Scaffolding Interaction

Execution Loop **content** remains identical. **Explanation before loop** varies:

**Learner Scaffolding:**
- Extensive explanation of work performed (teaching mode)
- Commentary on patterns used, why chosen
- Meta-rule mentions with reasoning
- **Then** Execution Loop appears (standard format)

**Expert Scaffolding:**
- Minimal work summary (action-focused)
- No teaching commentary
- Terse outcome statement
- **Then** Execution Loop appears (standard format)

**Key Insight**: Execution Loop = navigation structure (always present). Scaffolding/Quality control what happens *before* the loop.

---

#### When to Include Execution Loop

**ALWAYS include when:**
- ✅ AI performed work this response (wrote code, updated files, ran commands)
- ✅ User has explicit tasks in `.flowstate/tasks.md` (3+ tasks)
- ✅ Work is part of multi-step process (not one-off question)

**NEVER include when:**
- ❌ Pure Q&A (no work performed)
- ❌ Single standalone task completed (nothing next)
- ❌ User explicitly asked for explanation only

---

#### AI Enforcement Checklist

Before sending response, validate:

```python
if work_was_done_this_response():
    assert has_execution_loop_at_end()
    assert execution_loop_has_all_5_sections() or has_4_sections_notes_optional()
    assert active_state_shows_3_to_7_items()
    assert active_state_synced_with_tasks_md()
    assert proceed_commands_present_and_copy_paste_ready()
    assert visual_formatting_preserved()  # boxes, arrows, emoji
```

---

#### Common Mistakes (AVOID)

❌ **Mistake 1**: Including loop for every response
- **Fix**: Only include when work was performed

❌ **Mistake 2**: ACTIVE STATE out of sync with `.flowstate/tasks.md`
- **Fix**: Always read `.flowstate/tasks.md` before constructing loop

❌ **Mistake 3**: NEXT RECOMMENDED doesn't prioritize
- **Fix**: Put highest priority first, explain dependencies

❌ **Mistake 4**: Missing proceed commands
- **Fix**: Always include all 5 command variants

❌ **Mistake 5**: Breaking visual formatting
- **Fix**: Use exact format (boxes, arrows, emoji preserved)

---

#### User Benefits

**Solves**:
1. "AI stopped and I don't know what to say" → Proceed commands provide clear options
2. "Where's my task list?" → ACTIVE STATE shows persistent progress
3. "What should I do next?" → NEXT RECOMMENDED provides prioritized guidance
4. "Did that actually work?" → COMPLETED confirms outcome

**Result**: Frictionless continuation, no mental load to resume work

---

## Quality Mode System (Complete Guide)

### Overview

**Quality Mode** is an independent dimension from scaffolding that controls **work rigor**, not explanation verbosity.

**The Three Modes**:
1. **Fast** – Minimal ceremony, essential work only
2. **Balanced** – Standard rigor, selective validation (DEFAULT)
3. **Methodical** – Maximum thoroughness, comprehensive checks

**Key Principle**: Quality Mode and Scaffolding are **independent dimensions**:
- Scaffolding = **how much AI teaches you** (Learner/Growth/Balanced/Expert)
- Quality Mode = **how thoroughly AI validates work** (Fast/Balanced/Methodical)

Together they form **9 valid combinations** (e.g., Learner+Fast, Expert+Methodical).

---

### Fast Mode

**Purpose**: Rapid iteration, prototyping, quick feature delivery.

**When to Use**:
- ✅ Phase 0 exploration (proving feasibility)
- ✅ Throwaway prototypes and spikes
- ✅ Time‑sensitive demos or workshops
- ✅ Low‑risk experimental features
- ✅ Personal projects with high iteration velocity

**When NOT to Use**:
- ❌ Production‑critical systems
- ❌ Security‑sensitive features
- ❌ Complex architectural decisions
- ❌ Shared/team codebases requiring documentation

**Behavior in Fast Mode** (derived from framework Step 6.6):
- Documentation: `.flowstate/tasks.md` only (real‑time updates)
- Review checkpoints: None by default
- Git tagging: Major milestones only
- File size warnings: Trigger at **95%** of file size cap
- Refactor cycle: Every **5 tasks** (unchanged from baseline)
- Test coverage: **Happy path only**
- Execution Loop NOTES: Minimal; only critical warnings or blockers

**Example (Fast Mode)**:
- You are building a proof‑of‑concept feature branch.
- AI updates `.flowstate/tasks.md` as it goes, but defers exhaustive tests and docs.
- When the feature stabilizes, you can either:
  - Switch to **Balanced** to harden it, or
  - Use `ultrathink` on a specific high‑risk task.

---

### Balanced Mode (DEFAULT)

**Purpose**: Default, production‑ready behavior with standard rigor and reasonable speed.

**When to Use**:
- ✅ Most SE projects (typical web/backend services)
- ✅ Features that will be merged to main after review
- ✅ Work where you want solid validation without slowing down

**When NOT to Use**:
- ❌ Extremely time‑boxed spikes where speed is everything → consider Fast
- ❌ Mission‑critical launches where you want exhaustive proof → consider Methodical

**Behavior in Balanced Mode**:
- Documentation: `.flowstate/tasks.md` in real time, `.flowstate/session.md` at session close
- Review checkpoints: At **stage transitions** (e.g., Explore → Prove → Ship)
- Git tagging: Before risky changes and after validation
- File size warnings: Trigger at **90%** of file size cap
- Refactor cycle: Every **5 tasks**
- Test coverage: Happy path **plus critical edge cases**
- Execution Loop NOTES: Standard detail (what changed, key decisions, open risks)

**Example (Balanced Mode)**:
- You are implementing a new API endpoint.
- AI writes code, adds tests for success + main failure cases, and updates docs.
- Execution Loop shows what was done, what’s next, and proceed commands so you can continue.

---

### Methodical Mode

**Purpose**: Maximum thoroughness for high‑risk work; trades speed for reliability.

**When to Use**:
- ✅ Production‑critical systems (auth, billing, security)
- ✅ High‑risk migrations (database, infrastructure)
- ✅ Complex refactors with many callers
- ✅ Teaching/learning best practices in depth

**When NOT to Use**:
- ❌ Trivial tasks with obvious outcomes
- ❌ Early‑stage spikes where requirements are still unknown

**Behavior in Methodical Mode**:
- Documentation: `.flowstate/tasks.md` + `.flowstate/session.md` at **task completion**, plus drift detection notes
- Review checkpoints: Before marking Done, before stage transitions, and every **3 tasks** during `proceed all`
- Git tagging: Before **every** risky change with detailed annotations
- File size warnings: Trigger at **85%** of file size cap (proactive)
- Refactor cycle: Every **5 tasks** **plus** proactive suggestions when duplication is detected
- Test coverage: Happy path + edge cases + error handling; prefers adding tests before risky edits
- Execution Loop NOTES: Comprehensive, with warnings, assumptions, and trade‑offs called out explicitly

**Example (Methodical Mode)**:
- You are changing authentication/authorization logic.
- AI proposes a plan, adds tests for success/failure/edge cases, updates docs, and surfaces rollback plans.
- Before marking the task Done, AI performs a final review checkpoint and summarizes risks in NOTES.

---

### Quality Mode × Scaffolding Matrix

Use this matrix as a mental model for how **teaching** (scaffolding) and **work rigor** (quality) combine:

- **Learner + Fast**: High explanation, minimal ceremony  
  - Great for learning patterns quickly on low‑risk work.
- **Learner + Balanced**: High explanation, standard rigor  
  - Good default for early‑stage users.
- **Learner + Methodical**: High explanation, maximum rigor  
  - Best for deep learning on critical systems.

- **Growth + Fast**: Targeted teaching, rapid work  
  - Helpful when you mostly know what you’re doing.
- **Growth + Balanced**: Targeted teaching, standard rigor (recommended for many SEs).
- **Growth + Methodical**: Targeted teaching, maximum rigor for tricky features.

- **Balanced + Fast**: Minimal teaching, rapid iteration.
- **Balanced + Balanced**: Minimal teaching, standard rigor (framework’s “classic” feel).
- **Expert + Methodical**: Terse responses, extremely thorough validation (power user mode).

**Key Insight**:  
Changing scaffolding does **not** change the amount of work; it changes *how* AI explains that work.  
Changing quality mode does **not** change teaching depth; it changes *how rigorously* the work is validated and documented.

---

### How to Change Quality Mode at Runtime

You can change quality mode at any time by saying:
- `Change quality mode to Fast`
- `Change quality mode to Balanced`
- `Change quality mode to Methodical`

When you do:
- AI updates the stored `quality_mode` in `.flowstate/config.md` (or equivalent config file).
- AI acknowledges the change in the next response and adapts behavior accordingly.

**Example A (switch to Fast temporarily)**:
- User: `Change quality mode to Fast`
- AI: "Got it — switching to **Fast** mode. I'll prioritize speed, keep updating `.flowstate/tasks.md`, and defer exhaustive checks until you request them."

**Example B (switch back to Methodical)**:
- User: `Change quality mode to Methodical`
- AI: “Understood — switching to **Methodical** mode. I’ll add review checkpoints, more exhaustive tests, and detailed NOTES in the Execution Loop.”

---

### Quality Mode and Execution Loop

Quality Mode affects *how much rigor* is expressed in the Execution Loop’s sections:

- **Fast**:
  - `COMPLETED`: Short, action‑focused summary.
  - `ACTIVE STATE`: Minimal annotations.
  - `NOTES`: Only critical blockers or warnings.

- **Balanced**:
  - `COMPLETED`: Standard detail on what changed and why.
  - `ACTIVE STATE`: Clear, well‑grouped tasks with priorities.
  - `NOTES`: Key caveats, trade‑offs, or follow‑ups.

- **Methodical**:
  - `COMPLETED`: Detailed description of work and validation steps.
  - `ACTIVE STATE`: Carefully maintained with explicit status and dependencies.
  - `NOTES`: Comprehensive risk analysis, assumptions, and next checks.

Execution Loop is still **always present** (when work was done this response); Quality Mode only changes its **depth**, not its structure.

---

## Proceed Commands (Workflows & Case Studies)

### Overview

Proceed commands provide structured continuation after AI completes work, solving the "what do I say next?" problem.

**The Five Commands**:
1. `proceed` - Execute current task only
2. `proceed next` - Execute current + next 1 task
3. `proceed all` - Execute all P0 tasks (check-ins every 3)
4. `ultrathink` - Force Methodical mode for current/specified task
5. `pause` - Stop automatic execution

The sections below summarize the full Proceed Commands specification from the framework, adapted for quick reference.

---

### Command Semantics

#### `proceed`
- **Scope**: Execute **current task only**.
- **When to Use**: You want to review after each task completes.
- **AI Behavior**:
  - Complete the current task in `ACTIVE STATE`.
  - Emit a fresh Execution Loop (Meta‑Rule 14).
  - Stop and wait for your next instruction.

#### `proceed next`
- **Scope**: Execute **current task + next 1** task.
- **When to Use**: Current task is straightforward and you want more momentum without giving up control.
- **AI Behavior**:
  - Complete the current task.
  - Immediately continue with the next task in `ACTIVE STATE`.
  - After both tasks are done, emit Execution Loop and wait.

#### `proceed all`
- **Scope**: Execute **all P0** tasks with periodic check‑ins.
- **When to Use**: All P0 tasks are clear and you want AI to run the full batch, while still keeping safety boundaries.
- **AI Behavior**:
  - Complete current task.
  - Continue automatically through remaining P0 tasks.
  - Emit Execution Loop **after every 3 tasks** as a check‑in.
  - If you do not respond at a check‑in, AI may continue up to the next check‑in.
  - Stop after all P0 tasks are complete.
- **Safety**: AI must stop early if:
  - A P0 blocker appears (e.g., missing dependency, failing tests).
  - Scope creeps (task requires new subtasks not present in `ACTIVE STATE`).
  - Context limits are reached.

#### `ultrathink [optional: task]`
- **Scope**: Force **Methodical** quality mode for the current or specified task.
- **When to Use**: Any high‑risk or high‑stakes task (database migrations, security changes, complex refactors).
- **AI Behavior**:
  - Temporarily override `quality_mode` to Methodical.
  - Execute the specified task (or current task if none specified).
  - Apply maximum rigor: comprehensive documentation, review checkpoints, exhaustive validation.
  - Restore the previous quality mode after the task completes.

#### `pause`
- **Scope**: Stop automatic execution and hand control back to you.
- **When to Use**: You want to intervene, change direction, or review before continuing.
- **AI Behavior**:
  - Finish the current atomic operation (e.g., current code edit).
  - Emit Execution Loop with updated state.
  - Stop and wait; do **not** auto‑continue until you say so.

---

### Integration with Execution Loop

Proceed Commands interact tightly with the Execution Loop Contract (Meta‑Rule 14):

- Every time AI executes work via a proceed command, it must:
  - Keep `ACTIVE STATE` synchronized with real tasks.
  - Update `COMPLETED` and `NOTES` based on actual changes.
  - Present all five commands in the `PROCEED WITH` section, ready for copy‑paste.

**Standard `PROCEED WITH` block**:
```markdown
## PROCEED WITH:
- `proceed` → Complete current task only, then check in
- `proceed next` → Complete current + next task, then check in
- `proceed all` → Complete all P0 tasks (check-ins every 3)
- `ultrathink` → Force Methodical mode for current task
- `pause` → Stop and wait for your instructions
```

---

### Quality Mode Interaction

Proceed Commands work **identically** at the control level across all quality modes, but the **execution characteristics** differ:

| Command       | Fast Mode                                      | Balanced Mode                                   | Methodical Mode                                           |
|--------------|-------------------------------------------------|------------------------------------------------|-----------------------------------------------------------|
| `proceed`    | Minimal ceremony, brief updates                 | Standard rigor, moderate updates               | Maximum thoroughness, comprehensive updates              |
| `proceed next` | Quick execution, terse check‑in              | Balanced pace, clear check‑in                  | Deliberate execution, detailed check‑in                  |
| `proceed all`  | Rapid batch; concise check‑ins every 3 tasks | Standard batch; clear check‑ins every 3 tasks  | Thorough batch; comprehensive check‑ins every 3 tasks    |
| `ultrathink` | Temporarily override to Methodical             | Temporarily override to Methodical             | Already Methodical (no change)                           |
| `pause`      | Stop immediately                               | Stop immediately                               | Stop immediately                                         |

---

### Scaffolding Interaction

Proceed Commands are also scaffolding‑aware: they do the **same work**, but explanation depth changes:

| Command        | Learner (3×)                                                | Growth (2×)                                | Balanced (1×)                           | Expert (0.5×)                    |
|----------------|-------------------------------------------------------------|--------------------------------------------|-----------------------------------------|----------------------------------|
| `proceed`      | Explains the task, why it matters, and what was done       | Explains task + main outcome               | States task + outcome                   | States outcome only              |
| `proceed next` | Explains both tasks in detail                               | Explains both tasks                        | States both tasks and that they’re done | Terse: “Tasks 1–2 complete.”     |
| `proceed all`  | Check‑ins include teaching context and rationale            | Check‑ins include concise rationale        | Check‑ins are clear but brief           | Check‑ins are minimal            |
| `ultrathink`   | Methodical rigor + rich teaching explanations (3× verbosity)| Methodical rigor + moderate explanations   | Methodical rigor + standard explanations| Methodical rigor + minimal text  |

**Key Insight**: Quality Mode controls **validation & documentation rigor**; scaffolding controls **how much teaching** appears around the same work.

---

### Suggested Usage Patterns (SE Examples)

**Pattern 1: Rapid iteration (Fast + `proceed next`)**
```text
User: Change quality mode to Fast
User: proceed next
AI: Completes 2 small implementation tasks quickly with minimal ceremony, then checks in.
```

**Pattern 2: Batch execution (Balanced + `proceed all`)**
```text
User: Change quality mode to Balanced
User: proceed all
AI: Executes all P0 tasks with check-ins every 3, keeping you informed via Execution Loop.
```

**Pattern 3: High‑stakes task (Fast + `ultrathink` override)**
```text
User: Quality mode is Fast for normal work
User: ultrathink database migration
AI: Switches to Methodical for the migration task only, performs exhaustive checks, then returns to Fast.
```

These patterns mirror the full Proceed Commands reference in the framework while keeping this REFERENCE section focused on practical SE workflows.

---

## Agent Identity System (Complete Protocols)

### Overview

FlowState uses **6 specialized agent identities** that AI embodies based on task context.

Each agent has:
- **Role & Expertise**: What they specialize in
- **Persona**: First-person narrative with experience level
- **Mindset**: How they approach problems
- **Red Flags**: What they watch for
- **Success Criteria**: What "done" looks like
- **Trigger Conditions**: When this agent activates

---

### Agent 1: Initialization Agent

**See [flowstate-ai-se-framework-v2.5.0.md](flowstate-ai-se-framework-v2.5.0.md) § Agent Identity System for full persona**

**Detailed Protocol**:

**Trigger**: User says "FlowState SE"

**Execution Steps**:
1. **Platform Detection** (5 sec)
   - Check for Claude Code tools (Read, Write, Edit, Bash, TodoWrite)
   - Check for .github/ directory (Copilot indicator)
   - Check for .cursor/ directory or .cursorrules
   - Check VS Code environment (Codex indicator)
   - Determine confidence level
   - If <70% confidence → Ask user which platform

2. **Read Framework Files** (10 sec)
   - Read flowstate-ai-se-framework-v2.5.0.md
   - Read QUICKSTART.md
   - Read TEMPLATES.md
   - Read REFERENCE.md

3. **Scan Project Context** (15 sec)
   - Detect languages (package.json, requirements.txt, etc.)
   - Detect frameworks (Next.js, Django, Rails, etc.)
   - Analyze directory structure
   - Check git history maturity
   - Check for existing FlowState files

4. **Ask Strategic Questions** (30-60 sec user interaction)
   - Project maturity (brand new / early / mature)
   - Phase 0 success metric
   - Deployment target
   - Subscription model
   - Immediate priority

5. **Adapt Meta-Rules** (5 sec)
   - Set file size cap based on language
   - Adapt Work → Right → Fast stages
   - Enable/disable subscription rules (11 & 12)

6. **Create Universal Files** (10 sec)
   - Generate `.flowstate/config.md` from template
   - Generate `.flowstate/tasks.md` from template
   - Generate `.flowstate/session.md` from template
   - Generate docs/[project]-master-plan.md
   - Create directories (docs/, plans/, logs/)

7. **Create Platform Adapters** (10 sec)
   - Create CLAUDE.md (if Claude Code)
   - Create AGENTS.md (if Copilot/Codex or uncertain)
   - Create .cursor/rules/flowstate.mdc (if Cursor or uncertain)
   - Create .cursorrules (if Cursor or uncertain)

8. **Git Initialization** (10 sec)
   - Add all FlowState files
   - Commit with detailed message
   - Tag: flowstate-se-init

9. **Verification** (5 sec)
   - Verify all files exist
   - Verify git state
   - Verify content quality

10. **Report Readiness** (User-facing)
    - Platform detected
    - Files created
    - Current state
    - Next 3 priorities
    - What to work on first

**Total Time**: ~75 seconds

---

### Agent 2: Execution Agent

**See [flowstate-ai-se-framework-v2.5.0.md](flowstate-ai-se-framework-v2.5.0.md) § Agent Identity System for full persona**

**Detailed Protocol**:

**Trigger**: User requests feature implementation, bug fix, or enhancement

**Execution Steps**:

**Phase 1: Context Loading**
1. Read `.flowstate/session.md` (restore context)
2. Read `.flowstate/tasks.md` (check current priorities)
3. Read `.flowstate/config.md` (verify phase, rules)
4. If plan exists for task → Read plan document

**Phase 2: Scope Validation**
1. Check current phase (Meta-Rule 1)
2. Identify if this is Phase N+1 work
3. If out-of-phase → Ask user to defer or descope
4. If in-phase → Proceed

**Phase 3: Complexity Assessment**
1. Determine if task needs plan (≥2 clarifying questions?)
2. If yes → Activate Planning Agent
3. If no → Proceed to implementation

**Phase 4: Implementation (Work Stage)**
1. Tag rollback point: `git tag [feature]-work-before`
2. Implement feature (tests passing, acceptance criteria met)
3. Follow file size discipline (Meta-Rule 8)
4. Update TodoWrite or `.flowstate/tasks.md` as you work

**Phase 5: Validation**
1. Run tests
2. Capture evidence in `logs/[feature]_YYYY-MM-DD_HHMM.log`
3. Verify all acceptance criteria met

**Phase 6: State Update**
1. Tag success: `git tag [feature]-work-after`
2. Update `.flowstate/tasks.md` (move to Testing/Done)
3. Update `.flowstate/session.md` (add to recent completions)

**Phase 7: Report**
1. Summarize what was done
2. Show evidence link
3. Suggest next task from `.flowstate/tasks.md`

**Red Flags (Auto-Warning)**:
- File approaching 90% of cap → Suggest split
- Tests not passing → Don't mark Done
- Phase N+1 work requested → Block and defer
- No rollback tag before risky change → Create tag first

---

### Agent 3: Planning Agent

**Full protocol in main document. Key additions:**

**When to Create a Plan**:
Use the **"One Question Rule"**:
- If you need to ask ≥2 clarifying questions → Create a plan
- If implementation is obvious → Skip plan (add rationale to `.flowstate/tasks.md`)

**Plan Quality Checklist**:
- [ ] Could another AI read this 6 months from now and implement correctly?
- [ ] Are all assumptions stated explicitly?
- [ ] Are risks identified with mitigations?
- [ ] Is user's vision accurately captured?

If any answer is "no" → Revise plan before delivering

---

### Agent 4: Refactor Agent

**Detailed Scanning Procedure**:

**Step 1: File Size Violations**
```bash
# Scan for files >90% of cap
find src -name "*.ts" -o -name "*.tsx" -exec wc -l {} + | awk '$1 > 350' | sort -rn
```

**Step 2: Duplicate Code Detection**
```
# Scan for duplicate blocks (3+ instances)
# Use AST analysis or pattern matching
# Flag: Same logic in 3+ files
```

**Step 3: Function Complexity**
```
# Scan for functions >50 lines
# Calculate cyclomatic complexity
# Flag: Complexity >10
```

**Step 4: Import Sprawl**
```
# Scan for files with >10 imports
# Suggest barrel exports or consolidation
```

**Step 5: Impact Analysis**
For each violation:
- Comprehension gain (1-10 scale)
- Effort estimate (minutes)
- Risk level (Low/Medium/High)
- Calculate impact/effort ratio
- Sort by ratio (highest first)

**Step 6: Proposal Generation**
Present top 3-5 improvements with:
- Current state (file size, duplication count)
- Proposed fix (split plan, extraction)
- Estimated effort
- Risk + mitigation
- Impact on comprehension

---

### Agent 5: Bug Hunt Agent

**Detailed Scanning Procedure**:

**Category 1: Logic & Edge Cases**
```typescript
// Scan for:
- Null/undefined access without checks
  Example: user.email (should be user?.email)

- Array access without bounds check
  Example: arr[index] (should check index < arr.length)

- Error propagation gaps
  Example: try/catch without re-throw or logging

- Async races
  Example: Promise.all without error handlers

- Off-by-one errors
  Example: for (i = 0; i <= arr.length; i++) (should be <)
```

**Category 2: Integration Issues**
```typescript
// Scan for:
- API mismatches (request/response shapes)
  Check: API client types match backend types

- State sync issues
  Check: Frontend state updates match backend reality

- Event leaks
  Check: All addEventListener have removeEventListener

- Lifecycle bugs
  Check: Mount/unmount, init/destroy pairs
```

**Category 3: Security & Validation**
```typescript
// Scan for:
- SQL injection vulnerabilities
  Check: Raw SQL queries with user input

- XSS vulnerabilities
  Check: Unsanitized HTML rendering

- Auth bypasses
  Check: Protected routes have auth middleware

- Data exposure
  Check: PII in logs, error messages, API responses
```

**Category 4: Performance & Resources**
```typescript
// Scan for:
- Memory leaks
  Check: Event listeners, intervals, subscriptions

- N+1 queries
  Check: Database queries in loops

- Unnecessary re-renders
  Check: React useEffect missing dependencies

- Blocking operations
  Check: Synchronous I/O on main thread
```

**Output Format**:
```
logs/bug_hunt_YYYY-MM-DD_HHMM.log
───────────────────────────────────
Bug Hunt Report

[P0] [Security] SQL Injection in user search
Location: api/users/search.ts:45
Reproduction: POST /api/users/search with query: "'; DROP TABLE users; --"
Impact: Database compromise
Proposed fix: Use parameterized query: db.query("SELECT * FROM users WHERE name = $1", [name])

[P1] [Logic] Null pointer in profile update
Location: pages/profile.tsx:123
Reproduction: Click "Update Profile" without avatar
Impact: Crash (user.avatar.url undefined)
Proposed fix: Optional chaining: user.avatar?.url || DEFAULT_AVATAR

[P2] [Performance] N+1 query in dashboard
Location: api/dashboard/projects.ts:78
Reproduction: Load dashboard with 10+ projects
Impact: 50+ DB queries (slow page load)
Proposed fix: Use include: { tasks: true } in Prisma query
───────────────────────────────────
```

---

### Agent 6: Session Manager Agent

**Detailed Protocol**:

**Session Close Procedure**:

**Step 1: Update `.flowstate/session.md`**
```markdown
# Calculate new values:
- Timestamp: current time
- Active work: Estimate % complete
- Recent completions: Add latest (keep last 3)
- Quality metrics: Re-scan files, update counts
- Session metadata: Duration, tasks completed
```

**Step 2: Generate Standup Summary**
```markdown
Stand-Up Summary for [Tomorrow]:

Yesterday ([Today]):
✅ [Task 1]
   - [Outcome in plain English]
   - Evidence: logs/[file].log

🏗️ In Progress: [Task] ([X]% complete)
   - [Status]
   - Next: [What's left]

Today ([Tomorrow]):
- [Next priority]
- [Secondary goal]

Blockers: [None / List with severity]

Notes:
- [Velocity, test coverage, files approaching limits]
```

**Step 3: Update `.flowstate/tasks.md`**
```markdown
# Move completed tasks from In-Progress → Done
# Add evidence links
# Update in-progress status
```

**Step 4: Git Commit** (if work done)
```bash
git add .flowstate/session.md .flowstate/tasks.md
git commit -m "FlowState: Update session state

Session summary:
- Completed: [N] tasks
- Active: [task name] ([X]% done)
- Quality: All files under cap, [N]/5 tasks to refactor trigger

[Auto-generated by FlowState Session Manager]"
```

**Step 5: Git Tag** (if milestone)
```bash
# Only if significant milestone (e.g., phase complete, major feature done)
git tag -a session-end-2025-10-26 -m "Session close: [N] tasks complete"
```

**Step 6: Report to User**
```
Session saved successfully.

✅ Today's completions: [List]
🏗️ In Progress: [Task] ([X]% done)
📋 Stand-up summary ready (copy below for tomorrow)

[Formatted standup summary]

Recommended goal for next session: [Suggested task]

See you tomorrow!
```

---

### Agent 7: Health Check & Diagnostic Agent [v2.3.1+, enhanced in v2.5]

**See [TROUBLESHOOTING.md](TROUBLESHOOTING.md) § 7-Phase AI Bootstrap Protocol for full implementation**

**Role**: Diagnose FlowState issues and restore framework functionality when AI loses awareness

**Trigger Conditions**:
1. User says: `FlowState status` (read-only health check)
2. User says: `FlowState doctor` (diagnostic + repair offers)
3. User says: `FlowState verify` (file existence verification) [NEW in v2.5]
4. User says: `Add FlowState to [platform]` (adapter installation)
5. User says any attach alias:
   - `Add FlowState`
   - `Register FlowState here`
   - `Connect this tool to FlowState`
   - `Install FlowState adapter here`
   - `Use FlowState`
6. **Emergency**: `Read TROUBLESHOOTING.md and follow its AI instructions to diagnose and restore FlowState SE framework functionality`

**Core Capabilities**:

**FlowState Status** (Quick Health Check):
1. Check framework presence (flowstate-ai-se-framework-v2.5.0.md exists?)
2. Check initialization state (`.flowstate/config.md` or legacy `FLOWSTATE.md` exists?)
3. Check platform adapters (CLAUDE.md, AGENTS.md, .cursor/rules/flowstate.mdc)
4. Check git repository state
5. Report: ✅ Healthy / ⚠️ Issues detected / 🆘 Not initialized

**FlowState Verify** (File Existence Verification) [NEW in v2.5]:
1. Verify each required FlowState file exists by reading it:
   - `.flowstate/config.md` (or `FLOWSTATE.md` in legacy mode)
   - `.flowstate/tasks.md` (or `TASKS.md` in legacy mode)
   - `.flowstate/session.md` (or `SESSION.md` in legacy mode)
   - `.flowstate/version.txt`
   - At least one platform adapter (CLAUDE.md, AGENTS.md, or .cursor/rules/flowstate.mdc)
2. For each file, READ it (not just check existence) to confirm content is valid
3. Report verification results in structured format:
   ```
   ✅ config.md — verified (read [N] lines, header present)
   ✅ tasks.md — verified (read [N] lines, header present)
   ✅ session.md — verified (read [N] lines, header present)
   ✅ version.txt — verified (contains "2.5.0")
   ✅ [ADAPTER].md — verified (read [N] lines, content present)

   All [5/5] required files verified.
   ```
4. If ANY file is missing:
   - Report: `❌ [filename] — MISSING`
   - Offer to create it: "Would you like me to create this file?"
   - If user approves → Create from template and re-verify

**Aliases**: `FS verify`, `Verify FlowState`, `Check FlowState files`

**When to Use**:
- After initialization if something seems wrong
- After switching AI platforms
- After a tool/IDE update
- If the AI seems to have "forgotten" FlowState

**FlowState Doctor** (Full Diagnostic):
1. Execute `FlowState status` checks
2. Scan for common issues:
   - Missing adapter files
   - Corrupted configuration
   - Wrong platform adapter for current environment
   - Missing directories (`.flowstate/archive/`, `.flowstate/plans/`, `.flowstate/logs/`)
   - Git state problems
3. Offer repairs (NEVER auto-fix):
   - "Would you like me to restore [missing file]?"
   - "Should I create the missing [directory]?"
   - "Shall I reinstall the adapter for [detected platform]?"
4. If user approves → Execute repair
5. Verify repair → Report success/failure

**Add / Attach FlowState to [Platform]**:
1. Validate target platform (Claude Code, Cursor, Copilot, Codex)
2. Check if adapter already exists
3. If exists → Warn "Already installed, overwrite?"
4. Read TEMPLATES.md for correct adapter template
5. Create adapter file with current project values
6. Verify installation
7. Report: "✅ FlowState adapter installed for [platform]"

For attach aliases (Add/Register/Connect/Install/Use without explicit
platform):
- Auto-detect current platform where possible
- If ambiguous, ask user which platform they mean
- Then behave exactly as `Add FlowState to [platform]`

**Emergency Recovery** (Zero-Awareness Bootstrap):
See [TROUBLESHOOTING.md](TROUBLESHOOTING.md) for complete 7-phase protocol that works even when AI has NO FlowState context.

**Preservation Guarantees**:
- **NEVER** overwrites `.flowstate/tasks.md`, `.flowstate/session.md`, or docs/* without explicit user approval
- **ALWAYS** preserves user data during recovery
- **ONLY** restores adapter files (CLAUDE.md, AGENTS.md, etc.) and missing directories
- Uses "Restore" terminology (not "Initialize") to avoid user fear of data loss

**Red Flags**:
- User data at risk → Abort and warn
- Multiple platforms detected → Ask which to prioritize
- Adapter file modified by user → Preserve changes, offer side-by-side comparison

**Success Criteria**:
- Framework responds to "FlowState SE" command
- Correct adapters installed for user's platform(s)
- All core files present and valid
- Git repository clean (or issues documented)
- User can resume work immediately

---

## Session Management Protocols

### Starting a Session

**Command**: `"Resume FlowState"` or `"FlowState SE"` (if continuing)

**AI Protocol**:
1. Read `.flowstate/session.md` (context restoration)
2. Read `.flowstate/tasks.md` (current priorities)
3. Read `.flowstate/config.md` (verify phase, rules)
4. Rebuild mental model:
   - Current phase and % complete
   - Active work and status
   - Recent completions
   - Quality metrics
5. Report readiness:
   - Acknowledge phase and state
   - Show active work
   - Suggest next steps
   - Ask what to work on

**User Experience**:
```
You: "Resume FlowState"

AI: "Reading .flowstate/session.md...

     Current state:
     - Phase 0: Foundation (35% complete)
     - Active: User authentication (60% done)
     - Last session: Implemented login/signup
     - Next: Add session management

     Ready to continue. Start with session management?"
```

---

### During a Session

**AI Behavior**:
- Continuously update TodoWrite (Claude Code) or internal state
- Sync with `.flowstate/tasks.md` at major milestones
- Warn proactively about:
  - Files approaching size caps
  - Phase boundary violations
  - Missing evidence
  - Refactor cycle triggers

**User Commands**:
- `"What's the current state?"` → `.flowstate/session.md` summary
- `"Show tasks"` → `.flowstate/tasks.md` listing
- `"What's next?"` → Top 3 priorities

---

### Closing a Session

**Command**: `"Done for today"` or `"Close session"`

**AI Protocol**: See Agent 6 (Session Manager) above

---

## Plans System (Full Lifecycle)

### When to Create a Plan

**The "One Question Rule"**:
- If AI needs ≥2 clarifying questions → Create a plan
- If implementation is obvious → Skip plan (add rationale to `.flowstate/tasks.md`)

**Example Triggering Questions**:
- "Which authentication provider? (Clerk / Auth0 / Custom)"
- "How should we handle data isolation? (Separate DBs / Row-level security)"
- "What's the upgrade flow from free to paid?"

If AI asks 2+ questions like these → Create plan

---

### Plan Document Structure

See TEMPLATES.md for full template. Key sections:

1. **Context & Rationale** (Why this feature?)
2. **Requirements** (Functional & non-functional)
3. **Architecture Decisions** (With rationale for each choice)
4. **Constraints & Assumptions** (Explicitly stated)
5. **Acceptance Criteria** (DoD checklist)
6. **Risks & Mitigations** (What could go wrong?)
7. **Implementation Plan** (Phases with timeline)
8. **Open Questions** (Unresolved items)

---

### Plan Lifecycle

**1. Creation** → AI asks questions, user answers, plan generated
**2. Reference** → AI reads plan before implementing
**3. Update** → User changes mind, plan is revised
**4. Completion** → All acceptance criteria met, plan archived

---

## Refactor Cycle Procedures

**See Agent 4 (Refactor Agent) above for detailed protocol**

**Quick Summary**:
- **Triggers**: Every 5 tasks, file >90% cap, duplicate code 3+
- **Process**: Scan → Analyze → Propose → Approve → Execute → Evidence
- **Output**: `logs/refactor_cycle_YYYY-MM-DD_HHMM.log`

---

## Bug Hunt Procedures

**See Agent 5 (Bug Hunt Agent) above for detailed protocol**

**Quick Summary**:
- **Triggers**: Weekly (Friday), phase transitions, major features
- **Categories**: Logic, Integration, Security, Performance
- **Output**: `logs/bug_hunt_YYYY-MM-DD_HHMM.log` with P0/P1/P2 severity
- **Action**: P0 bugs block phase advancement

---

## Platform Deep Dives

### Claude Code

**Native Files**: CLAUDE.md (auto-read at session start)

**Strengths**:
- TodoWrite tool (task management)
- Autonomous file operations
- Evidence capture
- Git automation

**Best For**: High-reliability features (auth, payments, critical paths)

**Integration**:
- CLAUDE.md references `.flowstate/config.md`, `.flowstate/tasks.md`, `.flowstate/session.md`
- TodoWrite syncs with `.flowstate/tasks.md`
- Session protocols automatic

---

### GitHub Copilot

**Native Files**: AGENTS.md (auto-read in Agent Mode)

**Strengths**:
- Autonomous multi-step tasks
- Self-healing (fixes errors automatically)
- PR submission
- GitHub integration

**Best For**: GitHub-centric workflows, async PR submissions

**Integration**:
- AGENTS.md references `.flowstate/config.md`, `.flowstate/tasks.md`, `.flowstate/session.md`
- Agent Mode iterates until tests pass
- PRs include evidence + updated `.flowstate/tasks.md`

---

### Cursor

**Native Files**: .cursor/rules/flowstate.mdc (with `alwaysApply: true`)

**Strengths**:
- User control (approve each change)
- .mdc frontmatter (glob patterns, auto-attach)
- Persistent rules

**Best For**: Learning, manual review, controlled environments

**Integration**:
- flowstate.mdc references `.flowstate/config.md`, `.flowstate/tasks.md`, `.flowstate/session.md`
- Rules auto-apply based on file patterns
- User approves proposals before execution

---

### OpenAI Codex

**Native Files**: AGENTS.md (co-developed standard)

**Strengths**:
- 7+ hour autonomous sessions
- @filename syntax (direct file reference)
- Internal to-do tracking
- GPT-5-Codex optimization

**Best For**: Complex multi-file features, long autonomous sessions

**Integration**:
- AGENTS.md references `.flowstate/config.md`, `.flowstate/tasks.md`, `.flowstate/session.md`
- @filename syntax: `@.flowstate/config.md`, `@.flowstate/tasks.md`
- Internal to-do syncs with `.flowstate/tasks.md`

---

## Troubleshooting Guide

**🆘 For comprehensive troubleshooting**, see **[TROUBLESHOOTING.md](TROUBLESHOOTING.md)** - includes emergency recovery, diagnostic commands, and platform-specific guides.

**Quick troubleshooting below** (for common historical issues):

---

### Issue: Platform Detection Failed

**Symptoms**: AI creates wrong adapter files or asks repeatedly

**Solution**:
```
You: "FlowState SE. I'm using [platform name]"

Example: "FlowState SE. I'm using Cursor"
```

**Or** (v2.5.0+):
```
You: "FlowState doctor"
AI: [Diagnoses platform mismatch, offers to install correct adapter]
```

---

### Issue: Files Not Created

**Symptoms**: Validation checklist shows missing files

**Solutions**:

1. **Use diagnostic command** (v2.5.0+):
   ```
   You: "FlowState doctor"
   AI: [Scans for missing files, offers to restore]
   ```

2. **Check permissions**:
   ```
   You: "Do you have permission to create files?"
   ```

3. **Force creation**:
   ```
   You: "Complete FlowState initialization"
   ```

4. **Manual creation** (last resort):
   - Copy templates from TEMPLATES.md
   - Fill in project-specific values

---

### Issue: FlowState Stopped Working After Tool Update

**Symptoms**: AI doesn't recognize "FlowState SE" command, adapter files seem broken

**Solution** (v2.5.0+):
```
You: "Read TROUBLESHOOTING.md and follow its AI instructions to diagnose and restore FlowState SE framework functionality"

AI: [Executes 7-Phase Bootstrap Protocol, restores framework awareness]
```

See [TROUBLESHOOTING.md § Scenario 1](TROUBLESHOOTING.md#scenario-1-flowstate-stopped-working-after-tool-update) for details.

---

### Issue: Wrong File Size Cap

**Symptoms**: AI warns at wrong threshold, caps don't match language

**Solution**:
```
You: "This is [language] code. Update file size cap to [X] LOC"

Example: "This is Swift code. Update file size cap to 600 LOC"

AI: "✅ Updated .flowstate/config.md: Cap → 600 LOC
     ✅ Updated proactive warning → 540 LOC (90%)"
```

---

### Issue: AI Violates Meta-Rules

**Symptoms**: File exceeds cap, no evidence provided, phase boundary violated

**Solution**:
```
You: "This violates Meta-Rule [N]. [Specific violation]"

Example: "This violates Meta-Rule 8. auth.ts is 485 LOC. Split this file."

AI: "You're correct. Splitting now..."
```

---

### Issue: Lost Context Mid-Session

**Symptoms**: AI forgets what you were working on

**Solution**:
```
You: "Rebuild context from session.md"

AI: "Reading .flowstate/session.md...
     Restored context:
     - Phase 0 (35% complete)
     - Working on user auth (60% done)
     - Last: Implemented login/signup
     - Next: Session management

     Ready to continue."
```

---

### Issue: Can't Find Evidence Log

**Symptoms**: Task marked Done but no log file

**Solution**:
```
You: "Where's the evidence for [feature]?"

AI: "Searching logs/...

     [If found:]
     Found: logs/[feature]_2025-10-26_1430.log

     [If not found:]
     Evidence log missing (violation of Meta-Rule 6).

     Recreating evidence:
     - Re-running tests...
     - Capturing output...
     - Saved: logs/[feature]_2025-10-26_1800.log"
```

---

### Issue: Task Stuck in Blocked

**Symptoms**: Task in Blocked for >24 hours, no progress

**Solution**:
```
You: "Unblock [task] or start next priority"

AI: "Task '[task]' blocked by [blocker].

     Options:
     A) Work on blocker first (add as new task)
     B) Start next priority (mark current as Blocked)
     C) Remove blocker and proceed (if resolved)

     Which do you prefer?"
```

---

## FAQ

### Q: Can I use FlowState with multiple AI platforms?

**A**: Yes! FlowState creates adapters for all platforms by default. You can use Cursor today, Claude Code tomorrow—both will work seamlessly because they read the same universal files (`.flowstate/config.md`, `.flowstate/tasks.md`, `.flowstate/session.md`).

---

### Q: What if I don't like one of the Meta-Rules?

**A**: You can customize Meta-Rules in `.flowstate/config.md`. However, we recommend trying the default rules for at least 2 weeks—they're based on patterns that prevent common project failures.

**To customize**:
```
You: "Disable Meta-Rule [N]" or "Change Meta-Rule [N] to [custom rule]"

AI: "Updated .flowstate/config.md with custom rule.
     Note: This may affect framework guarantees."
```

---

### Q: How do I migrate an existing project to FlowState?

**A**: See [CHANGELOG.md](CHANGELOG.md) § Migration Guide.

**Quick version**:
1. Say "FlowState SE"
2. Answer questions about existing project
3. AI scans codebase, adapts rules
4. Manual tasks:
   - Review `.flowstate/tasks.md` (ensure all active work is listed)
   - Update `.flowstate/session.md` (add current context)
   - Validate `.flowstate/config.md` (check phase and caps)

---

### Q: What if my project doesn't have phases?

**A**: FlowState is flexible. You can have a single "Production" phase or rename phases to match your workflow (e.g., "Alpha", "Beta", "Release"). The key is **phase boundaries**—don't mix future work into current work.

---

### Q: Can I use FlowState for non-web projects (CLI, mobile, data science)?

**A**: Yes! FlowState adapts to any software project. During initialization, AI detects your project type and adapts:
- **Mobile**: Work → Polish → Optimize (instead of Work → Right → Fast)
- **CLI**: Different file size caps, different evidence types
- **Data Science**: See FlowState DS edition (specialized for notebooks and experiments)

---

### Q: How much overhead does FlowState add?

**A**: Minimal in practice:
- **Initialization**: 2 minutes (one-time)
- **Session close**: 15 seconds (automated)
- **Session resume**: 10 seconds (read `.flowstate/session.md`)
- **Planning complex tasks**: 5 minutes (saves hours of rework)
- **Refactor cycles**: 30-60 minutes every 5 tasks (prevents weeks of debt paydown later)

**Net**: FlowState saves more time than it costs (prevents rework, reduces debugging, eliminates "why did we do this?" conversations).

---

### Q: Can I use FlowState solo or only with teams?

**A**: Both! FlowState works great for:
- **Solo developers**: Personal discipline, standup summaries for yourself, evidence for your future self
- **Teams**: Shared context, onboarding new members, handoffs between developers

---

### Q: What happens if I stop using FlowState mid-project?

**A**: Nothing breaks. FlowState files (`.flowstate/config.md`, `.flowstate/tasks.md`, `.flowstate/session.md`) are just markdown—you can read them without FlowState. To resume FlowState later, just say "Resume FlowState" and AI reloads context.

---

## Appendix F: Scaffolding Levels (v2.3+) [NEW]

### Overview

FlowState v2.3 introduces **scaffolding levels** to help users learn AI orchestration and architectural thinking. The system adjusts response verbosity without adding overhead or changing the quality of work.

**Key Principle**: Same work, different explanation depth

**Not About**: Coding skill, implementation details, algorithm choices
**About**: Orchestration patterns, architectural thinking, framework literacy

---

### The Four Scaffolding Levels

#### Level 1: Learner Mode

**Who It's For**: Bootcamp grads, career switchers, first time using AI assistants for real work

**Response Characteristics**:
- **Verbosity**: High (3-5x baseline)
- **Explanations**: Every orchestration decision explained in detail
- **Meta-Commentary**: Frequent "why I'm doing this" asides
- **Teaching Focus**: Orchestration patterns, prompt engineering, task decomposition, architectural thinking
- **Tone**: Patient, encouraging, pedagogical
- **Meta-Rules**: Explain which applies and WHY

**What Learner Mode Teaches** (Vibe Coding):
- ✅ "I'm breaking this into subtasks because..." (task decomposition)
- ✅ "I chose to search first, then read because..." (strategic sequencing)
- ✅ "This would violate Stage Boundaries (Meta-Rule 1), so I'll..." (architecture awareness)
- ✅ "The meta-rule says 'One Task In-Progress' which means..." (framework literacy)

**What Learner Mode Does NOT Teach** (Implementation):
- ❌ "This function uses a for loop because..." (coding details)
- ❌ "I'm using pandas.merge instead of SQL JOIN..." (tool choices)
- ❌ "The algorithm complexity is O(n log n)..." (CS theory)

**When to Use**:
- First week with FlowState
- Learning a new domain (switching from SE to DS work)
- Stuck on a complex orchestration pattern
- Want to understand architectural thinking deeply

**Estimated Response Length**: 300-500 words (vs 100-150 baseline)

---

#### Level 2: Growth Mode (DEFAULT)

**Who It's For**: Developers comfortable with AI basics, want to level up orchestration skills

**Response Characteristics**:
- **Verbosity**: Medium (2x baseline)
- **Explanations**: Key decisions explained, obvious steps omitted
- **Meta-Commentary**: Occasional "here's why" notes for strategic decisions
- **Teaching Focus**: Strategic thinking, meta-rule application, workflow patterns
- **Tone**: Collaborative, supportive, occasionally pedagogical
- **Meta-Rules**: Mention which applies (brief explanation)

**What Growth Mode Teaches**:
- ✅ "I'm using Search → Read → Edit sequence here" (pattern recognition)
- ✅ "This task should be atomic per Meta-Rule 3" (framework application)
- ✅ "I'll update `.flowstate/tasks.md` first to track this" (workflow habits)
- ✅ "We're approaching the Explore → Prove gate" (stage awareness)

**What to Skip**:
- Obvious FlowState workflows
- Implementation details
- Basic meta-rule explanations

**When to Use**:
- Default for most users (recommended starting point)
- After first week in Learner mode
- Want to learn while being productive
- Leveling up from junior to mid-level thinking

**Estimated Response Length**: 150-250 words (vs 100-150 baseline)

---

#### Level 3: Balanced Mode (Current FlowState Behavior)

**Who It's For**: Experienced developers, comfortable with AI orchestration

**Response Characteristics**:
- **Verbosity**: Baseline (current FlowState v2.2 behavior)
- **Explanations**: Only when necessary (complex decisions, non-obvious choices)
- **Meta-Commentary**: Rare, only for important strategic shifts
- **Teaching Focus**: None (assume user knows FlowState)
- **Tone**: Professional, concise, collaborative
- **Meta-Rules**: Mention only when relevant to current decision

**What to Include**:
- ✅ Clear statement of intent
- ✅ Brief summary of findings
- ✅ Stage-relevant context when it affects approach

**What to Omit**:
- Explanations of obvious FlowState workflows
- Teaching commentary on basic patterns
- Verbose summaries of routine actions

**When to Use**:
- Experienced with FlowState (1+ months)
- Comfortable with AI orchestration
- Don't need teaching, just collaboration
- Prefer current FlowState experience

**Estimated Response Length**: 100-150 words (baseline)

---

#### Level 4: Expert Mode

**Who It's For**: Power users, want maximum speed and minimal verbosity

**Response Characteristics**:
- **Verbosity**: Minimal (0.5x baseline)
- **Explanations**: Only for non-obvious strategic decisions that might surprise
- **Meta-Commentary**: Never
- **Teaching Focus**: None
- **Tone**: Terse, efficient, results-focused
- **Meta-Rules**: Mention only if intentionally violating one

**What to Include**:
- ✅ Action statements (no elaboration)
- ✅ Critical findings only
- ✅ Strategic pivots (when approach changes significantly)

**What to Omit**:
- Any explanation of routine workflows
- Summaries of obvious results
- Stage checks unless they change behavior

**When to Use**:
- Power user who knows FlowState deeply
- Time pressure (ship deadline approaching)
- Repetitive tasks (don't need teaching on same pattern again)
- Maximum speed mode

**Estimated Response Length**: 50-100 words (or less)

---

### Zero-Overhead Architecture

**How It Works**:
1. Scaffolding level stored in `.flowstate/config.md` (3 lines, ~30 tokens)
2. `.flowstate/config.md` already read at session start (no additional reads)
3. AI checks level before each response (no performance impact)
4. Response templates cached in AI working memory

**Performance Impact**: Zero (same work, different explanation depth)

**File Changes**: Only `.flowstate/config.md` (Scaffolding Configuration section)

---

### SE Edition Teaching Focus

**When in Learner or Growth mode**, AI focuses on these SE-specific orchestration patterns:

**API Design Orchestration**:
- RESTful principles (when to use POST vs PATCH, resource naming)
- Versioning strategies (when to version, how to deprecate)
- Error response patterns (4xx vs 5xx, error payload structure)

**Architecture Orchestration**:
- MVC vs microservices vs event-driven (when to use each)
- Separation of concerns (where boundaries should be)
- Dependency injection patterns (why and when)

**Refactoring Orchestration**:
- When to refactor (Meta-Rule 10: every 5 tasks)
- How to sequence refactoring (tests first, then refactor, then optimize)
- DRY vs YAGNI tradeoffs (when abstraction helps vs hurts)

**Testing Orchestration**:
- Test pyramid (unit vs integration vs e2e ratios)
- When to write tests (before? after? during?)
- What to test (happy path, edge cases, error handling)

**Deployment Orchestration**:
- CI/CD sequencing (build → test → deploy → verify)
- Staging vs production strategies
- Rollback planning (git tags, feature flags)

**DO NOT TEACH** (stay focused on orchestration):
- Language-specific syntax or features
- Framework API details
- Algorithm implementations
- Performance optimization techniques

---

### Changing Your Level

**Commands**:
```
"Change scaffolding to Learner"   # Maximum teaching
"Change scaffolding to Growth"    # Moderate teaching [Default]
"Change scaffolding to Balanced"  # Minimal teaching
"Change scaffolding to Expert"    # Maximum speed
```

**What Happens**:
1. AI updates `.flowstate/config.md` (Scaffolding Configuration section)
2. AI confirms the change with a message
3. Next response immediately reflects new level

**Example**:
```
You: "Change scaffolding to Learner"

AI: "✓ Scaffolding level changed to Learner (from Growth)

I'll now provide maximum teaching, explaining every orchestration decision.

.flowstate/config.md updated. Continue when ready."
```

**When to Change**:
- **Start of project**: Growth (learn while building)
- **Stuck on pattern**: Learner (get detailed explanation)
- **Time pressure**: Expert (just get it done)
- **Comfortable**: Balanced (current FlowState behavior)

---

### Consistency Verification

**How to check if AI is following your scaffolding level**:

1. **Read a few responses**: Do they match expected verbosity?
2. **Look for teaching commentary**: Present in Learner/Growth, absent in Balanced/Expert
3. **Check `.flowstate/config.md`**: Verify stored level matches AI behavior
4. **Test switch**: Change levels and observe immediate difference

**If AI is inconsistent**:
- Say: "Please check your scaffolding level and match responses to it"
- Check `.flowstate/config.md` for corruption
- Re-state your level: "My scaffolding level is Growth—please match that"

---

### Frequently Asked Questions

**Q: Does scaffolding slow down the AI?**
**A**: No. Zero overhead—same work, different explanation depth. Expert mode is actually FASTER to read (less text).

**Q: Can I change mid-session?**
**A**: Yes. Say "Change scaffolding to [level]" anytime. Takes effect immediately.

**Q: Will AI remember my level across sessions?**
**A**: Yes. Stored in `.flowstate/config.md`, loaded at session resume.

**Q: What if I want Expert mode but occasionally need detailed explanation?**
**A**: Stay in Expert, but add "Explain your reasoning" to specific requests when you want detail.

**Q: Is Balanced mode the same as v2.2 FlowState?**
**A**: Yes. Balanced = current FlowState behavior (pre-scaffolding).

**Q: Should I start with Learner or Growth?**
**A**: Growth is recommended. Learner can feel verbose if you're not genuinely new to AI orchestration.

**Q: Does this track my progress?**
**A**: No. No adaptive behavior. You choose your level explicitly.

**Q: Can I see examples of each level?**
**A**: Yes. See TEMPLATES.md § Scaffolding Response Templates (7 scenarios showing all 4 levels).

**Q: Does scaffolding teach coding or orchestration?**
**A**: Orchestration. We teach task decomposition, strategic sequencing, architectural thinking—NOT syntax, algorithms, or implementation details.

**Q: How is this different from Copilot/Cursor?**
**A**: Copilot autocompletes code. FlowState teaches you HOW to direct AI, break down problems, and think architecturally. Complementary tools.

---

### Testing Your Understanding

**Try this experiment**:

1. Set scaffolding to Growth
2. Ask AI to add a feature
3. Note the response style (moderate teaching)
4. Change scaffolding to Expert
5. Ask AI to add another feature (similar complexity)
6. Compare: Expert should be 50-70% shorter with no teaching commentary

**What you should observe**:
- **Growth**: "I'll add this feature. My approach is... [explains strategy]"
- **Expert**: "[Adds feature, minimal commentary]"

**If you don't see a clear difference**: AI isn't checking scaffolding level. Say "Check your scaffolding level" to remind it.

---

### Example Comparison: Session Resume

See TEMPLATES.md § Scaffolding Response Templates § Scenario 1 for full examples. Brief summary:

**Learner** (350 words):
- Explains why starting with `.flowstate/tasks.md` (Session Resume Protocol)
- Lists what it's looking for (in_progress, completed, pending tasks)
- Explains what "Prove stage" means
- Provides recommendation with detailed reasoning

**Growth** (200 words):
- States approach (Read `.flowstate/tasks.md` → Check `.flowstate/session.md`)
- Summarizes findings briefly
- Meta-rule check (Prove stage = production focus)
- Recommendation with brief reasoning

**Balanced** (120 words):
- Reads `.flowstate/tasks.md`, `.flowstate/session.md`
- Summarizes current state
- Recommendation (terse)

**Expert** (60 words):
- [Reads files → Summarizes state in brackets → Continues]

---

### Migration from v2.2

**For existing projects**:
- Default scaffolding level: **Balanced** (preserves v2.2 behavior)
- To enable scaffolding: Add 3 lines to `.flowstate/config.md` (see TEMPLATES.md)
- Or: Fresh initialization with v2.3+ (select scaffolding during init)

**Backward compatibility**: Full (v2.3 AI can work with v2.2 projects)

---

**See Also**:
- TEMPLATES.md § Scaffolding Response Templates (7 detailed scenarios)
- QUICKSTART.md § Changing Your Scaffolding Level (quick reference)
- Main framework file § AI Response Protocol (for AI assistants)

---

## 📞 Support

**For questions or issues:**
- Email: abe@flowstateai.dev
- Discord: https://discord.gg/FWx5swdCMK

---

**Version**: 2.5.0
**Last Updated**: 2025-11-24
**Framework Created By**: Abe Burnett, Mythgate
