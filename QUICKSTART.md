# FlowState SE - Quick Start Guide
## Get Running in 5 Minutes

**Version**: 2.5.0
**Last Updated**: 2025-11-24

---

> **🆘 EMERGENCY: FlowState Not Responding?**
> 
> If your AI seems completely unaware of FlowState, use this command:
> ```
> Read TROUBLESHOOTING.md and follow its AI instructions. If you can't access that file, search this workspace for files containing "FlowState" and report what you find.
> ```
> This runs the bootstrap protocol that diagnoses and usually auto-fixes the issue.
> 
> See **[TROUBLESHOOTING.md](TROUBLESHOOTING.md)** for complete diagnostic guide.

---

## ⚡ The 3-Minute Path to Productivity

### Step 1: Place Framework Files (15 seconds)

Put these 6 files where your AI can access them (project root or `docs/` folder):

```
your-project/
├── flowstate-ai-se-framework-v2.5.0.md  ← The main file
├── QUICKSTART.md (this file)
├── REFERENCE.md
├── TEMPLATES.md
└── CHANGELOG.md
```

**Tip**: These files should be in a location your AI can read. Most modern AI assistants can read files in your project directory.

---

### Step 2: Initialize FlowState (a few minutes)

Open your AI assistant and **say**:

```
Read flowstate-ai-se-framework-v2.5.0.md and execute FlowState SE initialization
```


That's it! Your AI will:
1. Find and read `flowstate-ai-se-framework-v2.5.0.md`
2. Recognize the initialization command
3. Execute the initialization protocol
4. Ask about git privacy (if git repository detected) - v2.2 feature
5. Ask you 5 strategic questions
6. Ask about scaffolding level (learning preferences) - v2.3 feature
7. Ask about quality mode (work rigor preferences) - **NEW in v2.4**
8. Create all FlowState files configured for your project

---

### Step 2.5: Git Privacy Configuration (If Git Detected) [NEW in v2.2]

**If your project is a git repository**, AI will ask:

#### Privacy Mode Selection
```
✅ Git repository detected.

How would you like to handle git integration?

[1] Private ignore (teammates can't see) [Recommended]
    • FlowState files invisible to teammates
    • No .gitignore changes

[2] Team ignore (visible in .gitignore)
    • Team sees FlowState in .gitignore
    • Shared team configuration

[3] Manual (you handle git yourself)

[4] Skip

Choice [1]: _
```

**Recommendation**: Choose **[1] Private ignore** for invisibility.

---

#### Filename Mode (If You Chose Private Ignore)
```
Would you like obfuscated filenames for extra privacy?

Standard:    FLOWSTATE.md, TASKS.md, SESSION.md
Obfuscated:  .project-config.md, .tasks.md, .session-state.md

Use obfuscated filenames? [y/N]: _
```

**Recommendation**: Choose **N** for standard (easier to recognize). Choose **y** if you want maximum stealth.

**Time added**: ~15 seconds (2 quick questions)

**What happens**:
- Private mode: AI configures `.git/info/exclude` (invisible to teammates)
- Team mode: AI adds patterns to `.gitignore` (visible to teammates)
- Manual/Skip: You handle git configuration yourself

---

### Step 3: Answer 5 Strategic Questions (2 minutes)

AI will ask:

#### Question 1: Project Maturity
```
A) Brand new (just started)
B) Early (0-3 months, basic functionality)
C) Mature (3+ months, production-ready)
```

**Tip**: Choose honestly—this affects file size caps and refactor frequency.

---

#### Question 2: Phase 0 Success Metric
```
What must be true to call Phase 0 "done"?

Example: "Users can sign up, create projects, and invite team members"
```

**Tip**: Be specific. This becomes your acceptance criteria.

---

#### Question 3: Deployment Target
```
A) Vercel / Netlify (serverless)
B) AWS / GCP / Azure (cloud)
C) Self-hosted (VPS, bare metal)
D) Other / Not decided
```

**Tip**: Affects infrastructure guidance AI provides.

---

#### Question 4: Subscription Model
```
A) Yes (Free, Pro, Enterprise tiers)
B) No (single tier or open source)
C) Not decided yet
```

**Tip**: "Yes" enables Meta-Rules 11 & 12 (subscription context, entitlement testing).

---

#### Question 5: Immediate Priority
```
What should we work on first after initialization?

Example: "Implement user authentication with Clerk"
```

**Tip**: This becomes your first task in TASKS.md.

---

### Step 3.5: Select Scaffolding Level (10 seconds) [NEW in v2.3]

AI will ask about your learning preferences:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SCAFFOLDING LEVEL SELECTION

FlowState can adjust its teaching style to match your experience
with AI orchestration (how you direct and collaborate with AI).

This is NOT about coding skill—it's about learning to "vibe code"
(orchestrate AI, think architecturally, decompose problems).

Select your preferred level:

[1] Learner   - Maximum teaching, explain every decision
               (First time using AI assistants for real work)

[2] Growth    - Moderate teaching, explain key decisions [RECOMMENDED]
               (Comfortable with AI basics, want to level up)

[3] Balanced  - Current FlowState behavior, explanations when needed
               (Experienced with AI orchestration)

[4] Expert    - Minimal explanations, maximum speed
               (Power users who know FlowState deeply)

You can change this anytime by saying "Change scaffolding to [level]"
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Your choice [1/2/3/4]: _
```

**Recommendation**: Choose **[2] Growth** if you're new to AI orchestration. Choose **[3] Balanced** if you're experienced.

**Time added**: ~10 seconds (1 question)

**What this does**:
- **Learner**: AI explains every orchestration decision in detail (great for learning)
- **Growth**: AI explains key strategic decisions (helps you level up)
- **Balanced**: AI explains only when necessary (experienced users)
- **Expert**: AI is terse and action-focused (power users)

**What scaffolding teaches** (Vibe Coding):
- ✅ Task decomposition (how to break down problems)
- ✅ Strategic sequencing (what to do first, why)
- ✅ Meta-rule application (when to follow which rule)
- ✅ Architectural thinking (system design, not just code)

**What scaffolding does NOT teach** (Implementation):
- ❌ Coding syntax or language features
- ❌ Tool selection (which library to use)
- ❌ Algorithm implementations

**See**: `REFERENCE.md` § Appendix F for complete scaffolding guide

---

### Step 3.6: Select Quality Mode (10 seconds) [NEW in v2.4]

AI will ask about work rigor preferences:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
QUALITY MODE SELECTION

Quality Mode controls the RIGOR of work performed (documentation depth,
validation thoroughness, review frequency). This is INDEPENDENT from
scaffolding level (which controls explanation verbosity).

Select your preferred quality mode:

[1] Fast        - Minimal ceremony, essential work only
                 (Prototyping, quick iterations, time-sensitive demos)

[2] Balanced    - Standard rigor, selective validation [RECOMMENDED]
                 (Normal development, balance speed with quality)

[3] Methodical  - Maximum thoroughness, comprehensive checks
                 (Production-critical, security-sensitive, complex systems)

You can change this anytime by saying "Change quality mode to [mode]"
For specific high-stakes tasks, use `ultrathink` to temporarily force
Methodical mode.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Your choice [1/2/3]: _
```

**Recommendation**: Choose **[2] Balanced** for most work. Use **[3] Methodical** for production deployments or security-critical features.

**Time added**: ~10 seconds (1 question)

**What this controls**:
- **Fast**: Skip optional docs, minimal validation, no check-ins
- **Balanced**: Standard docs/tests, occasional check-ins (DEFAULT)
- **Methodical**: Comprehensive docs, exhaustive validation, frequent check-ins

**Quality Mode × Scaffolding are INDEPENDENT**:
- Scaffolding = HOW MUCH AI EXPLAINS (teaching verbosity)
- Quality Mode = HOW MUCH WORK AI DOES (validation rigor)
- You can have any combination (e.g., Expert scaffolding + Methodical quality = thorough work, terse explanations)

**See**: `REFERENCE.md` § Quality Mode System for complete guide

---

### Step 4: AI Configures Everything (a few minutes)

After you answer the questions, AI automatically:
- ✅ Detects your platform (Claude Code / Copilot / Cursor / Codex)
- ✅ Scans your project (languages, frameworks, directory structure)
- ✅ Adapts Meta-Rules (file size caps based on language)
- ✅ Creates 3 universal files (`FLOWSTATE.md`, `TASKS.md`, `SESSION.md`)
- ✅ Creates platform adapters (`CLAUDE.md`, `AGENTS.md`, `.cursor/rules/*.mdc`)
- ✅ Optionally creates a git checkpoint **only** if you're not in Private mode and explicitly ask for it
- ✅ Reports readiness with next steps

**You'll see something like this:**
```
┌─────────────────────────────────────────────────────────┐
│  ✅ FlowState AI Framework SE v2.5.0 Initialized        │
└─────────────────────────────────────────────────────────┘

Platform Detected: Claude Code
Languages: TypeScript, JavaScript
Frameworks: Next.js, React, Prisma

Files Created:
  ✅ FLOWSTATE.md (Project rules, 14 Meta-Rules including Execution Loop)
  ✅ TASKS.md (5 initial Phase 0 tasks)
  ✅ SESSION.md (Session state tracker)
  ✅ CLAUDE.md (Claude Code instructions)
  ✅ AGENTS.md (Copilot/Codex compatibility)
  ✅ .cursor/rules/flowstate.mdc (Cursor rules)

Configuration:
  Scaffolding Level: Growth (moderate teaching)
  Quality Mode: Balanced (standard rigor)

Git (optional, non-private modes only):
  - You may create your own checkpoint commit/tag if you want FlowState tracked in git.
  - In Private mode, FlowState does **not** create git commits or tags automatically.

Current State:
  Phase: Phase 0 – Foundation (0% complete)
  File Size Cap: ≤400 LOC (TypeScript/JavaScript)

## 🎯 ACTIVE STATE:
  ⏳ P0 Task 1: Implement user authentication with Clerk
  ⏳ P0 Task 2: Set up PostgreSQL database with Prisma
  ⏳ P0 Task 3: Create basic API routes structure
  ⏳ P0 Task 4: Add error handling middleware
  ⏳ P0 Task 5: Write initial integration tests

## 🎯 NEXT RECOMMENDED:
1. Start with Task 1 (authentication) - unblocks user features
2. Then Task 2 (database) - required for data persistence
3. Then Task 3 (API structure) - foundation for all endpoints

## PROCEED WITH:
- `proceed` → Start Task 1 only, check in after
- `proceed next` → Complete Tasks 1-2, check in
- `proceed all` → Complete all 5 P0 tasks (check-ins every 3)

What would you like to work on first?
```

---

### Step 5: Verify & Start Building (30 seconds)

**Quick Verification** [NEW in v2.5]: Instead of manually checking files, say:

```
FlowState verify
```

The AI will read each file and confirm it exists with a verification report:
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
VERIFICATION COMPLETE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✅ config.md — verified
✅ tasks.md — verified
✅ session.md — verified
✅ version.txt — verified
✅ CLAUDE.md — verified
✅ directories — verified
All [6/6] checks passed.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Manual Check** (if you prefer): Verify these files exist:

#### Universal FlowState Files:
- [ ] `.flowstate/config.md`
- [ ] `.flowstate/tasks.md`
- [ ] `.flowstate/session.md`
- [ ] `.flowstate/version.txt` (should contain "2.5.0")
- [ ] `.flowstate/archive/`, `.flowstate/plans/`, `.flowstate/logs/` directories

#### Platform Adapters (at least one):
- [ ] `CLAUDE.md` created (if Claude Code detected)
- [ ] `AGENTS.md` created (if Copilot/Codex detected)
- [ ] `.cursor/rules/flowstate.mdc` created (if Cursor detected)
- [ ] `.cursorrules` created (legacy Cursor support)

#### Git State (optional, only if you chose to commit):
- [ ] Commit exists for your project baseline (message of your choice)
- [ ] Tag exists (e.g., `flowstate-se-init`) if you created one

In **Private** mode it is normal for there to be **no** FlowState commits or tags.

---

## 🎯 What's Now Possible (v2.5.0 Features)

Now that FlowState is initialized, here's what you can do:

| Feature | Command | What it does |
|---------|---------|--------------|
| **Learn concepts** | `Change concept level to Novice` | AI teaches you language/framework concepts as you work |
| **Sync after offline work** | `FlowState sync` | Reconcile your task list with code changes you made without FlowState |
| **Guided debugging** | `Learner MAX` | Get guided problem-solving instead of "just fix it" |
| **Search old tasks** | `FlowState find task [query]` | Search archived completed tasks |
| **Generate handoff** | `FlowState handoff` | Create context document for another developer or AI |
| **Check velocity** | `How am I doing?` | See progress metrics and estimates |
| **Verify files** | `FlowState verify` | Confirm all FlowState files exist and are valid |

**Tip**: These are all optional enhancements. The core FlowState workflow (tasks, sessions, meta-rules) works the same as before.

---

## 🚀 Your First Session (Start Building)

### Start Working

```
You: "Implement user authentication with Clerk"

AI: [Reads FLOWSTATE.md, TASKS.md, SESSION.md]
    "Starting with user authentication...

     I'll implement:
     1. Clerk SDK integration
     2. Sign-up and login flows
     3. Session management
     4. Protected routes

     This is a [Work] stage implementation (make it function).

     Proceeding..."

    [AI implements feature following all 13 Meta-Rules]

AI: "✅ User authentication complete!

     ✅ Tests passing (evidence: logs/auth_2025-10-26_1430.log)
     ✅ Git tagged: auth-work-after (rollback point)
     ✅ TASKS.md updated (moved to Testing)

     Next priority: Set up PostgreSQL database with Prisma

     Continue with database setup?"
```

---

### Check Current State

```
You: "What's the current state?"

AI (Session Manager Agent):
"Reading .flowstate/session.md...

 Phase 0: Foundation (15% complete)

 Active Work:
 - User authentication (Done - in Testing)

 Completed (Last 3):
 1. User authentication with Clerk (2025-10-26)
    Evidence: logs/auth_2025-10-26_1430.log

 Next Priorities:
 1. [P0] Set up PostgreSQL database with Prisma
 2. [P0] Create basic API routes structure
 3. [P1] Implement error handling middleware

 Quality Metrics:
 - Files under cap: ✅ All files <400 LOC
 - Refactor counter: 1/5 tasks (trigger at 5)
 - Test coverage: 45% (target: 80% by Phase 1)

 On track for Phase 0 completion."
```

---

### End Your Session

```
You: "Done for today"

AI (Session Manager Agent):
"Closing FlowState session...

 ✅ .flowstate/session.md updated
 ✅ .flowstate/tasks.md synced
 ✅ Standup summary generated
 ✅ Git committed: 'FlowState: Update session state'

 Session Summary:

 Yesterday (2025-10-26):
 ✅ Completed user authentication with Clerk
    - Users can sign up, login, manage sessions
    - Tests passing (87% coverage on auth module)
    - Evidence: logs/auth_2025-10-26_1430.log

 Today (2025-10-27):
 - Set up PostgreSQL database with Prisma
 - Create basic API routes structure

 Blockers: None

 Notes:
 - On track for Phase 0 (3 weeks remaining)
 - Test coverage: 45% (need 80% by Phase 1)
 - All files under size cap

 See you tomorrow!"
```

---

## 📋 Common Commands Reference

### Session Management

| Command | What It Does |
|---------|-------------|
| `Read flowstate-ai-se-framework-v2.5.0.md and execute FlowState SE initialization` | Initialize FlowState (first time only) |
| `Resume FlowState` | Load context from .flowstate/session.md and continue work |
| `What's the current state?` | Get phase progress, active work, next priorities |
| `Done for today` | Update .flowstate/session.md, generate standup summary, close session |

---

### System Health & Diagnostics [NEW in v2.3.1]

| Command | What It Does |
|---------|-------------|
| `FlowState status` | Quick read-only health check (framework, initialization, adapters, git) |
| `FlowState doctor` | Full diagnostic + offer to restore broken configuration |
| `Add FlowState to [platform]` | Install adapter for additional AI tool (e.g., "Add FlowState to Cursor") |
| `Read TROUBLESHOOTING.md and follow its AI instructions` | Emergency recovery (works even when AI has zero FlowState awareness) |

**For detailed troubleshooting**, see **[TROUBLESHOOTING.md](TROUBLESHOOTING.md)**

---

### Task Management

| Command | What It Does |
|---------|-------------|
| `Show tasks` | List all tasks from .flowstate/tasks.md (Backlog, In-Progress, Done) |
| `What's next?` | Get top 3 priorities from .flowstate/tasks.md |
| `Add task: [description]` | Add new task to .flowstate/tasks.md backlog |

---

### Planning

| Command | What It Does |
|---------|-------------|
| `Create plan for [feature]` | Trigger Planning Agent to create detailed plan document |
| `Show plan PLAN-001` | Display specific plan document |
| `List all plans` | Show all plans in `plans/` directory |

---

### Quality Management

| Command | What It Does |
|---------|-------------|
| `Run refactor cycle` | Trigger Refactor Agent to scan and propose improvements |
| `Run bug hunt` | Trigger Bug Hunt Agent to scan for issues |
| `Check file sizes` | List files approaching size caps |
| `Show quality metrics` | Display test coverage, file sizes, refactor counter |

---

### Git & Evidence

| Command | What It Does |
|---------|-------------|
| `Show evidence for [feature]` | Display evidence log from `logs/` directory |
| `List rollback tags` | Show all git tags for rollback (`*-before`, `*-after`) |
| `Show recent commits` | Display git log with FlowState commit messages |

---

## 🆘 Quick Troubleshooting

**Something not working?** → See **[TROUBLESHOOTING.md](TROUBLESHOOTING.md)** for comprehensive diagnostics and recovery procedures.

### Quick Checks

1. **FlowState not responding?**
   - Try: `Read TROUBLESHOOTING.md and follow its AI instructions...` (works even with zero FlowState awareness)
   - See: [Emergency Recovery Protocol](TROUBLESHOOTING.md#emergency-recovery-command)

2. **Files weren't created?**
   - Try: `FlowState doctor` (diagnoses + offers to fix)
   - See: Partially Initialized

3. **Lost context mid-session?**
   - Try: `Rebuild context from SESSION.md`
   - See: [Session Recovery](TROUBLESHOOTING.md#lost-context-mid-session)

4. **Wrong platform detected?**
   - Try: `FlowState SE. I'm using [platform name]`
   - See: [Platform Detection Issues](TROUBLESHOOTING.md#platform-detection-issues)

### Most Common Issues

- **[FlowState stopped working after tool update](TROUBLESHOOTING.md#scenario-1-flowstate-stopped-working-after-tool-update)** - Tool updated and AI lost framework awareness
- **[Setting up on multiple platforms](TROUBLESHOOTING.md#scenario-2-setting-up-multiple-ai-platforms)** - Using Claude + Cursor + Copilot together
- **[New machine setup](TROUBLESHOOTING.md#scenario-3-new-machine-setup)** - Cloned repo, framework not working
- **[File size violations](TROUBLESHOOTING.md#file-size-cap-issues)** - AI creates files >400 LOC
- **[Manual edits broke framework](TROUBLESHOOTING.md#scenario-5-manual-edits-broke-framework)** - Modified adapter files incorrectly

---

### Problem: Can't find test for a module

**Solution:**
```
You: "Where are the tests for [module]?"

AI: "Searching for tests...

     Found:
     - Unit tests: tests/[module].test.ts
     - Integration tests: tests/integration/[module]-integration.test.ts

     [If not found:]
     No tests found for [module] (comprehension debt violation - Meta-Rule 13).

     Create tests now? Recommended location: tests/[module].test.ts"
```

---

## 🎯 Platform-Specific First Sessions

### Claude Code

```
Day 1: Initialize
You: "FlowState SE"
AI: [Initializes automatically]

Day 2: Resume
You: "Resume FlowState"
AI: [Reads .flowstate/session.md automatically]
```

**Notes:**
- CLAUDE.md is auto-read at session start
- TodoWrite tool syncs with TASKS.md
- Evidence logs captured automatically

---

### GitHub Copilot

```
Day 1: Initialize
You: "FlowState SE"
AI: [Initializes, creates AGENTS.md]

Day 2: Resume
You: "@workspace Resume FlowState"
AI: [Reads AGENTS.md, SESSION.md]
```

**Notes:**
- AGENTS.md is auto-read in Agent Mode
- Use autonomous execution for multi-step tasks
- PRs submitted automatically with evidence

---

### Cursor

```
Day 1: Initialize
You: "FlowState SE"
AI: [Initializes, creates .cursor/rules/flowstate.mdc]

Day 2: Resume
Just start working—rules auto-apply
```

**Notes:**
- flowstate.mdc has `alwaysApply: true`
- You approve each file edit (control)
- Rules reference FLOWSTATE.md, TASKS.md, SESSION.md

---

### OpenAI Codex

```
Day 1: Initialize
You: "FlowState SE"
AI: [Initializes, creates AGENTS.md]

Day 2: Resume
You: "@AGENTS.md Resume FlowState"
AI: [Reads AGENTS.md and loads context]
```

**Notes:**
- Use @filename syntax for direct references
- Leverage 7+ hour sessions for complex features
- Internal to-do syncs with TASKS.md

---

## ✅ Success Checklist (After First Session)

After your first session with FlowState, you should be able to:

- [ ] Initialize project with "FlowState SE" (2 minutes)
- [ ] See all files created correctly (validation checklist passed)
- [ ] Implement a feature with AI following Meta-Rules
- [ ] See evidence log created in `logs/` directory
- [ ] See git tags created (`[feature]-before`, `[feature]-after`)
- [ ] See TASKS.md updated as AI works
- [ ] Close session and get standup summary
- [ ] Resume next day with "Resume FlowState" (context restored in <30 seconds)

**If any of these failed**, see Troubleshooting section above or consult [REFERENCE.md](REFERENCE.md).

---

## 🎓 Changing Your Scaffolding Level [NEW in v2.3]

**Anytime during your session**, you can adjust how much teaching you receive from AI.

### Commands

```
"Change scaffolding to Learner"   # Maximum teaching
"Change scaffolding to Growth"    # Moderate teaching [Default]
"Change scaffolding to Balanced"  # Minimal teaching
"Change scaffolding to Expert"    # Maximum speed
```

### What Changes

- ✅ AI response verbosity (how much explanation you get)
- ✅ Teaching commentary (orchestration patterns, meta-rule application)
- ✗ The work itself (same quality across all levels)

### When to Change

**Scenarios**:
- **Start of project**: Growth (learn while building)
- **Stuck on pattern**: Learner (get detailed explanation)
- **Time pressure**: Expert (just get it done)
- **Comfortable with FlowState**: Balanced (current behavior)

### Example

```
You: "Change scaffolding to Learner"

AI: "✓ Scaffolding level changed to Learner (from Growth)

I'll now provide maximum teaching, explaining every orchestration decision
in detail. This is great for learning new patterns and understanding how
to think architecturally.

FLOWSTATE.md updated. Continue when ready."
```

**See**: `REFERENCE.md` § Appendix F for complete scaffolding guide with examples

---

## 📚 Next Steps

**You've completed QuickStart!** Here's what to explore next:

1. **Dive Deeper**: Read [flowstate-ai-se-framework-v2.5.0.md](flowstate-ai-se-framework-v2.5.0.md) for philosophy and agent identities
2. **Master Meta-Rules**: See [REFERENCE.md](REFERENCE.md) for detailed rules and protocols
3. **Customize Templates**: See [TEMPLATES.md](TEMPLATES.md) to customize documents
4. **Check Version History**: See [CHANGELOG.md](CHANGELOG.md) for migration guides

---

## 💬 Getting Help

**Common Resources:**
- **Quick answers**: This file (QUICKSTART.md)
- **Detailed guidance**: [REFERENCE.md](REFERENCE.md)
- **Customization**: [TEMPLATES.md](TEMPLATES.md)

**Still stuck?**
- Email: abe@flowstateai.dev
- Discord: https://discord.gg/FWx5swdCMK

---

**You're ready to build. Ship smart, ship fast, ship sustainable.** 🚀
