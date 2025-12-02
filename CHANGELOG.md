# FlowState SE - Changelog
## Version History and Migration Guides

**Current Version**: 2.5.0
**Last Updated**: 2025-11-24

---

## [2.5.0] - 2025-11-24

### 🎓 Contextual Concept Teaching (CCT)

**NEW**: AI now teaches language/framework/library concepts gradually over time.

- **Concept Levels**: Novice / Apprentice (default) / Practitioner / Fluent
- **Per-technology tracking**: Different mastery levels for each technology
- **~1 concept per session**: Brief, contextual, non-blocking teaching
- **Vocabulary progression**: AI adapts vocabulary as you learn

This is INDEPENDENT from existing Scaffolding (AI orchestration teaching):
- Scaffolding = How to direct AI
- Concept Levels = Domain knowledge of your tech stack

### 🎓 Learner MAX Mode

**NEW**: Guided problem-solving for users who get stuck.

- Three options: "Just fix it" / "Walk me through" / "Explain first"
- Diagnostic question frameworks for common problem types
- Always escapable: Say "just fix it" anytime
- Builds debugging skills, not just AI dependence

### 🔄 FlowState Sync Protocol

**NEW**: Reconcile FlowState with reality after off-reservation work.

- 7-phase sync protocol
- Detects drift between TASKS.md and actual code state
- Integrates with git (if FlowState manages git)
- Suggests specific next tasks with quick-start triggers (say "1", "2", or "both")
- Rich aliases: `FS sync`, `Sync up`, `Catch up`, etc.

### 📁 .flowstate/ Directory (New Default)

**CHANGED**: All FlowState files now live in `.flowstate/` by default.

- Cleaner project root
- No conflicts with user's README.md, etc.
- Easier privacy configuration
- Automatic migration from v2.4 structure

Structure:
```
.flowstate/
├── config.md (was FLOWSTATE.md)
├── tasks.md (was TASKS.md)
├── session.md (was SESSION.md)
├── archive/
├── plans/
├── logs/
└── version.txt
```

### 📦 Task Archival System

**NEW**: Automatic archival of completed tasks.

- `ARCHIVED-TASKS.md` for historical context
- Triggers: >15 done tasks, phase transition, manual request
- Searchable: `FlowState find task [query]`
- Rich aliases and flexible intent matching

### 🌐 Proactive Knowledge Currency Protocol

**NEW**: AI self-assesses knowledge freshness and requests updates.

- Confidence indicators in responses (HIGH/MEDIUM/LOW)
- Proactive prompts: "My knowledge of X is from [date], shall I search for updates?"
- Documentation lookup: `FlowState docs [tech] [topic]`

### 📈 Velocity Metrics

**NEW**: Progress analytics at TOP of SESSION.md.

- Tasks completed this week
- Velocity trends
- Phase completion projections
- Bottleneck detection
- Enabled by default (opt-out available)

### 🤝 Handoff Generation

**NEW**: Context transfer documents for multi-developer/multi-AI scenarios.

- Command: `FlowState handoff`
- Comprehensive project state summary
- Technical context and gotchas
- Immediate next steps
- Prominently placed in SESSION.md and QUICKSTART.md

### 🔄 Phase Retrospectives

**NEW**: Learning capture at phase transitions.

- Automatic prompt when phase completes
- What went well / what to improve
- Saved to `.flowstate/archive/retrospective-phase-N.md`
- Key learnings carried forward

### 💡 Enhanced Key Decisions Section

**IMPROVED**: SESSION.md Key Decisions section with better guidance.

- Architectural decisions with rationale
- Tech stack constraints
- Fragile areas (files to handle carefully)
- User preferences discovered during work

### ✅ Self-Verification Protocol

**NEW**: Mandatory verification step during initialization prevents silent failures.

- AI now reads each file after creation to confirm it exists
- Explicit verification output format proves files were actually created
- If any file is missing, AI creates it and re-verifies before reporting success
- **Cross-AI reliability**: Designed to catch failures on Codex, Gemini, and other platforms that sometimes skip tool calls
- New command: `FlowState verify` — run anytime to check all files exist

### 🎯 "What's Now Possible" Upgrade Experience

**NEW**: UPGRADE.md now shows transformation stories, not just procedural steps.

- Before/After comparisons for each major feature
- "Try it after upgrading" prompts with specific commands
- Quick reference table of new commands
- Helps users understand value of new features, not just how to install them

### 🔧 Other Improvements

- **Flexible command matching**: AI responds to intent, not just exact syntax
- **Quick task triggers**: Say "1", "2", or "both" after sync/resume
- **Cross-references**: All documents properly linked
- **Version/date consistency**: All files updated to 2.5.0
- **Cross-AI robustness**: Instructions use explicit "DO NOT skip" and "MUST" language for better reliability across platforms

### Migration from v2.4

See UPGRADE.md for complete migration guide. Key points:
- Automatic migration of file structure to `.flowstate/`
- Privacy settings preserved (never changed during migration)
- All user content preserved
- Adapter files updated with new paths

---

## Version 2.4.0 (2025-11-15)

### 🚀 Major Feature: Quality Mode System + Execution Loop Contract

This release introduces a comprehensive execution control system that gives users fine-grained control over work rigor and provides persistent task visibility with frictionless continuation.

**Key Innovation**: Independent quality mode dimension + structured execution loop with proceed commands.

**Target Audience**: All FlowState users who want better control over AI work thoroughness and seamless task continuation.

---

### ✨ New Features

#### 1. **Quality Mode System - Independent Work Rigor Control**

**The Problem**: Users needed flexibility between:
- Fast prototyping (minimal ceremony)
- Standard development (balanced rigor)
- Production-critical work (maximum thoroughness)

Previous system: Scaffolding controlled BOTH explanation verbosity AND work rigor (conflated concerns).

**The Solution**: Quality Mode as independent dimension from scaffolding

**The Three Quality Modes**:

**Fast Mode** - Minimal ceremony, essential work only:
- Documentation: Update TASKS.md + SESSION.md only (skip DECISIONS.md, PLAN-*.md)
- Validation: Run tests, basic checks (skip integration tests, edge cases)
- Git tagging: Milestones only
- Evidence trails: Minimal logging
- Review checkpoints: None (proceed to completion)
- **Use cases**: Prototyping, throwaway code, time-sensitive demos

**Balanced Mode (DEFAULT)** - Standard rigor, selective validation:
- Documentation: Update TASKS.md, SESSION.md, DECISIONS.md for major decisions
- Validation: Unit + integration tests, basic edge cases, type checking
- Git tagging: Every 3 tasks or significant feature
- Evidence trails: Moderate logging (key findings)
- Review checkpoints: Occasional (after complex tasks)
- **Use cases**: Normal development, most team projects

**Methodical Mode** - Maximum thoroughness, comprehensive checks:
- Documentation: Update ALL files (TASKS.md, SESSION.md, DECISIONS.md, PLAN-*.md)
- Validation: Comprehensive tests (unit, integration, edge cases, security)
- Git tagging: Every completed task
- Evidence trails: Detailed logging (all findings, rationale, alternatives)
- Review checkpoints: Frequent (every 1-2 tasks)
- **Use cases**: Production deployments, security-critical, complex architecture, migrations

**Configuration**: Added to FLOWSTATE.md during initialization (Step 6.6)

**Command**: `Change quality mode to [Fast/Balanced/Methodical]`

---

#### 2. **Independent Dimensions: Scaffolding × Quality Mode**

**Critical Design Decision**: These are INDEPENDENT dimensions that combine

**Scaffolding Level** controls:
- ❓ How much explanation accompanies the work
- ❓ Teaching verbosity (3x / 2x / 1x / 0.5x)
- ❓ Pedagogical tone (patient vs terse)

**Quality Mode** controls:
- ❓ How much work is done per task
- ❓ Rigor of validation (minimal vs standard vs comprehensive)
- ❓ Documentation updates (skip vs selective vs complete)

**9 Valid Combinations**:
| Combination | Behavior |
|-------------|----------|
| Learner + Fast | Minimal rigor, maximum teaching |
| Learner + Balanced | Standard rigor, maximum teaching |
| Learner + Methodical | Maximum rigor, maximum teaching |
| Growth + Fast | Minimal rigor, moderate teaching |
| Growth + Balanced | Standard rigor, moderate teaching |
| Growth + Methodical | Maximum rigor, moderate teaching |
| Balanced + Fast | Minimal rigor, minimal teaching |
| Balanced + Balanced | Standard rigor, minimal teaching |
| Balanced + Methodical | Maximum rigor, minimal teaching |
| Expert + Fast | Minimal rigor, no teaching |
| Expert + Balanced | Standard rigor, no teaching |
| Expert + Methodical | Maximum rigor, no teaching |

**Example**: Expert + Methodical = Thorough work with terse explanations (power user who wants production rigor without verbosity)

---

#### 3. **Meta-Rule 14: Execution Loop Contract**

**The Problem**: Users experienced friction:
- "AI stopped and I don't know what to say next"
- "Where's my task list between responses?"
- "What should I do after this completes?"

**The Solution**: Every work response ends with structured 5-part Execution Loop

**The 5-Part Structure**:

1. **COMPLETED** (1-2 sentences)
   - What was just finished
   - Outcome or status

2. **ACTIVE STATE** (3-7 items, visual format)
   - Current task list with priorities and progress
   - P0/P1/P2 priority labels
   - ✅/🔄/⏸️ status indicators
   - Visual arrows showing current position

3. **NEXT RECOMMENDED** (1-3 actions, prioritized)
   - What should happen next (in priority order)
   - Brief rationale for sequencing
   - Dependencies or prerequisites

4. **PROCEED WITH** (copy-paste commands)
   - `proceed` → Current task only
   - `proceed next` → Current + next 1 task
   - `proceed all` → All P0 tasks (check-ins every 3)
   - `ultrathink` → Force Methodical mode for current task
   - `pause` → Stop and wait for instruction

5. **NOTES** (optional)
   - Warnings or blockers
   - Phase progress updates
   - Important decisions made

**When Applied**: After every response where AI performed work (wrote code, updated files, ran commands)

**Quality Mode Interaction**:
- Fast: Terse COMPLETED, minimal/no NOTES
- Balanced: Clear COMPLETED, occasional NOTES
- Methodical: Detailed COMPLETED, comprehensive NOTES

**Scaffolding Interaction**:
- Execution Loop structure stays consistent
- Explanation BEFORE loop varies by scaffolding level
- Learner: Extensive teaching before loop
- Expert: Minimal summary before loop

---

#### 4. **Proceed Commands - Structured Continuation Control**

**The Five Commands**:

**`proceed`** - Execute current task only:
- Complete the current task in ACTIVE STATE
- Check in via Execution Loop
- Wait for next instruction

**`proceed next`** - Execute current + next 1 task:
- Complete current task
- Automatically start next task
- Check in after completing second task

**`proceed all`** - Execute all P0 tasks with check-ins every 3:
- Complete current task
- Continue with remaining P0 tasks automatically
- Check in after every 3 tasks
- Stop after completing all P0 tasks
- **Safety**: Stops on blockers, scope creep, or context limit

**`ultrathink [optional: task]`** - Force Methodical mode temporarily:
- Override current quality mode to Methodical
- Execute specified task (or current if none specified)
- Apply maximum thoroughness
- Return to previous quality mode after completion
- **Use case**: High-stakes tasks requiring extra rigor

**`pause`** - Stop automatic execution:
- Stop after completing current operation
- Show Execution Loop with current state
- Wait for explicit instruction

**Command Aliases**: `continue`, `next`, `go`, `keep going`, etc. are equivalent

**Quality Mode Interaction**: Commands work identically, execution characteristics differ
**Scaffolding Interaction**: Commands work identically, explanation verbosity differs

---

### 🔧 Framework Changes

#### Initialization Updates (Step 6.6)
- **New step**: Quality Mode selection after Scaffolding
- **Prompt**: Choose Fast/Balanced/Methodical with use case descriptions
- **Default**: Balanced mode (standard rigor)
- **Configuration**: Stored in FLOWSTATE.md § Quality Mode Configuration
- **Time added**: ~10 seconds

#### FLOWSTATE.md Template Updates
- **New section**: Quality Mode Configuration (3 lines)
- **Fields**: Quality Mode, Changed date, Independence note
- **Matrix reference**: Quality × Scaffolding combinations

#### Meta-Rules Count
- **Updated**: 13 Meta-Rules → 14 Meta-Rules
- **New**: Meta-Rule 14 (Execution Loop Contract)
- **All references updated**: Framework, TEMPLATES.md, REFERENCE.md, QUICKSTART.md

#### AI Response Protocol Updates
- **New section**: Quality Mode × Scaffolding Interaction (~150 lines)
- **9-combination matrix**: All valid pairings documented
- **AI checklist**: Pre-response validation logic
- **Common misconceptions**: Clarifications on independent dimensions

---

### 📚 Documentation Updates

#### Framework File (`flowstate-ai-se-framework-v2.4.0.md`)
- **Lines added**: +769 lines (2,239 → 3,008 lines, +34% growth)
- **Step 6.6**: Quality Mode Selection (~120 lines)
- **Meta-Rule 14**: Execution Loop Contract (~250 lines)
- **Proceed Commands Reference**: ~200 lines (all variants, matrices, patterns)
- **Quality × Scaffolding Integration**: ~150 lines (matrix, examples, checklist)

#### TEMPLATES.md
- **Quality Mode Configuration template**: Added to FLOWSTATE.md template
- **Meta-Rule 14**: Added to meta-rules list with summary
- **Quality × Scaffolding matrix**: Documented with examples
- **Version**: 2.3.1 → 2.4.0

#### REFERENCE.md
- **Meta-Rule 14 Deep Dive**: Complete specification (~180 lines)
  - 5-part structure with examples
  - Quality/scaffolding interactions
  - AI enforcement checklist
  - Common mistakes and solutions
  - User benefits
- **Quality Mode System section**: Placeholder with cross-references
- **Proceed Commands section**: Placeholder with cross-references
- **Table of contents**: Updated (13 → 14 meta-rules, new sections)
- **Version**: 2.3.1 → 2.4.0

#### QUICKSTART.md
- **Step 3.6**: Quality Mode Selection with recommendations
- **Initialization flow**: Updated to include quality mode
- **Example output**: Shows Execution Loop format, 14 meta-rules, both configs
- **Proceed commands**: Shown in example initialization output
- **Version**: 2.3.1 → 2.4.0

---

### 🎯 Design Rationale

#### Why Independent Dimensions?

**Rejected Approach**: Multiplicative system (Scaffolding × Quality = 12 combined modes)
- **Problem**: Users would need to understand 12 distinct behaviors
- **Complexity**: Difficult to reason about interactions

**Rejected Approach**: Restrictive coupling (e.g., Expert can't use Fast)
- **Problem**: Artificial constraints on user needs
- **Real scenario**: Power users DO need fast prototyping sometimes

**Chosen Approach**: Independent Orthogonal Dimensions (Option B)
- **Benefit**: Simple mental model (set each independently)
- **Flexibility**: Any combination valid (9 total)
- **Intuitive**: Scaffolding = explanation depth, Quality = work rigor
- **User control**: Change either dimension without affecting the other

#### Why "Methodical" Instead of "Deep"?

User feedback: "Methodical" better conveys:
- Deliberate, systematic approach
- Comprehensive validation
- Production-ready thoroughness

"Deep" could imply just more thinking, not necessarily more rigor.

#### Why "proceed all" with Check-ins?

**Rejected**: Unbounded "proceed with all recommendations"
- **Problem**: No limits, runaway execution risk
- **Safety concern**: User loses control

**Chosen**: Bounded with check-ins every 3 tasks
- **Safety**: Regular checkpoints for user review
- **Control**: User can pause at any check-in
- **Transparency**: Clear progress updates
- **Predictable**: Known behavior (stop at 3, 6, 9, etc.)

---

### 📋 Migration Guide: v2.3.2 → v2.4.0

#### For New Projects

Initialize with v2.4.0:
```
Read flowstate-ai-se-framework-v2.4.0.md and execute FlowState SE initialization
```

You'll be asked about:
1. Strategic questions (5 questions)
2. Scaffolding level (Learner/Growth/Balanced/Expert)
3. **NEW**: Quality mode (Fast/Balanced/Methodical)

#### For Existing v2.3.x Projects

**Option A: Manual Update** (Recommended for understanding changes)

1. **Update FLOWSTATE.md**:
   ```markdown
   ## Quality Mode Configuration [NEW in v2.4]

   **Quality Mode**: Balanced
   **Changed**: 2025-11-15
   **Independent from**: Scaffolding Level
   ```

2. **Replace framework files**:
   - `flowstate-ai-se-framework-v2.3.2.md` → `flowstate-ai-se-framework-v2.4.0.md`
   - Update TEMPLATES.md, REFERENCE.md, QUICKSTART.md

3. **Verify Meta-Rules**:
   - Confirm FLOWSTATE.md shows "14 Meta-Rules" (was 13)

4. **Test proceed commands**:
   - Say `proceed` after AI completes work
   - Verify Execution Loop appears

**Option B: Fresh Re-initialization** (If you want clean slate)

1. Backup TASKS.md and SESSION.md
2. Remove old FlowState files
3. Run initialization command with v2.4.0
4. Restore backed-up files

**No Breaking Changes**: v2.4.0 is fully backward compatible
- Existing projects continue working with default Balanced quality mode
- Scaffolding system unchanged
- All v2.3.2 Meta-Rules preserved (added Meta-Rule 14)

**Time Required**: ~5 minutes (manual) or ~3 minutes (fresh init)

---

### 🛡️ Backward Compatibility

**Preserved from v2.3.2**:
- ✅ All 13 existing Meta-Rules (numbered 1-13)
- ✅ Scaffolding system (Learner/Growth/Balanced/Expert)
- ✅ Git privacy features
- ✅ Platform adapters (Claude Code, Copilot, Cursor)
- ✅ File structure (FLOWSTATE.md, TASKS.md, SESSION.md)
- ✅ Agent identity system

**Added in v2.4.0**:
- ✅ Meta-Rule 14 (non-breaking addition)
- ✅ Quality Mode system (defaults to Balanced if not configured)
- ✅ Execution Loop (only appears after work done)
- ✅ Proceed commands (optional, user-initiated)

**AI Compatibility**:
- v2.4.0 AI can work with v2.3.2 projects (graceful degradation)
- v2.3.2 AI reading v2.4.0 framework will ignore new sections (no errors)

---

### 📊 Metrics

**File Sizes**:
- Framework: 2,239 lines → 3,008 lines (+769 lines, +34%)
- TEMPLATES.md: 3,047 lines → 3,125 lines (+78 lines, +2.5%)
- REFERENCE.md: 1,869 lines → 2,062 lines (+193 lines, +10%)
- QUICKSTART.md: 693 lines → 754 lines (+61 lines, +9%)

**Total Documentation**: ~9,000 lines (+1,101 lines from v2.3.2)

**New Concepts**: 3 (Quality Modes, Execution Loop, Proceed Commands)

**Valid Configurations**: 36 total (4 scaffolding × 3 quality × 3 phases)

---

### 🔮 What's Next

**Potential v2.5 Features** (User feedback dependent):
- Quality mode presets (e.g., "Production Deploy" = auto-Methodical)
- Task templates with recommended quality modes
- Execution Loop customization (user-defined sections)
- Analytics (time per quality mode, task completion rates)

**Feedback Welcome**:
- Email: abe@flowstateai.dev
- Discord: https://discord.gg/FWx5swdCMK

---

## Version 2.3.2 (2025-11-15)

### 🔄 Major Feature: Automated Upgrade System

This release introduces a comprehensive automated upgrade system that makes version transitions seamless while preserving all user customizations and work.

**Key Innovation**: Single-command upgrade with intelligent preservation and scaffolding integration.

**Target Audience**: Existing FlowState users upgrading from v2.x versions.

---

### ✨ New Features

#### 1. **UPGRADE.md - Complete Upgrade Automation**

**The Problem**: Manual version upgrades were:
- Error-prone (users might miss files or version references)
- Time-consuming (multiple steps, manual file copying)
- Risky (potential to overwrite customizations)
- Unclear (users unsure what gets updated vs preserved)

**The Solution**: Single-prompt automated upgrade with AI-driven process

**Upgrade Command**:
```
I'm upgrading FlowState AI. Please read and execute the upgrade process in UPGRADE.md (located in the flowstate upgrade folder in my project root). Follow all steps and ask me for input when needed.
```

**Key Features**:
- **7-phase upgrade process**: Inventory → Analysis → Scaffolding Config → Upgrade → Scaffolding Execution → Verification → Cleanup
- **Smart preservation**: Automatically detects and preserves TASKS.md, SESSION.md, .flowstate/, and custom configs
- **Version detection**: Identifies current version and determines upgrade path
- **Scaffolding integration**: Configure scaffolding preferences during upgrade (Minimal/Moderate/Comprehensive)
- **Backup checkpoints**: Creates git commit or backup before making changes
- **Error handling**: Stops on errors, preserves user data, provides rollback guidance
- **Auto-cleanup**: Removes temporary upgrade folder after successful upgrade

---

#### 2. **Intelligent Customization Detection**

**During upgrade**, the AI:
- Scans for modified templates in TEMPLATES.md
- Identifies custom configurations in .flowstate/
- Detects user-added files not part of standard framework
- Merges new framework features with existing customizations
- Reports what was preserved and what was updated

---

#### 3. **Scaffolding Preference Integration**

**New in upgrade process**:
- Asks user about scaffolding preferences (Enable/Skip)
- Offers three levels: Minimal, Moderate, Comprehensive
- Option to scaffold immediately or configure for later
- Non-destructive scaffolding (never overwrites existing files)

---

### 🔧 Improvements

#### Documentation
- **UPGRADE.md**: New 300+ line comprehensive upgrade guide with AI protocol
- **README.md**: Added "What's New in v2.3.2" section with upgrade instructions
- **File structure**: Now 7 files (added UPGRADE.md)
- **Total size**: 275KB (up from 251KB in v2.3.1)

#### Version Management
- **File naming**: Framework file now `flowstate-ai-se-framework-v2.3.2.md`
- **Version markers**: Updated all version references in framework files
- **Compatibility**: Supports upgrades from v2.1.x, v2.2.x, v2.3.0, v2.3.1

---

### 📋 Migration Guide: v2.3.1 → v2.3.2

**For Existing Users**:

1. **Download v2.3.2**: Place upgrade folder in project root
2. **Run upgrade command**: Copy-paste the upgrade prompt to your AI
3. **Answer scaffolding questions**: Choose your preferred level or skip
4. **Verify**: Run "FlowState SE" to confirm everything works
5. **Cleanup**: AI will offer to remove temporary upgrade folder

**No Breaking Changes**: v2.3.2 is fully backward compatible with v2.3.1

**Time Required**: ~2-5 minutes (mostly automated)

---

### 🛡️ What's Preserved During Upgrade

**Never Modified**:
- `TASKS.md` (your task list)
- `SESSION.md` (your session logs)
- `.flowstate/` directory (all configs)
- Custom prompts and tools
- User-created files
- Your codebase and project files

**Updated/Replaced**:
- `flowstate-ai-se-framework-v2.3.x.md` → `v2.3.2.md`
- `README.md`, `QUICKSTART.md`, `REFERENCE.md`
- `TEMPLATES.md` (merges new templates with custom ones)
- `TROUBLESHOOTING.md`, `CHANGELOG.md`

**Added**:
- `UPGRADE.md` (new upgrade system)

---

### 📊 File Comparison

**v2.3.1 → v2.3.2**:
- Files: 6 → 7 (+1 UPGRADE.md)
- Total size: 251KB → 275KB (+24KB)
- Framework file: `v2.3.1.md` → `v2.3.2.md`

---

### 🐛 Bug Fixes

- None (this is a feature-additive release)

---

### 📚 Documentation Updates

- **UPGRADE.md**: Complete new file (24KB)
- **README.md**: Added v2.3.2 section, updated file list
- **CHANGELOG.md**: This section

---

### ⚙️ Technical Details

**Upgrade Process Architecture**:
1. **Step 0**: Locate and verify upgrade files
2. **Step 1**: Detect current version and framework location
3. **Step 2**: Inventory and analysis (compare versions)
4. **Step 3**: Scaffolding configuration (user preferences)
5. **Step 4**: Upgrade execution (with preservation)
6. **Step 5**: Scaffolding execution (if requested)
7. **Step 6**: Verification and reporting
8. **Step 7**: Cleanup (remove temp files)

**AI Protocol**: Detailed instructions for AI assistants in UPGRADE.md ensure consistent, safe upgrades

---

### 🎯 Roadmap Impact

**Future Versions**:
- All future releases (v2.3.3+, v2.4+, v3.x) will include UPGRADE.md
- Upgrade system will support multi-version jumps (e.g., v2.2 → v2.4)
- Scaffolding preferences will persist across upgrades

---

## Version 2.3.1 (2025-11-15)

### 🆘 Major Feature: Emergency Recovery & Diagnostics

**The Problem**: FlowState breaks when AI tools update:
- User's Claude/Cursor/Copilot updates → AI loses FlowState awareness
- Framework files intact, but AI can't access them
- No way to diagnose what's broken
- User fears data loss if they "re-initialize"

**The Solution**: TROUBLESHOOTING.md with 7-Phase AI Bootstrap Protocol

**Emergency Command**:
```
Read TROUBLESHOOTING.md and follow its AI instructions to diagnose and restore FlowState SE framework functionality
```

**Key Features**:
- **Preservation Guarantees**: Never overwrites TASKS.md, SESSION.md, or user state
- **Diagnostic Commands**: `FlowState status`, `FlowState doctor`, `Add FlowState to [platform]`
- **Multi-Platform Support**: Works with Claude Code, Cursor, Copilot, Cline
- **Path Diagnostics**: Detects and resolves file access issues
- **Zero Data Loss**: Always preserves user work during recovery

---

## Version 2.3 (2025-11-08)

### 🎓 Major Feature: Scaffolding Levels (Learn to Vibe Code)

This release adds **scaffolding levels** to help users learn AI orchestration and architectural thinking. FlowState can now adjust its teaching style to match your experience level—from maximum teaching for beginners to maximum speed for power users.

**Key Innovation**: Same work quality, different explanation depth. Zero overhead.

**Target Audience Expansion**: Opens FlowState to bootcamp grads, career switchers, junior engineers, and anyone learning to "vibe code" (orchestrate AI effectively).

---

### ✨ New Features

#### 1. **Four Scaffolding Levels** (Step 6.5 in Initialization)

**Learner Mode** - Maximum teaching (3-5x baseline verbosity):
- Explains every orchestration decision in detail
- Teaches architectural patterns and meta-rule application
- Best for: First time using AI assistants for real work
- Response length: 300-500 words

**Growth Mode** [DEFAULT] - Moderate teaching (2x baseline verbosity):
- Explains key strategic decisions
- Occasional teaching moments
- Best for: Comfortable with AI basics, want to level up
- Response length: 150-250 words

**Balanced Mode** - Current FlowState behavior (1x baseline verbosity):
- Explanations only when necessary
- Best for: Experienced with AI orchestration
- Response length: 100-150 words (same as v2.2)

**Expert Mode** - Maximum speed (0.5x baseline verbosity):
- Minimal explanations, action-focused
- Best for: Power users who know FlowState deeply
- Response length: 50-100 words

**Configuration**: Selected during initialization (one question, ~10 seconds)

**Commands**:
```
"Change scaffolding to Learner"   # Switch to maximum teaching
"Change scaffolding to Growth"    # Switch to moderate teaching
"Change scaffolding to Balanced"  # Switch to minimal teaching
"Change scaffolding to Expert"    # Switch to maximum speed
```

---

#### 2. **Vibe Coding Pedagogy**

**Teaching Focus**: Orchestration and architecture, NOT implementation

**What Scaffolding Teaches** (Learner/Growth modes):
- ✅ Task decomposition (how to break down problems)
- ✅ Strategic sequencing (what to do first, why)
- ✅ Meta-rule application (when to follow which rule)
- ✅ Architectural thinking (system design, not just code)

**What Scaffolding Does NOT Teach** (stays focused):
- ❌ Coding syntax or language features
- ❌ Tool selection (which library to use)
- ❌ Algorithm implementations
- ❌ Performance optimization techniques

**SE Edition Teaching** (when in Learner/Growth):
- API design orchestration (RESTful principles, versioning)
- Architecture patterns (MVC, microservices, when to use each)
- Refactoring strategies (when to refactor, how to sequence)
- Testing orchestration (unit vs integration vs e2e)
- Deployment orchestration (CI/CD sequencing)

---

#### 3. **Zero-Overhead Architecture**

**Design Principle**: Same work, different explanation depth

**Implementation**:
- Scaffolding level stored in FLOWSTATE.md (3 lines, ~30 tokens)
- FLOWSTATE.md already read at session start (no additional reads)
- AI checks level before each response (no performance impact)
- Response templates cached in AI working memory

**Performance Impact**: Zero (no speed degradation, no token bloat)

---

#### 4. **Consistency Enforcement**

**AI Instruction Protocol**: AI MUST check scaffolding level BEFORE EVERY RESPONSE

**Consistency Plumbing**:
- Explicit AI instruction in main framework file
- Response templates for 7 common scenarios (all 4 levels)
- Session close reminder of current level
- User can verify with "Check your scaffolding level"

**Testing Criteria**:
- User switches from Growth to Expert → responses immediately 50-70% shorter
- No mixing of levels within a single response
- Teaching commentary present/absent based on level

---

#### 5. **Comprehensive Documentation**

**Added Scaffolding Response Templates** (TEMPLATES.md):
- 7 scenarios showing all 4 levels:
  1. Session Resume
  2. Adding Error Handling
  3. Refactoring for DRY
  4. Investigating a Bug
  5. Planning a Complex Feature
  6. Approaching Stage Gate
  7. Handling Scope Creep
- Each scenario: Learner, Growth, Balanced, Expert examples
- Total: ~900 lines of templates for AI to internalize

**Added Appendix F** (REFERENCE.md):
- Complete scaffolding guide (~350 lines)
- Level descriptions with response characteristics
- SE Edition teaching focus
- Consistency verification guide
- FAQs and testing instructions

---

### 📊 Statistics

#### Documentation Size

| File | v2.2 Lines | v2.3 Lines | Lines Added |
|------|-----------|-----------|-------------|
| Main framework file | 1,656 | 2,026 | +370 |
| TEMPLATES.md | 1,915 | 2,815 | +900 |
| QUICKSTART.md | 602 | 745 | +143 |
| REFERENCE.md | 1,400 | 1,754 | +354 |
| CHANGELOG.md | 541 | 841 | +300 (this section) |
| README.md | 450 | 550 | +100 (estimated) |

**Total Lines Added**: ~2,167 lines across all SE Edition files

#### Key Metrics

- **Scaffolding levels**: 4 (Learner, Growth, Balanced, Expert)
- **Response templates**: 7 scenarios × 4 levels = 28 examples
- **Default level**: Growth (moderate teaching)
- **Time added to init**: ~10 seconds (1 question)
- **Overhead**: Zero (same work, different explanation)

---

### 🔄 Migration Notes

#### Upgrading from v2.2 to v2.3

**For new projects**:
- Initialize with v2.3 → Select scaffolding level during init (Step 6.5)
- Recommendation: Choose **Growth** (default) or **Balanced** (if experienced)

**For existing v2.2 projects**:

**Option A: Continue with v2.2 behavior (no migration)**
- No changes required
- v2.3 AI can work with v2.2 projects
- Scaffolding disabled (effectively Balanced mode)

**Option B: Add scaffolding manually (2 minutes)**
1. Open FLOWSTATE.md
2. Add after "Infrastructure" section:
   ```markdown
   ## Scaffolding Configuration

   **Scaffolding Level**: Growth
   **Changed**: [current date]
   **Teaching Focus**: SE Edition orchestration patterns

   **About Scaffolding Levels**:
   - Change anytime: "Change scaffolding to [Learner/Growth/Balanced/Expert]"
   - See REFERENCE.md § Appendix F for details
   ```
3. Save file
4. Say to AI: "I've updated FLOWSTATE.md with scaffolding configuration. Please acknowledge."

**Option C: Fresh initialization (5-10 minutes)**
1. Back up customizations from FLOWSTATE.md
2. Remove old FlowState files
3. Run: "Read flowstate-ai-se-framework-v2.3.1.md and execute FlowState SE initialization"
4. Select scaffolding level when prompted
5. Restore customizations to new FLOWSTATE.md

**Breaking Changes**: None

**Backward Compatibility**: Full (v2.3 works with v2.2 projects)

---

### 🎯 What's Next

#### Planned for v2.4 (Q2 2026)

**Community Contributions**:
- User-submitted scaffolding response templates
- Industry-specific teaching content (healthcare, finance, etc.)
- Language-specific templates (Go, Rust, Swift)

**Advanced Pedagogy** (Opt-in):
- Socratic mode (ask questions instead of giving answers)
- Pair programming mode (collaborative back-and-forth)
- Review mode (detailed explanations of existing code)

**Analytics** (Anonymous, Opt-in):
- Which scaffolding levels are most popular?
- A/B testing of teaching approaches
- Community feedback loop

---

### 🙏 Acknowledgments

**v2.3 developed by**: Abe Burnett, Mythgate
**Pedagogy consultation**: Claude (Anthropic Sonnet 4.5)
**Testing**: Integrated self-review process + scaffolding consistency validation

**Feedback incorporated from**:
- User request: "Can FlowState help me learn?"
- Market research: Bootcamp grad pain points
- Internal testing: Scaffolding consistency across sessions

---

### 📞 Support & Feedback

**Found an issue?**
- Email: abe@flowstateai.dev
- Discord: https://discord.gg/FWx5swdCMK

**Want to contribute?**
- Scaffolding response templates (new scenarios)
- SE Edition teaching content (API design, testing, deployment patterns)
- Industry-specific examples (healthcare, finance, gaming, etc.)

---

## Version 2.2 (2025-11-08)

### 🔐 Major Feature: Invisible Initialization & Git Privacy

This release adds **invisible initialization** via `.git/info/exclude` and optional filename obfuscation, allowing developers to use FlowState AI in any professional environment without teammates knowing.

**Key Innovation**: FlowState files can now be completely invisible to teammates—no `.gitignore` changes, no repository traces, maximum privacy.

---

### ✨ New Features

#### 1. **Git Privacy Configuration** (Step 5.5 in Initialization)
- **Private Ignore Mode** (default/recommended):
  - Configures `.git/info/exclude` (never committed)
  - FlowState files invisible to teammates
  - No `.gitignore` changes
  - Clean `git status` (files ignored locally)
- **Team Ignore Mode**:
  - Adds patterns to `.gitignore`
  - Team-visible collaboration
  - Shared FlowState configuration
- **Manual/Skip Modes**:
  - User handles git configuration
  - Maximum flexibility

**Use Case**: Developer can use FlowState in corporate environment without revealing AI usage to team or management.

---

#### 2. **Filename Obfuscation** (Optional Privacy Layer)
- **Standard Mode** (default):
  - `FLOWSTATE.md`, `TASKS.md`, `SESSION.md`
  - Clear, recognizable filenames
- **Obfuscated Mode** (extra stealth):
  - `.project-config.md`, `.tasks.md`, `.session-state.md`
  - Generic dotfile names
  - Even if teammates see files in IDE, they don't recognize FlowState

**Filename Mapping**:
```
Standard          →  Obfuscated
FLOWSTATE.md      →  .project-config.md
TASKS.md          →  .tasks.md
SESSION.md        →  .session-state.md
docs/*-master-plan.md  →  docs/.master-plan.md
plans/PLAN-*.md   →  plans/.plan-*.md
logs/*.log        →  logs/.log-*.txt
CLAUDE.md         →  .ai-adapter.md
AGENTS.md         →  .ai-adapter.md
.cursor/rules/flowstate.mdc  →  .cursor/rules/project.mdc
```

---

#### 3. **Privacy Migration Commands**
- **"Make FlowState Visible"**: Convert from private → team mode
- **"Make FlowState Private"**: Convert from team → private mode
- **"Check FlowState git privacy"**: Verify current configuration

**Use Case**: Start with private mode during proof-of-concept, then share with team when ready.

---

#### 4. **Enhanced Initialization Flow**
- Git repository detection (handles submodules, worktrees)
- Two-stage privacy configuration (mode selection, then filename mode)
- Error handling for edge cases (read-only `.git/`, permission denied)
- Success report shows privacy configuration

**Time Added**: ~15 seconds (2 quick questions during initialization)

---

### 🔄 Changes

#### Initialization Protocol
- **Added**: Step 5.5 - Configure Git Privacy (between project detection and strategic questions)
- **Updated**: Step 8 - Create files using filename mode from Step 5.5
- **Updated**: Step 10 - Git commit conditional (skip if private mode)
- **Updated**: Step 11 - Verification checks both filename modes
- **Updated**: Step 12 - Success report shows privacy configuration

#### TEMPLATES.md
- **Added**: `.git/info/exclude` template with standard and obfuscated patterns
- **Added**: Filename modes explanation and mapping table
- **Updated**: All 9 templates support both filename modes
- **Updated**: All cross-references show "X OR Y" format (e.g., "FLOWSTATE.md OR .project-config.md")

#### Documentation
- **QUICKSTART.md**: Added Step 2.5 showing git privacy flow
- **REFERENCE.md**: Added "Git Integration & Privacy" appendix
- **All files**: Version updated to 2.2, date updated to 2025-11-08

---

### 🚫 Breaking Changes

**NONE** - v2.2 is fully backward compatible with v2.1.

- Existing v2.1 projects continue working with no changes required
- Git privacy is optional (only activates if git repository detected)
- Standard filenames remain the default
- All v2.1 commands and workflows unchanged

---

### 📦 Migration Guide: v2.1 → v2.2

#### Option A: Fresh Projects
Just use v2.2 initialization. Git privacy flow happens automatically if git detected.

---

#### Option B: Add Privacy to Existing v2.1 Project

**If you want to make your existing FlowState installation invisible:**

**Step 1**: Say to AI:
```
Configure FlowState private ignore
```

**Step 2**: AI will:
1. Check if `.gitignore` contains FlowState patterns
2. If yes → Remove patterns from `.gitignore`
3. Add patterns to `.git/info/exclude`
4. Verify configuration
5. Prompt you to commit `.gitignore` change

**Step 3**: Commit the .gitignore change (if FlowState was in .gitignore):
```bash
git add .gitignore
git commit -m "Remove FlowState patterns (now using private ignore)"
git push
```

**Result**:
- Your teammates' next `git pull` removes FlowState from `.gitignore`
- FlowState files invisible to teammates (never were in their clones)
- You continue using FlowState normally (files ignored locally)

**Time Required**: 2 minutes

---

#### Option C: Migrate to Obfuscated Filenames (Maximum Stealth)

**If you want to rename files for extra privacy:**

**Step 1**: Backup your current FlowState files (optional safety):
```bash
cp FLOWSTATE.md FLOWSTATE.md.backup
cp TASKS.md TASKS.md.backup
cp SESSION.md SESSION.md.backup
```

**Step 2**: Say to AI:
```
Migrate FlowState to obfuscated mode
```

**Step 3**: AI will:
1. Rename all files (FLOWSTATE.md → .project-config.md, etc.)
2. Update all internal cross-references
3. Configure `.git/info/exclude` with obfuscated patterns
4. Remove FlowState from `.gitignore` (if present)
5. Report success

**Result**:
- All files renamed to generic dotfile names
- All cross-references updated automatically
- Maximum stealth (teammates won't recognize files even in IDE)

**Time Required**: 3-5 minutes

**Risk**: Low (AI verifies all cross-references, but backup recommended)

---

#### Option D: No Migration (Continue with v2.1 Behavior)

**If you're happy with current setup:**

- Do nothing
- v2.2 framework files work with v2.1 projects
- Git privacy features available when you want them
- Use "Make FlowState visible" or "Make FlowState private" anytime

---

### 🔍 Edge Cases Handled

1. **Git Submodules**: `.git` file (not directory) → AI resolves `gitdir:` pointer
2. **Git Worktrees**: Shared git directory → .git/info/exclude applies to all worktrees
3. **Read-Only `.git/`**: Permission denied → AI offers fallback (.gitignore or manual)
4. **Missing `.git/info/exclude`**: File doesn't exist → AI creates it safely
5. **User Deletes `.git/info/exclude`**: Session resume verifies and offers to re-configure

---

### 📊 Comparison: v2.1 vs v2.2

| Feature | v2.1 | v2.2 |
|---------|------|------|
| **Git Privacy** | Manual (user adds to .gitignore) | Automatic (private/team/manual) |
| **Teammate Visibility** | Visible in .gitignore | Invisible (if private mode) |
| **Filename Options** | Standard only | Standard or obfuscated |
| **Privacy Migration** | N/A | "Make Visible" / "Make Private" |
| **Init Time** | 75 seconds | 90 seconds (+15s for git privacy) |
| **Edge Cases** | Not handled | Submodules, worktrees, read-only |
| **Breaking Changes** | From v2.0 | None (fully compatible with v2.1) |

---

### 🎯 Who Should Use v2.2?

**Use v2.2 if you:**
- Work in corporate/team environments
- Want to use FlowState without teammates knowing
- Need maximum privacy for AI-assisted development
- Want flexibility to share FlowState later

**Stick with v2.1 if you:**
- Solo developer (no teammates)
- Team already knows you use AI tools
- Open source project (transparency preferred)
- Don't use git version control

**Note**: v2.2 works great for solo developers too—privacy features simply don't activate if no git detected.

---

### 📚 Additional Resources

- **Privacy Guide**: See main framework § Git Privacy Management
- **Migration Commands**: Listed above in Migration Guide
- **Troubleshooting**: See REFERENCE.md § Git Privacy Edge Cases
- **Examples**: See QUICKSTART.md § Step 2.5

---

## Version 2.1 (2025-10-26)

### 🎉 Major Release: Platform-Agnostic Architecture

This release represents a complete reimagining of FlowState SE based on deep UX analysis and 2025 platform standards research.

---

### ✨ New Features

#### 1. **"FlowState SE" Initialization** (95% Friction Reduction)
- **Before**: 54-line initialization prompt (complex, manual)
- **After**: 2 words: `"FlowState SE"` (automated, instant)
- AI reads framework files and self-configures
- Total initialization time: ~75 seconds

#### 2. **Platform-Agnostic Architecture**
- **Universal Files**: FLOWSTATE.md, TASKS.md, SESSION.md (single source of truth)
- **Platform Adapters**: CLAUDE.md, AGENTS.md, .cursor/rules/*.mdc (integration layer)
- **Standards-Based**: Uses AGENTS.md (2025 standard), .mdc format (Cursor 2025), CLAUDE.md (established convention)
- **Automatic Detection**: AI detects platform and creates appropriate adapters
- **Universal Compatibility**: Create all adapters by default → works on any platform

#### 3. **Comprehensive Agent Identity System**
- **6 Specialized Agents**: Initialization, Execution, Planning, Refactor, Bug Hunt, Session Manager
- **Expert Personas**: Each agent has 10-20 years simulated experience
- **Contextual Activation**: AI switches personas based on task
- **Consistent Behavior**: Same expertise across all platforms
- **Detailed Protocols**: Step-by-step procedures for each agent

#### 4. **5-File Framework Structure** (Following DS Edition Pattern)
- `flowstate-ai-se-framework-v2.1.md` - Main document (philosophy, approach)
- `QUICKSTART.md` - 5-minute onboarding
- `REFERENCE.md` - Detailed Meta-Rules, protocols, troubleshooting
- `TEMPLATES.md` - All document templates
- `CHANGELOG.md` - This file (version history, migration guides)

#### 5. **Reduced Document Count** (7 → 3 Universal Files)
- **FLOWSTATE.md**: Consolidates Master Plan + CLAUDE.md content + Meta-Rules
- **TASKS.md**: Consolidates AGENTS.md + HANDOFF.md + Implementation Alignment
- **SESSION.md**: Replaces CONTEXT-SNAPSHOT.md (improved structure)
- 57% reduction in files to manage

#### 6. **Improved Information Architecture**
- **Progressive Disclosure**: Quick Start → Core Concepts → Advanced → Reference
- **Value Proposition First**: Show "why" before "how"
- **Scannable**: TL;DR boxes, clear sections, decision trees
- **Platform Selection**: Decision tree instead of overwhelming comparison

---

### 🔄 Changed

#### Meta-Rules
- **All 13 Meta-Rules remain** (kept equal as requested)
- **Better organization**: Grouped by theme (Scope, Quality, Risk, Business, Sustainability)
- **Improved examples**: Concrete examples for each rule
- **Language adaptation**: File size caps adapt automatically to detected language

#### Session Management
- **Automated protocols**: AI handles session close automatically
- **Standup summaries**: Auto-generated, copy/paste ready
- **Velocity tracking**: Cumulative stats in SESSION.md
- **Quality metrics**: File sizes, refactor counter, test coverage tracked

#### Platform Support
- **Claude Code**: CLAUDE.md (auto-read at session start)
- **GitHub Copilot**: AGENTS.md (official 2025 standard, auto-read in Agent Mode)
- **Cursor**: .cursor/rules/flowstate.mdc (new 2025 format with frontmatter)
- **OpenAI Codex**: AGENTS.md + @filename syntax support

---

### 🗑️ Removed

- **54-line initialization prompt**: Replaced with "FlowState SE"
- **Manual platform setup**: Now automatic detection
- **HANDOFF.md**: Consolidated into TASKS.md
- **CONTEXT-SNAPSHOT.md**: Replaced with improved SESSION.md
- **Implementation Alignment**: Consolidated into TASKS.md
- **Comprehension Debt Strategy**: Folded into Meta-Rule 13 in FLOWSTATE.md

---

### 🐛 Fixed

- **Initialization UX paradox**: No longer ask user to explain to AI how to read instructions
- **Platform confusion**: Clear decision tree, automatic detection
- **Information overload**: Progressive disclosure, 5-file structure
- **Template accessibility**: Dedicated TEMPLATES.md file
- **Validation gap**: Checklist to verify initialization worked

---

### 📊 Metrics (V2.0 → V2.1)

| Metric | V2.0 | V2.1 | Improvement |
|--------|------|------|-------------|
| Initialization Command | 54 lines | 2 words | 95% reduction |
| Time to Initialize | 5-10 min | 75 sec | 87% faster |
| Framework Files | 1 (2,798 lines) | 5 (~600 lines each) | Better modularity |
| Project Documents | 7 files | 3 universal + adapters | 57% reduction |
| Platform Support | Manual setup | Automatic | Zero config |
| Time to Comprehension | 30+ min | 5 min | 83% faster |

---

## Version 2.0 (2025-10-25)

### Initial Release
- 13 Meta-Rules system
- 7-document architecture
- Manual platform configuration
- Single monolithic framework file (2,798 lines)
- Manual initialization (54-line prompt)

---

## Migration Guide: V2.0 → V2.1

### 📋 Should You Migrate?

**Migrate if:**
- ✅ You want simplified initialization ("FlowState SE" vs 54 lines)
- ✅ You want platform-agnostic setup (works on Claude Code, Copilot, Cursor, Codex)
- ✅ You want agent identities (6 specialized personas for consistent behavior)
- ✅ You want better onboarding (5-minute QUICKSTART vs 30-minute read)
- ✅ You're starting a new project (use V2.1 from day 1)

**Stay on V2.0 if:**
- ⚠️ You're mid-project and V2.0 is working (don't disrupt flow)
- ⚠️ You've heavily customized V2.0 documents (migration requires manual merge)
- ⚠️ Your team is trained on V2.0 (retraining cost > benefit)

**Recommendation**: New projects use V2.1, existing projects evaluate on case-by-case basis.

---

### 🔄 Migration Process (Existing V2.0 Projects)

#### Option A: Fresh Start (Recommended for Small Projects)

**Best for**: Projects <1 month old, <10 completed tasks, 1-2 developers

**Process**:
1. **Archive V2.0 state**:
   ```bash
   mkdir flowstate-v2.0-archive
   mv CLAUDE.md AGENTS.md HANDOFF.md CONTEXT-SNAPSHOT.md docs/implementation-alignment.md flowstate-v2.0-archive/
   ```

2. **Initialize V2.1**:
   ```
   Say to AI: "FlowState SE"
   Answer 5 strategic questions
   ```

3. **Manually transfer active work**:
   - Copy in-progress tasks from old AGENTS.md → new TASKS.md
   - Copy recent completions to new SESSION.md
   - Update new FLOWSTATE.md with any custom rules from old CLAUDE.md

4. **Validate**:
   - Check TASKS.md has all active work
   - Check SESSION.md has current context
   - Check FLOWSTATE.md has your customizations

**Time**: 15-30 minutes

---

#### Option B: Gradual Migration (Recommended for Large Projects)

**Best for**: Projects >1 month old, >10 completed tasks, teams of 3+

**Process**:

**Phase 1: Add V2.1 alongside V2.0** (Week 1)
1. Initialize V2.1 in parallel:
   ```
   Say to AI: "FlowState SE. This is an existing V2.0 project. Create V2.1 files alongside existing ones."
   ```

2. AI creates V2.1 files (FLOWSTATE.md, TASKS.md, SESSION.md, adapters)

3. Both systems coexist:
   - Old V2.0 files: CLAUDE.md, AGENTS.md, HANDOFF.md, CONTEXT-SNAPSHOT.md
   - New V2.1 files: FLOWSTATE.md, TASKS.md, SESSION.md

**Phase 2: Sync Content** (Week 1-2)
4. Manually sync active work:
   ```
   V2.0 AGENTS.md → V2.1 TASKS.md (copy in-progress tasks)
   V2.0 CONTEXT-SNAPSHOT.md → V2.1 SESSION.md (copy active context)
   V2.0 CLAUDE.md → V2.1 FLOWSTATE.md (copy custom rules)
   V2.0 HANDOFF.md → V2.1 TASKS.md (copy status updates)
   ```

5. Keep both updated for 1-2 weeks (overlap period)

**Phase 3: Cutover** (Week 2-3)
6. Stop updating V2.0 files

7. Use only V2.1 files going forward

8. Archive V2.0 files:
   ```bash
   mkdir flowstate-v2.0-archive
   mv CLAUDE.md AGENTS.md HANDOFF.md CONTEXT-SNAPSHOT.md flowstate-v2.0-archive/
   ```

**Time**: 2-3 weeks (gradual transition)

---

#### Option C: Manual Migration (Full Control)

**Best for**: Heavily customized V2.0 setups, specific requirements

**Process**:

1. **Read V2.1 templates** (TEMPLATES.md)

2. **Create new files manually**:
   - FLOWSTATE.md (use template, populate with your project)
   - TASKS.md (use template, copy tasks from old AGENTS.md)
   - SESSION.md (use template, copy context from old CONTEXT-SNAPSHOT.md)

3. **Create platform adapters**:
   - If using Claude Code → Create CLAUDE.md from template
   - If using Copilot/Codex → Create AGENTS.md from template
   - If using Cursor → Create .cursor/rules/flowstate.mdc from template

4. **Test with AI**:
   ```
   Say to AI: "Resume FlowState. Read FLOWSTATE.md, TASKS.md, SESSION.md."
   ```

5. **Validate AI behavior**:
   - Does AI follow Meta-Rules?
   - Does AI update TASKS.md correctly?
   - Does AI generate standup summaries?

**Time**: 1-2 hours

---

### 🔍 Document Mapping (V2.0 → V2.1)

| V2.0 File | V2.1 File | Notes |
|-----------|-----------|-------|
| **Master Plan** | FLOWSTATE.md | Consolidated (Phase definitions + rules) |
| **CLAUDE.md** | FLOWSTATE.md + CLAUDE.md (adapter) | Rules in FLOWSTATE, platform-specific in adapter |
| **AGENTS.md** | TASKS.md + AGENTS.md (adapter) | Task content in TASKS, platform-specific in adapter |
| **HANDOFF.md** | TASKS.md | "What's Working/Broken" → TASKS.md status sections |
| **CONTEXT-SNAPSHOT.md** | SESSION.md | Improved structure, standup summaries |
| **Implementation Alignment** | TASKS.md | Phase tracking in TASKS progress section |
| **Comprehension Debt Strategy** | FLOWSTATE.md | Folded into Meta-Rule 13 |

---

### ⚙️ Custom Rules Migration

**If you customized Meta-Rules in V2.0:**

1. **Identify customizations**:
   - Open old CLAUDE.md
   - Find any sections you modified

2. **Transfer to V2.1 FLOWSTATE.md**:
   - Copy your custom rules
   - Add to appropriate Meta-Rule section
   - Or add as "Project-Specific Context" section

3. **Inform AI**:
   ```
   Say: "I've customized Meta-Rule [N] in FLOWSTATE.md. Please follow the updated version."
   ```

---

### 🧪 Testing Your Migration

**After migration, verify:**

- [ ] **Initialization test**:
  - [ ] Say "Resume FlowState"
  - [ ] AI reads FLOWSTATE.md, TASKS.md, SESSION.md
  - [ ] AI reports current phase and status correctly

- [ ] **Task execution test**:
  - [ ] Request a small feature
  - [ ] AI follows Meta-Rules
  - [ ] AI updates TASKS.md
  - [ ] AI creates evidence log in logs/

- [ ] **Session close test**:
  - [ ] Say "Done for today"
  - [ ] AI updates SESSION.md
  - [ ] AI generates standup summary
  - [ ] Standup summary is copy/paste ready

- [ ] **Platform adapter test** (if applicable):
  - [ ] Check CLAUDE.md / AGENTS.md / .cursor/rules/*.mdc exists
  - [ ] Adapter references FLOWSTATE.md, TASKS.md, SESSION.md
  - [ ] Platform reads adapter automatically (or with @filename)

---

### 🆘 Migration Troubleshooting

#### Issue: AI doesn't recognize V2.1 files

**Solution**:
```
Say: "Initialize FlowState SE. Read FLOWSTATE.md, TASKS.md, and SESSION.md for context."
```

---

#### Issue: V2.0 and V2.1 files conflict

**Solution**:
```
Option 1: Archive V2.0 files immediately
Option 2: Prefix V2.0 files with "v2.0-" to distinguish
```

---

#### Issue: Lost custom rules during migration

**Solution**:
```
1. Check flowstate-v2.0-archive/ for old CLAUDE.md
2. Copy custom sections
3. Add to V2.1 FLOWSTATE.md
4. Inform AI of changes
```

---

#### Issue: AI uses wrong file (old AGENTS.md instead of new TASKS.md)

**Solution**:
```
Say: "Use the new V2.1 files: FLOWSTATE.md for rules, TASKS.md for tasks, SESSION.md for context. Ignore old V2.0 files."
```

---

## Breaking Changes

### V2.0 → V2.1

**File Structure**:
- **Removed**: HANDOFF.md, CONTEXT-SNAPSHOT.md, Implementation Alignment, Comprehension Debt Strategy
- **Added**: 5-file framework structure (main, QUICKSTART, REFERENCE, TEMPLATES, CHANGELOG)
- **Changed**: Document names (AGENTS.md split into content [TASKS.md] + adapter [AGENTS.md])

**Initialization**:
- **Removed**: 54-line initialization prompt
- **Added**: "FlowState SE" command (2 words)

**Platform Support**:
- **Changed**: Manual setup → Automatic detection
- **Added**: Platform adapters (CLAUDE.md, AGENTS.md, .cursor/rules/*.mdc)

**Agent System**:
- **Added**: 6 specialized agent identities with detailed protocols
- **Changed**: AI behavior now switches personas based on context

---

## Deprecations

### V2.1 Deprecations

- **None** (V2.1 is fully supported, no planned deprecations)

### V2.0 Deprecations

- **V2.0 framework file** (`flowstate-ai-se-framework-v2.md`) → Archived as `flowstate-ai-se-framework-v2.0-ARCHIVE.md`
- **V2.0 document structure** (7 files) → Use V2.1 (3 universal + adapters)
- **54-line initialization prompt** → Use "FlowState SE"

**Support Timeline**:
- V2.0 archived 2025-10-26 (still accessible, but not actively developed)
- V2.1 is current version (active development, support, improvements)

---

## Roadmap

### V2.2 (Released: 2025-11-08)

**Potential Features**:
- **Team Scaling**: Multi-developer coordination (task assignment, parallel work)
- **Advanced Metrics**: Velocity dashboards, burn-down charts
- **AI Learning**: Framework learns from your patterns (suggest personalized optimizations)
- **Integration**: GitHub Issues, Linear, Jira sync
- **VS Code Extension**: Native integration for Copilot/Codex

**Not Committed** (ideas under consideration):
- Real-time collaboration (multiple AIs on same project)
- FlowState Cloud (centralized state management)
- Language-specific variants (FlowState Rust, FlowState Swift)

---

## FAQ

### Q: Can I use V2.0 and V2.1 on the same project?

**A**: Yes, during migration (Option B). Both can coexist for 1-2 weeks. After cutover, archive V2.0 files and use only V2.1.

---

### Q: Will V2.0 get updates?

**A**: No. V2.0 is archived as of 2025-10-26. All future development is on V2.1. Critical security fixes only for V2.0.

---

### Q: Do I need to migrate immediately?

**A**: No. V2.0 still works. Migrate when convenient (new project, natural break point, team onboarding).

---

### Q: What if I can't use V2.1 features (e.g., no platform adapter support)?

**A**: V2.1 gracefully degrades. You can use universal files (FLOWSTATE.md, TASKS.md, SESSION.md) manually without adapters. AI just won't auto-read on session start.

---

### Q: Can I customize V2.1 like I did V2.0?

**A**: Yes. Edit FLOWSTATE.md for rules, TASKS.md for workflows, SESSION.md for tracking. Templates in TEMPLATES.md are starting points, not rigid requirements.

---

### Q: Will migrating break my project?

**A**: No. FlowState is documentation + AI guidance. Migrating just changes which files AI reads. Your code is unchanged. Worst case: Revert to V2.0 files.

---

## Support

**For migration help:**
- Email: abe@flowstateai.dev
- Discord: https://discord.gg/FWx5swdCMK
- GitHub Issues: (if applicable)

**For bug reports:**
- Describe: V2.0 → V2.1 migration step that failed
- Include: Error messages, unexpected behavior
- We'll help troubleshoot

---

**Version**: 2.5.0
**Last Updated**: 2025-11-24
**Framework Created By**: Abe Burnett, Mythgate

---

*Thank you for using FlowState. Ship smart, ship fast, ship sustainable.* 🚀
---

## Maintainer Appendix: Version Consistency Checklist (v2.5)

Run these from the repo root to catch drift in SE v2.5 files.

- Version banners not set to 2.5
  `rg -n --pcre2 '^\*\*Version\*\*:\s*(?!2\.5\b)2\.\d+' releases/se-edition/flowstate-ai-se-v2.5-release`

- Released date not set to 2025-11-24
  `rg -n --pcre2 '^\*\*Released\*\*:\s*(?!2025-11-24\b)\d{4}-\d{2}-\d{2}' releases/se-edition/flowstate-ai-se-v2.5-release`

- Legacy framework filename self-references
  `rg -n 'flowstate-ai-se-framework-v2(?!\\.5)\\.\w*' releases/se-edition/flowstate-ai-se-v2.5-release`

- Old initialization banners/commit samples
  `rg -n --pcre2 '(Initialized|Initialize FlowState AI Framework SE) v2\.(0|1|2|3|4)' releases/se-edition/flowstate-ai-se-v2.5-release`

- Discord invite not on current URL
  `rg -n 'discord\.gg/(?!FWx5swdCMK)\S+' releases/se-edition/flowstate-ai-se-v2.5-release`
