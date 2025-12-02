# FlowState AI Framework SE - Upgrade Guide

> **📦 Upgrading from a Previous Version?**
> Use this file if you have a **pre-existing FlowState AI v2.x installation**.
> For fresh installations, see [QUICKSTART.md](./QUICKSTART.md) instead.

---

## Quick Start - Upgrade Prompt

**Before running**: Place the v2.5.0 upgrade files in a folder in your project root. Use one of these names:
- `flowstate-v2.5.0-se/` (recommended)
- `flowstate-upgrade/`
- `flowstate-se-v2.5.0/`

**Copy and paste this prompt to your AI assistant:**

```
I'm upgrading FlowState AI SE to v2.5.0. The upgrade files are in [FOLDER NAME] in my project root. Please:
1. Read UPGRADE.md from that folder
2. Execute the upgrade process starting at Step 0
3. Ask me for input when needed

If you can't find the folder, search for "UPGRADE.md" in my project root directories.
```

**Example** (if your folder is named `flowstate-upgrade`):
```
I'm upgrading FlowState AI SE to v2.5.0. The upgrade files are in flowstate-upgrade/ in my project root. Please read UPGRADE.md from that folder and execute the upgrade process starting at Step 0.
```

---

## 🎯 What's Now Possible (v2.5.0)

Before diving into the upgrade process, here's what you'll be able to do after upgrading:

---

### 🎓 Learn While You Build

**Before v2.5**: You either knew the tech stack or struggled in silence. The AI assumed you knew everything.

**Now**: Set your **Concept Level** and the AI teaches you ~1 concept per session as you work. Learning Flutter? It'll explain widgets, state management, and navigation patterns naturally as they come up—without slowing you down.

**Try it after upgrading**:
- `"Change concept level to Novice"` — Maximum teaching (new technology)
- `"Change concept level to Apprentice"` — Gradual teaching (default)
- `"Change concept level to Fluent"` — No teaching (you're an expert)

---

### 🔄 Catch Up After Working Offline

**Before v2.5**: If you coded without FlowState (used a different AI, worked offline, quick-fixed something), your task list drifted out of sync. Re-syncing was manual and tedious.

**Now**: Say **"FlowState sync"** and the AI:
1. Scans your git changes since last session
2. Matches changes to your task list
3. Asks what to mark as done
4. Suggests what to work on next

**Try it after upgrading**:
- `"Sync up"` or `"Catch up"` or `"I did work without you"`
- The AI will walk you through reconciliation

---

### 📦 Find Old Decisions and Completed Work

**Before v2.5**: Completed tasks piled up at the bottom of TASKS.md. Finding how you implemented something months ago meant scrolling through noise.

**Now**: Tasks **auto-archive** after phase transitions. Search your history with natural language.

**Try it after upgrading**:
- `"FlowState find task authentication"` — Find how you implemented auth
- `"Find task API"` — Find API-related completed work
- `"Search archived tasks for database"` — Search the archive

---

### 📁 Cleaner Project Root

**Before v2.5**: FLOWSTATE.md, TASKS.md, SESSION.md cluttered your project root alongside your actual README.md.

**Now**: Everything lives in **`.flowstate/`** by default:
```
.flowstate/
├── config.md (was FLOWSTATE.md)
├── tasks.md
├── session.md
├── archive/
└── ...
```

**During upgrade**: You'll be asked if you want to migrate to the new structure or keep root-level files.

---

### 🆘 Get Unstuck with Guided Debugging

**Before v2.5**: When stuck, you either asked the AI to "just fix it" (learned nothing) or struggled alone.

**Now**: **Learner MAX** mode offers three paths when you're stuck:
- **"Just fix it"** — AI solves it, explains briefly
- **"Walk me through"** — AI asks guiding questions, you solve it
- **"Explain first"** — AI teaches the concept, then you apply it

**Try it after upgrading**:
- Wait until you hit a bug, then see if the AI offers Learner MAX
- Or say `"Learner MAX"` to activate it manually

---

### 📈 See Your Progress at a Glance

**Before v2.5**: Progress tracking was buried. You had to dig through SESSION.md to understand velocity.

**Now**: **Velocity metrics** appear at the TOP of session.md:
- Tasks completed this week
- Phase completion estimates
- Bottleneck detection

**Try it after upgrading**:
- Open `.flowstate/session.md` and see the new header
- Say `"How am I doing?"` for a progress summary

---

### ✅ Verify Everything Worked

**Before v2.5**: If initialization failed silently (e.g., a file wasn't created), you'd only discover it later when something broke.

**Now**: The **`FlowState verify`** command lets you check that all files exist and are valid anytime.

**Try it after upgrading**:
- `"FlowState verify"` or `"FS verify"` or `"Check FlowState files"`
- You'll see a verification report showing ✅ or ❌ for each file

---

### 🚀 Quick Reference: New Commands to Try

| Command | What it does |
|---------|--------------|
| `FlowState sync` | Reconcile after working offline |
| `FlowState verify` | Check all FlowState files exist |
| `FlowState find task [query]` | Search archived tasks |
| `FlowState handoff` | Generate context for another dev/AI |
| `Change concept level to [level]` | Adjust teaching depth |
| `Learner MAX` | Activate guided problem-solving |

---

*Ready to upgrade? Continue to the next section for the upgrade process.*

---

## What This Upgrade Does

**Version**: v2.4.x → v2.5.0
**Release Date**: 2025-11-24
**Type**: Feature update (CCT + Sync Protocol + .flowstate/ directory) with enhanced upgrade tooling

### Key Changes in v2.5.0
- **New**: Contextual Concept Teaching (CCT) - teaches language/framework/library concepts
- **New**: Learner MAX Mode - guided problem-solving
- **New**: FlowState Sync Protocol - reconcile state after off-reservation work
- **New**: `.flowstate/` directory structure (new default)
- **New**: Task Archival System (ARCHIVED-TASKS.md)
- **New**: Proactive Knowledge Currency Protocol
- **New**: Velocity Metrics at top of SESSION.md
- **New**: Handoff Generation Protocol
- **New**: Phase Retrospectives
- **Preserved**: Automated upgrade system from v2.3.2 (7-phase workflow, customization preservation)

### What Gets Updated
- All framework core files (`flowstate-ai-se-framework-v2.5.0.md`, `REFERENCE.md`, etc.)
- Documentation files (`README.md`, `QUICKSTART.md`, `TEMPLATES.md`, `TROUBLESHOOTING.md`)
- Version metadata and changelogs

### What Stays Unchanged
- Your `TASKS.md` (task list)
- Your `SESSION.md` (session logs)
- Your `.flowstate/` directory and all configurations
- Any custom prompts, tools, or integrations you've created
- Your project files and codebase

---

## Version Compatibility

This upgrade process supports upgrading from:
- ✅ v2.4.x → v2.5.0 (recommended path)
- ✅ v2.3.0 → v2.5.0
- ✅ v2.3.1 → v2.5.0
- ✅ v2.3.2 → v2.5.0
- ✅ v2.2.x → v2.5.0 (with compatibility notes)
- ✅ v2.1.x → v2.5.0 (with breaking change warnings)

**Note**: If upgrading from v2.0.x or earlier, please review the [CHANGELOG.md](./CHANGELOG.md) for breaking changes.

---

## 📋 Configurable Features by Version (SE Edition)

This section lists all configurable features and when they were introduced.  
During upgrade, you'll only be asked about features that are **new since your current version**.

### v2.5.0 (2025-11-24)

#### Concept Level [CONFIGURABLE] [NEW]

**What it does**: Adjusts how much AI teaches language/framework/library concepts, separate from orchestration scaffolding.

**Best for**:
- Novice: Learning a completely new technology from scratch
- Apprentice: Basic familiarity, still building fluency
- Practitioner: Comfortable with fundamentals, only need advanced concepts
- Fluent: Deep expertise, no teaching needed

**Where stored**: `.flowstate/config.md` § `Concept Learning Configuration`
**Detection marker**: `## 📚 Concept Learning Configuration`
**Default**: Apprentice
**Options**: Novice | Apprentice | Practitioner | Fluent

**User Prompt**:
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
CONCEPT LEVEL SELECTION [NEW in v2.5]

Concept Levels control how much I teach language/framework/library concepts.
This is INDEPENDENT from Scaffolding (which controls AI orchestration teaching).

Select your starting level:

[1] Novice     - Maximum concept teaching, explain everything
                (Best for: Technologies you've never used)

[2] Apprentice - Moderate teaching, gradual introduction [DEFAULT]
                (Best for: Basic familiarity, still learning)

[3] Practitioner - Minimal teaching, advanced concepts only
                  (Best for: Comfortable with fundamentals)

[4] Fluent     - No teaching, full technical vocabulary
                (Best for: Deep expertise in this technology)

You can set different levels per technology later.
Change anytime by saying "Change concept level to [level]"
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Your choice [1/2/3/4]: _
```

---

#### .flowstate/ Directory Structure [CONFIGURABLE] [NEW]

**What it does**: Moves all FlowState files to a dedicated `.flowstate/` directory for cleaner project organization.

**Where stored**: Directory location itself
**Detection marker**: Presence of `.flowstate/` directory vs root-level files
**Default**: `.flowstate/` directory (new in v2.5)
**Options**: `.flowstate/` directory (new default) | Root level (legacy)

**Migration Note**: Existing users upgrading from v2.4 can keep root-level files or migrate to `.flowstate/`. The upgrade process will offer this choice.

**New Directory Structure**:
```
.flowstate/
├── config.md (was FLOWSTATE.md)
├── tasks.md (was TASKS.md)
├── session.md (was SESSION.md)
├── archive/
│   └── tasks-archive.md
├── plans/
├── logs/
└── version.txt
```

---

#### Velocity Metrics [CONFIGURABLE] [NEW]

**What it does**: Adds progress analytics to the top of SESSION.md.

**Where stored**: `.flowstate/session.md` header
**Detection marker**: `## 📈 Velocity & Progress`
**Default**: Enabled
**Options**: Enabled (opt-out available) | Disabled

---

### v2.4.0 (2025-11-15)

#### Quality Mode [CONFIGURABLE]

**What it does**: Adjusts **work rigor** (validation + documentation) independently from scaffolding (teaching verbosity).

**Best for**:
- Fast: Rapid prototyping, quick iterations, exploratory work
- Balanced: Normal development, most team projects
- Methodical: Production APIs, complex systems, security‑sensitive or mission‑critical work

**Where stored**: `FLOWSTATE.md` § `Quality Mode Configuration`  
**Detection marker**: `## 🎯 Quality Mode Configuration`  
**Default**: Balanced  
**Options**: Fast \| Balanced \| Methodical

**User Prompt**:
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
QUALITY MODE SELECTION [NEW in v2.4]

Quality Mode controls the rigor and thoroughness of your work.
This is INDEPENDENT from Scaffolding Level (which controls explanations).

Select your preferred mode:

[1] Fast      - Minimal ceremony, quick iteration
               (Best for: Prototyping, exploration, quick demos)

[2] Balanced  - Standard rigor [RECOMMENDED]
               (Best for: Normal development, most projects)

[3] Methodical - Maximum thoroughness
                (Best for: Production APIs, critical systems, deployments)

You can change this anytime by saying "Change quality mode to [mode]"
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Your choice [1/2/3]: _
```

**SE-Specific Context**:
- Fast: Code only, defer comprehensive tests and docs
- Balanced: Code + tests + essential docs (API/contracts)
- Methodical: Code + comprehensive tests + full docs + deployment readiness + security review

---

### v2.3.0 (2025-11-08)

#### Scaffolding Levels [CONFIGURABLE]

**What it does**: Adjusts AI response verbosity and teaching style to match your experience with AI orchestration.

**Best for**:
- Learner: First time using AI assistants for real development work
- Growth: Comfortable with AI basics, want to level up orchestration skills
- Balanced: Experienced with AI‑assisted development
- Expert: Power users who know FlowState deeply, want maximum speed

**Where stored**: `FLOWSTATE.md` § `Scaffolding Configuration`  
**Detection marker**: `## 🎓 Scaffolding Configuration`  
**Default**: Growth  
**Options**: Learner \| Growth \| Balanced \| Expert

**User Prompt**:
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SCAFFOLDING LEVEL SELECTION

FlowState can adjust its teaching style to match your experience with
AI orchestration (directing and collaborating with AI assistants).

This is NOT about coding skill—it's about learning to "vibe code"
(orchestrate AI, think architecturally, decompose problems).

Select your preferred level:

[1] Learner   - Maximum teaching, explain every decision
               (Best for: First time using AI assistants for real work)

[2] Growth    - Moderate teaching, explain key decisions [RECOMMENDED]
               (Best for: Comfortable with AI basics, want to level up)

[3] Balanced  - Minimal teaching, explanations when needed
               (Best for: Experienced with AI orchestration)

[4] Expert    - No teaching, maximum speed
               (Best for: Power users who know FlowState deeply)

You can change this anytime by saying "Change scaffolding to [level]"
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Your choice [1/2/3/4]: _
```

**SE-Specific Teaching Focus** (Learner/Growth):
- API design orchestration (REST, versioning strategies)
- Architecture patterns (monolith vs services, when to split)
- Refactoring strategies (when to refactor, how to stage changes)
- Testing strategies (unit vs integration vs e2e, coverage decisions)
- Deployment orchestration (CI/CD sequencing)

---

### v2.2.0 (2025-11-08)

#### Privacy Controls [CONFIGURABLE]

**What it does**: Configures git integration and optional filename obfuscation for FlowState files.

**Best for**:
- Private: Solo developers; teammates shouldn’t see FlowState files
- Team: Teams sharing FlowState configuration via `.gitignore`
- Manual: Advanced users who want full manual control
- Skip: Not using git or will configure later

**Where stored**: `FLOWSTATE.md` § `Privacy Configuration`  
**Detection marker**: `## 🔒 Privacy Configuration`  
**Default**: Private with standard filenames  
**Options**: Private \| Team \| Manual \| Skip (+ filename obfuscation sub‑choice)

**User Prompt**:
```
✅ Git repository detected.

FlowState creates working files that should not be committed to version control.

How would you like to handle git integration?

[1] Private ignore (teammates can't see) [RECOMMENDED]
    • Configures .git/info/exclude (never committed)
    • FlowState files invisible to teammates
    • No .gitignore changes

[2] Team ignore (visible in .gitignore)
    • Adds FlowState patterns to .gitignore
    • Team sees "flowstate" patterns in .gitignore
    • Shared team configuration

[3] Manual (you handle git yourself)
    • No automatic configuration
    • You manage version control

[4] Skip (no git configuration)
    • FlowState files may appear in git status
    • You'll need to ignore them manually later

Choice [1/2/3/4]: _
```

**Follow-up prompt** (if user chooses [1] Private):
```
Would you like obfuscated filenames for extra privacy?

Standard mode:    FLOWSTATE.md, TASKS.md, SESSION.md
Obfuscated mode:  .project-config.md, .tasks.md, .session-state.md

Obfuscated filenames prevent teammates from recognizing FlowState
even if they see the files in your IDE file explorer.

Use obfuscated filenames? [y/N]: _
```

**SE-Specific Context**:
- Most solo developers choose Private + standard filenames
- Teams typically choose Team ignore
- Obfuscation is useful in competitive or stealth project environments

---

## For AI Assistants: Upgrade Process

**IMPORTANT**: When a user runs the upgrade prompt above, follow this protocol exactly.

Before executing any numbered step (0–7), re-open this `UPGRADE.md` file and re-read the instructions for that specific step. Do not rely solely on previous conversation history or summaries.

### Smart Upgrade Rules for AI Assistants

When performing an upgrade, follow these rules:

1. **Never reconstruct files from memory (S1)**  
   Always open and read the actual files on disk (both the user's current files and the new files in the upgrade folder). Do not rewrite entire files based only on your own summaries.

2. **Prefer atomic replacement over manual edits (S2)**  
   For framework-owned, non-customized files, replace the entire file with the new version instead of performing line-by-line edits.

3. **Use a diff to choose strategy (S3)**  
   Compare old vs new file contents:
   - If differences are only version numbers, dates, or obvious metadata → treat as **uncustomized** and use full-file replacement.
   - If there are substantive content differences → treat as **customized** and use the file-specific merge rules below.

4. **Operate at section/block granularity (S4)**  
   When merging, anchor on markdown headings or clearly marked blocks. Copy or insert whole sections/blocks rather than editing individual sentences inside user-owned areas.

5. **User files are additive-only (S5)**  
   For user-owned files like `FLOWSTATE.md`, `TASKS.md`, `SESSION.md`, project code, and docs:
   - Never delete or overwrite existing user content.
   - Only insert new sections (e.g., new configuration blocks), and only when the corresponding section header is missing.

6. **Always be idempotent (S6)**  
   Assume steps may be re-run after interruptions or context compaction. Design your actions so re-running Step 4 or Step 5 never creates duplicates, corrupts files, or regresses behavior.

7. **Ask on ambiguous customization (S7)**  
   If you are unsure whether a file is customized, show a brief diff summary and ask the user whether to:
   - Keep their version,
   - Replace with the new standard version, or
   - Merge specific custom blocks into the new version.

Additionally, this upgrade process uses a per-project state file:

- **Upgrade state file**: `UPGRADE-STATE.md` in the project root.
  - Treat this as the source of truth for which steps have completed and what configuration choices the user made.
  - At the beginning of any step, if `UPGRADE-STATE.md` exists, read it and resume from the first step whose status is not `completed`.
  - If it does not exist at Step 0, create it and initialize all steps (0–7) as `pending`.
  - After completing each step, update `UPGRADE-STATE.md` to mark that step as `completed` and record any new information (such as feature choices).

### Step 0: Locate and Verify Upgrade Files

1. **Find the upgrade folder**: Look for a folder in the project root containing this `UPGRADE.md` file
   - Common names: `flowstate-v2.5.0-se`, `flowstate-upgrade`, `flowstate-se-v2.5.0`
   - If multiple folders found, ask user which to use

2. **Verify upgrade folder contents**: Ensure these files exist in the upgrade folder:
   - `UPGRADE.md` (this file)
   - `flowstate-ai-se-framework-v2.5.0.md`
   - `README.md`
   - `QUICKSTART.md`
   - `REFERENCE.md`
   - `TEMPLATES.md`
   - `TROUBLESHOOTING.md`
   - `CHANGELOG.md`

3. **Initialize or update `UPGRADE-STATE.md`**:
   - Check if `UPGRADE-STATE.md` exists in the project root.
   - If it exists:
     - Read it and determine which steps (0–7) are already marked as `completed`.
   - If it does not exist:
     - Create a new `UPGRADE-STATE.md` with:
       - Edition, from-version (if known), to-version (`2.5.0`).
       - A list of steps (0–7) all marked `pending`.
       - An empty `New Feature Choices` section to be filled in during Step 3.5.

4. **Ensure upgrade folder is private in git (Private mode only)**:
   - If you detect that the project is using **Private Ignore** git mode (from `FLOWSTATE.md` Privacy Configuration) and you are able to modify `.git/info/exclude`:
     - Append the detected upgrade folder path (e.g., `flowstate-v2.5.0-se/`) to `.git/info/exclude`, creating the file if needed.
   - This ensures the temporary upgrade folder stays hidden from `git status` in private mode.

5. **If files missing**: Alert user and stop upgrade process

---

### Step 1: Detect Current Version and Framework Location

1. **Look for version markers** (in order of preference):
   - Check for `.flowstate/version.txt`
   - Look for `flowstate-ai-se-framework-v*.md` in project root or common locations
   - Check `TASKS.md` header for version reference
   - Scan for framework files with version numbers in filename

2. **Determine current version**:
   - Extract version number from findings
   - If uncertain, ask user: "I detected version X.X.X, is this correct?"

3. **Locate framework installation**:
   - Find where current framework files are located
   - Common locations: project root, `.flowstate/`, `docs/flowstate/`
   - Ask user to confirm location if multiple possibilities exist

4. **Report findings to user**:
   ```
   Upgrade Summary:
   - Current version: vX.X.X
   - Target version: v2.5.0
   - Framework location: [path]
   - Upgrade folder: [path]

   Ready to proceed with upgrade analysis.
   ```

5. **Detect filename mode and canonical core files**:
   - Check for standard vs obfuscated filenames for core state:
     - Standard: `FLOWSTATE.md`, `TASKS.md`, `SESSION.md`
     - Obfuscated: `.project-config.md`, `.tasks.md`, `.session-state.md`
   - Set `filename_mode` logically as:
     - `"standard"` if standard files exist (even if obfuscated do not).
     - `"obfuscated"` if obfuscated files exist (even if standard do not).
   - Treat whichever set exists as the **canonical** core files for this project.
   - Throughout the remainder of this upgrade:
     - Do **not** treat the absence of the other naming convention as "missing" or "partially initialized".
     - Never recreate core files under the other naming convention if one set already exists.

---

### Step 2: Inventory and Analysis Phase

1. **Compare files between versions**:
   - List all files in upgrade folder
   - Compare with files in current framework location
   - Identify: new files, updated files, unchanged files, deprecated files

2. **Detect customizations**:
   - Look for signs of user modifications:
     - Custom sections in `TASKS.md`
     - Modified templates in `TEMPLATES.md`
     - Custom configurations in `.flowstate/`
     - User-added files (not part of standard framework)

3. **Generate comparison report** and show to user:
   ```
   Upgrade Analysis Report
   =======================

   Files to be updated: [list with brief description of changes]
   New files to be added: [list]
   Files to be preserved: [list of user files]
   Detected customizations: [list any custom modifications found]

   Estimated upgrade time: ~X minutes
   Risk level: Low (standard framework update)
   ```

4. **Wait for user acknowledgment** before proceeding

---

### Step 3: Scaffolding Configuration (NEW in v2.3.2)

**Before applying the upgrade**, ask the user about scaffolding preferences:

1. **Ask about scaffolding**:
   ```
   FlowState v2.3.2+ includes an improved scaffolding system. Would you like to:

   A) Enable scaffolding and configure it now
   B) Skip scaffolding configuration (you can enable it later)

   What's your preference? (A/B)
   ```

2. **If user chooses A**, ask about scaffolding level:
   ```
   Which scaffolding level would you prefer?

   1. Minimal: Basic project structure only (directories, core config files)
      - Use if: You have an established project structure

   2. Moderate: Standard setup (Minimal + common utilities, basic docs, testing setup)
      - Use if: You want standardized tooling without too much overhead
      - RECOMMENDED for most projects

   3. Comprehensive: Full framework (Moderate + advanced features, complete docs, examples, CI/CD)
      - Use if: Starting a new project or want complete FlowState integration

   Which level? (1/2/3)
   ```

3. **Ask about execution timing**:
   ```
   When should I run scaffolding?

   A) Run immediately after upgrade completes
   B) Just configure it, I'll run it manually later

   What's your preference? (A/B)
   ```

4. **Record preferences** for use in Step 5

---

### Step 3.5: New Features Discovery & Configuration [NEW]

**Purpose**: Detect which configurable features the user doesn't have yet and offer to configure them **before** applying the upgrade.

**Process**:

1. **Read user's existing FLOWSTATE.md**:
   - Determine filename based on privacy mode (if known):
     - Standard: `FLOWSTATE.md`
     - Obfuscated: `.project-config.md`
   - If unsure, try `FLOWSTATE.md` first, then `.project-config.md`. If both fail, ask the user which file to use.
   - Read the selected file into memory.
   - Extract current version (if present) from a line like:
     - `**Current Version**: X.Y.Z` or `**Version**: X.Y.Z`
   - Extract all section headers (lines starting with `##`).

2. **Parse "Configurable Features by Version"** (earlier in this `UPGRADE.md`):
   - Treat the `📋 Configurable Features by Version (SE Edition)` section as the **feature catalog**.
   - For each `### v[X.Y.Z]` block:
     - Record the version and any `#### [Feature Name] [CONFIGURABLE]` entries.
   - Build a list of configurable features introduced **after the user's current version** (if version is unknown, treat all catalog entries as candidates).

3. **Check which features are already configured**:
   - For each candidate feature:
     - Look for its `Detection marker` header (or equivalent text) in the extracted `##` section headers.
     - Use flexible matching so that emoji differences or minor text changes still count as “configured”.
   - If a feature’s configuration section appears to exist:
     - Treat it as configured and **do not overwrite** the user’s content.
   - If the section is missing:
     - Add the feature to the **missing features** list to be surfaced.

4. **Present missing features to the user**:

   - **If no missing features**:
     ```
     ✅ No new configurable features since v[USER_VERSION]

     All current features are already configured in your FLOWSTATE.md.
     Proceeding with framework file updates...
     ```

   - **If one or more features are missing**:
     - Explain what you found and that you’ll walk through configuration:
       ```
       You're upgrading from v[USER_VERSION] → v[NEW_VERSION].

       I found [N] new configurable feature(s) since v[USER_VERSION]
       that are not yet configured in your FLOWSTATE.md.

       I can either:
       A) Apply recommended defaults for these features, or
       B) Walk you through each feature with detailed explanations.

       A) Recommended defaults:
          - Privacy Controls: Private (standard filenames), .git/info/exclude mode
          - Scaffolding Levels: Growth
          - Quality Mode: Balanced

       B) Detailed configuration:
          - I'll show you each feature's description and options
            and ask for your choices one by one.

       What's your preference? (A/B)
       ```
     - If the user chooses **A** (recommended defaults):
       - Use the defaults documented in the "Configurable Features by Version (SE Edition)" section.
       - Record these choices directly into `UPGRADE-STATE.md` under `New Feature Choices`.
       - Show a brief summary of the applied defaults and proceed to Step 4.
     - If the user chooses **B**:
       - For each missing feature:
         - Show its name, version introduced, short description, and **User Prompt** text from the catalog.
         - Collect the user’s choice (respecting documented defaults if they explicitly request them).

5. **Record user's choices in `UPGRADE-STATE.md`**:
   - Build a logical map such as:
     - `new_feature_configurations = { "Privacy Controls": choice, "Scaffolding Levels": choice, "Quality Mode": choice }`
   - Write this map into `UPGRADE-STATE.md` under a `New Feature Choices` section so that it can be reliably read later, even if the conversation is compacted.

6. **Confirm configuration summary**:
   ```
   ✅ New feature configuration complete:
     - Privacy Controls: [choice or “already configured”]
     - Scaffolding Levels: [choice or “already configured”]
     - Quality Mode: [choice or “already configured”]

   These settings will be written into your FLOWSTATE.md during the upgrade.
   Proceeding to Step 4: Upgrade Execution...
   ```

**Error Handling**:
- If you cannot read `FLOWSTATE.md` (or equivalent):
  - Warn the user, ask them to confirm the correct path, and retry.
- If version cannot be detected:
  - Ask the user: “What version are you currently on?” and proceed using that value.
- If the user provides an invalid choice:
  - Re-prompt once with the available options; if still unclear, fall back to the documented default and state that explicitly.

Proceed to **Step 4: Upgrade Execution Phase** after this step completes.

---

### Step 4: Upgrade Execution Phase

**Now apply the upgrade with user customization preservation:**

Before beginning this step, re-read `UPGRADE-STATE.md` to determine:
- Which steps are already marked `completed`
- Any `New Feature Choices` recorded during Step 3.5

1. **Create backup checkpoint (privacy-aware)**:
   ```
   Creating backup of current framework state before upgrade...
   ```
   - Determine the current **Privacy Mode** by reading the `## 🔒 Privacy Configuration` section from `FLOWSTATE.md` (or `.project-config.md`) and extracting:
     - `Privacy Mode`: [Private / Team / Manual / Skip]
   - Then:
     - If **Privacy Mode = Private**:
       - Do **not** run `git add`, `git commit`, or any other git commands automatically.
       - Inform the user that, for privacy reasons, FlowState will not create git checkpoints and that they may create their own backup manually if desired.
     - If **Privacy Mode = Team**:
       - If a git repository is present and user has not objected to git use in this session, you may suggest:
         - `git add -A && git commit -m "Pre-upgrade checkpoint: v[OLD] → v2.5.0"`
       - If the user prefers not to commit, skip this step and note that no checkpoint was created.
     - If **Privacy Mode = Manual** or **Skip**:
       - Ask explicitly:
         - "You're in [Manual/Skip] git mode. Would you like me to create a git checkpoint for this upgrade? (y/N)"
       - Only run git commands if the user explicitly answers yes; otherwise, skip git and proceed.

2. **Update core framework files (apply S1–S3)**:
   - For each of these framework-owned files in the framework location:
     - `flowstate-ai-se-framework-v2.5.0.md` (replaces old version file)
     - `README.md`
     - `REFERENCE.md`
     - `QUICKSTART.md`
     - `TROUBLESHOOTING.md`
     - `CHANGELOG.md`
   - Use Smart Rules:
     - Read both the existing project file and the new version from the upgrade folder.
     - If the only differences are version numbers, dates, or other metadata → treat as uncustomized and **replace the entire file** with the new one.
     - If there are substantive differences or signs of user customization:
       - Show a brief summary of differences and ask the user whether to:
         - Keep their version,
         - Replace with the new version, or
         - Merge specific custom sections.
       - If merging, operate at section/block level (S4) rather than rewriting the whole file.

3. **Handle `TEMPLATES.md` specially (apply S2–S4)**:
   - Compare the existing `TEMPLATES.md` in the project with the new one in the upgrade folder.
   - If the only differences are version numbers, dates, or obvious metadata:
     - Treat as uncustomized and **replace the entire `TEMPLATES.md`** with the new version.
   - If the file is customized:
     - Treat the `## Custom Templates (User-Owned)` section (if present) as user-owned.
     - Extract that section from the existing `TEMPLATES.md`.
     - Replace `TEMPLATES.md` with the new version from the upgrade folder.
     - Append the extracted `## Custom Templates (User-Owned)` block verbatim to the end of the new file.
     - Do not modify framework-owned templates outside this custom section.

4. **Preserve user state files (S5)**:
   - NEVER overwrite these files:
     - `TASKS.md`
     - `SESSION.md`
     - `.flowstate/` directory contents
     - Any user-created files
   - These are user-owned; treat them as read-only during the upgrade, except for safe version header updates where clearly indicated.

5. **Add new configuration sections to FLOWSTATE.md (if needed)**:
   - Read `UPGRADE-STATE.md` and load `New Feature Choices` into a logical map (e.g., `new_feature_configurations`).
   - If this map is non-empty:
     - Read the current `FLOWSTATE.md` (or obfuscated equivalent).
     - For each feature in `new_feature_configurations`:
       - Locate the corresponding section template in the new `TEMPLATES.md` (e.g., Privacy Configuration, Scaffolding Configuration, Quality Mode Configuration).
       - Populate the template with the user’s chosen value(s) and set `Changed` to today’s date.
       - Insert the section into `FLOWSTATE.md` in this order (where missing):
         1. Tech Stack
         2. Privacy Configuration
         3. Scaffolding Configuration
         4. Quality Mode Configuration
         5. Meta-Rules section
       - **Do not modify or delete** any existing configuration sections; add only what is missing (S5).

6. **Update version references**:
   - Create/update `.flowstate/version.txt` with "2.5.0"
   - If `TASKS.md` has a version in its header, update it
   - Update any other clearly identified version markers found

7. **Delete old version framework file** (if different name):
   - Example: Remove the previous framework file (for example, `flowstate-ai-se-framework-v2.3.2.md`) after confirming v2.5.0 is in place

---

### Step 5: Scaffolding Execution (If User Requested)

**Only execute if user chose to run scaffolding immediately in Step 3:**

1. **Load scaffolding configuration** from user's preferences

2. **Run scaffolding at selected level**:
   - Read the scaffolding section in `flowstate-ai-se-framework-v2.5.0.md`
   - Execute scaffolding according to user's selected level (Minimal/Moderate/Comprehensive)
   - **Never overwrite existing files** - only create new ones or ask before replacing

3. **Report what was scaffolded**:
   ```
   Scaffolding Complete:
   - Created: [list of new directories/files]
   - Skipped: [list of existing files not overwritten]
   ```

---

### Step 6: Verification and Reporting Phase

1. **Verify upgrade success**:
   - Confirm all new files are in place
   - Check version markers are updated
   - Verify user files are intact
   - Test framework is accessible (try reading main framework file)

2. **Generate completion report** (IMPORTANT: Include the "What You Can Now Do" section):
   ```
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
   ✅ FlowState AI SE Upgrade Complete!
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

   Upgraded: v[OLD] → v2.5.0

   📊 Summary:
   - Files updated: [count and key files]
   - New files added: [count]
   - User files preserved: [count]
   - Directory structure: [.flowstate/ or legacy root-level]

   🔍 Verification:
   - Framework location: [path]
   - Version file: .flowstate/version.txt → 2.5.0
   - Status: ✅ Ready to use

   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
   🎯 WHAT YOU CAN NOW DO (v2.5.0)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

   🎓 LEARN WHILE YOU BUILD
      Say: "Change concept level to Novice" (or Apprentice/Fluent)
      → AI teaches you ~1 concept per session as you work

   🔄 CATCH UP AFTER WORKING OFFLINE
      Say: "FlowState sync" or "Catch up"
      → Reconcile your task list with actual code changes

   📦 SEARCH OLD DECISIONS
      Say: "FlowState find task authentication"
      → Search archived tasks for how you implemented something

   🆘 GET UNSTUCK WITH GUIDED DEBUGGING
      Say: "Learner MAX" when stuck
      → Choose: "Just fix it" / "Walk me through" / "Explain first"

   ✅ VERIFY FILES ANYTIME
      Say: "FlowState verify"
      → Confirm all FlowState files exist and are valid

   📈 SEE YOUR PROGRESS
      Open: .flowstate/session.md
      → Velocity metrics now appear at the top

   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
   🚀 QUICK REFERENCE: NEW COMMANDS
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

   | Command                          | What it does                    |
   |----------------------------------|---------------------------------|
   | FlowState sync                   | Reconcile after working offline |
   | FlowState verify                 | Check all FlowState files exist |
   | FlowState find task [query]      | Search archived tasks           |
   | FlowState handoff                | Generate context for another AI |
   | Change concept level to [level]  | Adjust teaching depth           |
   | Learner MAX                      | Activate guided debugging       |

   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

   📝 Recommended First Action:
   Try saying "FlowState sync" to see the new sync protocol in action!

   Need help? Run "FlowState status" or see TROUBLESHOOTING.md
   ```

3. **Prompt user to test**:
   ```
   Your upgrade is complete! Try one of these to explore the new features:

   → "FlowState sync" — See the new reconciliation protocol
   → "FlowState verify" — Confirm all files are in place
   → "Change concept level to Apprentice" — Enable concept teaching

   Or say "FlowState SE" to verify basic functionality.
   ```

---

### Step 7: Cleanup Phase

1. **Ask user about cleanup**:
   ```
   Upgrade complete! Would you like me to remove the temporary upgrade folder?

   Folder to remove: [path to upgrade folder]

   (Y/N)
   ```

2. **If user says Yes**:
   - Delete the upgrade folder (e.g., `flowstate-v2.5.0-se/`)
   - Confirm deletion:
     ```
     ✅ Cleanup complete. Temporary upgrade folder removed.
     ```

3. **If user says No**:
   - Leave folder in place
   - Notify:
     ```
     Upgrade folder preserved at: [path]
     You can manually delete it when ready.
     ```

---

### Error Handling

**If any step fails:**

1. **Stop immediately** and report error to user
2. **Do not proceed** to next steps
3. **Provide clear error message**:
   ```
   ⚠️ Upgrade Error at Step X: [description]

   What happened: [details]
   Your data: Safe (no user files were modified)
   Current state: [description]

   Suggested action: [specific fix]
   ```

4. **If backup was created**: Inform user how to rollback
5. **Do not delete upgrade folder** until issue is resolved

---

## Manual Upgrade Steps (If Needed)

In rare cases, you may need to perform manual steps:

### If AI Cannot Complete Upgrade

1. **Backup your current framework files**
2. **Copy all files** from upgrade folder to framework location (except `UPGRADE.md`)
3. **Preserve** your `TASKS.md` and `SESSION.md`
4. **Update** `.flowstate/version.txt` to `2.5.0`
5. **Delete** old version framework file
6. **Test** by running "FlowState SE"

### If Git Conflicts Occur

1. **Commit your current changes** before upgrading
2. **Run upgrade process**
3. **Resolve any git conflicts** manually
4. **Test framework** after resolution

---

## Troubleshooting

### "Cannot find upgrade folder"
- **Solution**: Ensure upgrade folder is in project root
- Folder should contain `UPGRADE.md` and all framework files
- Try: `ls -la` in project root to verify folder exists

### "Current version detection failed"
- **Solution**: Manually tell AI your current version
- Say: "I'm currently on version X.X.X, please proceed with upgrade"

### "Customizations detected, unsure how to merge"
- **Solution**: AI should ask for your guidance
- Review the conflict and choose: Keep yours, use new, or merge manually

### "Framework not working after upgrade"
- **Solution**: Run emergency recovery
- Command: `Read TROUBLESHOOTING.md and follow its AI instructions`
- This will restore FlowState without losing your work

### "Want to rollback upgrade"
- **Solution**: Restore from git or backup
- If git: `git revert [upgrade commit]`
- If no git: Manually restore from backup (if created)

---

## Breaking Changes

### From v2.2.x or earlier

- **Scaffolding system redesigned**: If you used custom scaffolding, review new system
- **Template organization changed**: Some templates renamed or reorganized
- **File structure updated**: Framework files may be in different locations

See [CHANGELOG.md](./CHANGELOG.md) for complete list of breaking changes.

---

## Post-Upgrade Checklist

After upgrade completes:

- [ ] Run "FlowState SE" to verify framework loads
- [ ] Check TASKS.md is intact with your tasks
- [ ] Review CHANGELOG.md for new features
- [ ] Test your primary workflows
- [ ] Configure scaffolding if you skipped it during upgrade
- [ ] Review TROUBLESHOOTING.md for new emergency commands
- [ ] Update any bookmarks/documentation pointing to old version

---

## Support

**Need help?**
- Emergency recovery: See [TROUBLESHOOTING.md](./TROUBLESHOOTING.md)
- Framework issues: Run `FlowState doctor` for diagnostics
- Version conflicts: See "Troubleshooting" section above

**Found a bug?**
- Report to: [Your support channel/email]
- Include: Current version, target version, error message, steps to reproduce

---

## Changelog Reference

For detailed information about what changed in v2.5.0, see:
- [CHANGELOG.md](./CHANGELOG.md) - Complete version history
- [README.md](./README.md) - Quick overview of v2.5.0 features

---

**Version**: 2.5.0
**Last Updated**: 2025-11-24
**Edition**: Software Engineering (SE)
**License**: Proprietary (Mythgate, Copyright Abe Burnett 2025)
