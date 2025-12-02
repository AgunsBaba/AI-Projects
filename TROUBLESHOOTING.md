# FlowState Troubleshooting & Diagnostics
Version: 2.5.0 (Software Engineering Edition)

---

## 🆘 EMERGENCY RECOVERY

**If FlowState is completely unresponsive** (AI doesn't recognize FlowState commands), use this command:

```
Read TROUBLESHOOTING.md and follow its AI instructions. If you can't access that file, search this workspace for files containing "FlowState" and report what you find.
```

This triggers the AI Bootstrap Protocol below, which will diagnose and often auto-fix the issue.

---

## 🤖 AI BOOTSTRAP PROTOCOL

**IF YOU ARE AN AI READING THIS FILE:**

You were directed here because the user is experiencing FlowState issues. Execute this protocol systematically.

---

### Phase 1: Confirm Framework Presence

**Check if you can access these files in this workspace:**
- `flowstate-ai-se-framework-v2.5.0.md`
- `QUICKSTART.md`
- `TEMPLATES.md`
- `REFERENCE.md`

**If ANY missing:**
```
Report to user:
"⚠️ FlowState framework files not found in this workspace.

Possible causes:
1. You opened a subdirectory instead of the repository root
2. Framework files weren't copied to this project
3. Framework files are in a different location

Current directory: [state current directory if detectable]

Fix:
- If wrong directory: Open the repository root folder
- If files missing: Copy framework files from FlowState package
- Then run this command again

Cannot proceed without framework files."
```

**STOP HERE** - Cannot proceed without framework files.

**If ALL present:** Continue to Phase 2.

---

### Phase 2: Detect System State

**Check for FlowState initialization by looking for these file patterns:**

**Standard mode indicators:**
- `.flowstate/config.md`
- `.flowstate/tasks.md`
- `.flowstate/session.md`

**Obfuscated mode indicators:**
- `.flowstate/.config.md`
- `.flowstate/.tasks.md`
- `.flowstate/.session.md`

**Determine state:**

| Files Found | State | Next Phase |
|------------|-------|------------|
| **None of the above exist** | Not Initialized | → Phase 3 (Initialization) |
| **Some exist (e.g., FLOWSTATE.md but not TASKS.md)** | Partially Initialized | → Phase 4 (Partial Recovery) |
| **All core files exist** | Fully Initialized | → Phase 5 (Integration Check) |

---

### Phase 3: Not Initialized - Offer Full Initialization

**Report to user:**
```
FlowState framework detected but not initialized in this project.

To initialize FlowState from scratch, use this command:

"Read flowstate-ai-se-framework-v2.5.0.md and execute FlowState SE initialization"

This will:
1. Ask you 5 strategic questions about your project
2. Create the .flowstate/ directory with config.md, tasks.md, and session.md
3. Set up platform adapters for your AI tool
4. Configure git privacy settings
5. Ask about scaffolding level (learning preferences)

This is a fresh initialization and will not overwrite any existing work.

Would you like to initialize FlowState now?
```

**If user says yes:**
```
Redirecting to initialization...

Say: "Read flowstate-ai-se-framework-v2.5.0.md and execute FlowState SE initialization"
```

**STOP HERE** - Let the standard initialization protocol take over.

---

### Phase 4: Partially Initialized - Refresh Missing Files

**Report to user:**
```
FlowState is partially initialized. Found:
✅ [list files that exist]
⚠️  Missing: [list files that don't exist]

This suggests either:
- Initialization was interrupted
- Files were accidentally deleted
- Working in a cloned repo where some files weren't committed

I can REFRESH the missing files without affecting your existing work.
This will NOT overwrite:
- Existing TASKS.md (your task list)
- Existing SESSION.md (your session history)
- Existing FLOWSTATE.md (your project configuration)

Would you like me to refresh the missing files?
```

**If user confirms:**

**For each missing core file:**

1. **If FLOWSTATE.md missing:**
   ```
   FLOWSTATE.md is the core configuration file. To recreate it, I need to ask
   you the same 5 strategic questions from initialization:
   
   1. Project maturity (new/early/mature)
   2. Phase 0 success metric
   3. Deployment target
   4. Subscription model
   5. Immediate priority
   
   Proceed with questions?
   ```
   Then follow standard initialization questions for FLOWSTATE.md only.

2. **If TASKS.md missing:**
   ```
   Creating TASKS.md from template...
   ✅ Created TASKS.md with standard structure:
      - Backlog (empty - ready for you to add tasks)
      - In-Progress (empty)
      - Done (empty)
   
   Add your first task with: "Add task: [description]"
   ```

3. **If SESSION.md missing:**
   ```
   Creating SESSION.md from template...
   
   What phase are you currently in?
   [0] Phase 0 - Foundation
   [1] Phase 1 - Core Features
   [2] Phase 2 - Enhancement
   [3] Phase 3 - Polish
   
   Your choice: _
   ```
   Then create SESSION.md with user's phase info.

4. **If docs/[project]-master-plan.md missing:**
   ```
   Creating master plan document...
   What is your project name? _
   ```
   Then create from template with user's project name.

**After refresh:**
```
✅ FlowState REFRESHED

Recreated files:
- [list of files recreated]

Preserved files (not touched):
- [list of files that existed]

Your existing work is intact. Now proceeding to Phase 5 to check
platform integration...
```

**Continue to Phase 5.**

---

### Phase 5: Check Platform Integration

**FlowState core files exist. Now verify platform adapters.**

**Step 5A: Detect Current Platform**

```
Determine which AI platform you're running in:

Signals to check:
- Large context window (>100K) + "Claude" mentions = Claude Code
- ".cursor" directory exists + Cursor UI elements = Cursor  
- "GitHub Copilot" in system context = Copilot
- "OpenAI" + "Codex" references = Codex
- If uncertain: ASK USER
```

**Step 5B: Detect Filename Mode**

```
If FLOWSTATE.md exists: filename_mode = "standard"
If .project-config.md exists: filename_mode = "obfuscated"
```

**Step 5C: Discover ALL Installed Adapters**

Check for ALL platform adapter files, not just current platform:

```bash
# Claude Code adapter
[ -f "CLAUDE.md" ] → Claude (standard)
[ -f ".ai-adapter.md" ] → Claude (obfuscated) or Universal adapter

# Cursor adapter
[ -f ".cursor/rules/flowstate.mdc" ] → Cursor (standard)
[ -f ".cursor/rules/project.mdc" ] → Cursor (obfuscated)
[ -f ".cursorrules" ] → Cursor (legacy)

# Copilot/Codex adapter
[ -f "AGENTS.md" ]         → Copilot/Codex (standard)
[ -f ".ai-adapter.md" ]    → Copilot/Codex (obfuscated) or Universal adapter

# JetBrains AI rules
[ -f ".aiassistant/rules/flowstate.md" ] → JetBrains AI rules for this project

# Windsurf rules
[ -f ".windsurfrules" ]    → Windsurf project rules
```

**Note**: `.ai-adapter.md` in obfuscated mode serves BOTH Claude and Copilot/Codex.

**Step 5D: Verify Each Discovered Adapter**

For **each adapter file found**, validate its content:

**Claude Code adapters** (`CLAUDE.md` or `.ai-adapter.md`):
- [ ] Contains "Version: 2.5.0" (Software Engineering Edition)
- [ ] Contains "You are operating under FlowState AI"
- [ ] Has "FlowState SE" command handling
- [ ] References correct core files for detected filename_mode

**Cursor adapters** (`.cursor/rules/flowstate.mdc` or `project.mdc`):
- [ ] Contains `alwaysApply: true`
- [ ] Globs include source files + FlowState docs
- [ ] Contains "FlowState SE" handling
- [ ] Has 13 Meta-Rules quick reference

**Copilot/Codex adapters** (`AGENTS.md` or `.ai-adapter.md`):
- [ ] Has FlowState agent/section defined
- [ ] Commands: "FlowState SE", "Resume FlowState", "What's the current state?"
- [ ] For Codex: includes `@FLOWSTATE.md` usage notes
- [ ] References correct core files for detected filename_mode

**JetBrains AI rules** (`.aiassistant/rules/flowstate.md`):
- [ ] Mentions FlowState AI Framework (SE)
- [ ] Instructs AI to read FLOWSTATE/TASKS/SESSION
- [ ] References FlowState commands: "FlowState SE", "FlowState status", "FlowState doctor"

**Windsurf rules** (`.windsurfrules`):
- [ ] Mentions FlowState AI Framework (SE)
- [ ] Instructs AI to read FLOWSTATE/TASKS/SESSION

**Special case: `.ai-adapter.md` in obfuscated mode**:
- This file serves **both** Claude Code **and** Copilot/Codex
- Verify it has instructions for **both** use cases:
  - Claude Code-style "You are operating under FlowState"
  - Agents-style "FlowState agent" definition

**Step 5E: Diagnose Integration Issues**

**Scenario A: No adapters found for current platform**
```
Diagnosis:
✅ FlowState initialized (core files present)
⚠️  No platform adapter for [current platform]

This is why I don't recognize FlowState commands—I have no instructions
to read FlowState files.

Would you like me to RESTORE the [platform] adapter?
```

**Scenario B: Adapter exists but broken/missing FlowState content**
```
Diagnosis:
✅ FlowState initialized (core files present)
⚠️  [adapter file] exists but doesn't contain FlowState configuration

Likely cause: File was overwritten (e.g., by tool update) or manually edited

Would you like me to RESTORE [adapter file] from v2.5.0 template?
```

**Scenario C: Adapter exists and looks correct**
```
Diagnosis:
✅ FlowState initialized (core files present)
✅ [adapter file] exists with correct FlowState configuration

But I'm not reading it, which means platform configuration issue.

→ Continue to Phase 7 (Platform Configuration Troubleshooting)
```

**Scenario D: Multi-platform setup with gaps**
```
Diagnosis:
✅ FlowState initialized (core files present)

Installed Adapters:
  ✅ Claude Code (CLAUDE.md) - working
  ⚠️  Cursor - No adapter found
  ✅ Copilot/Codex (AGENTS.md) - present

You have a multi-platform setup. FlowState works in Claude and Copilot
but not in Cursor because the Cursor adapter is missing.

Would you like me to RESTORE the Cursor adapter?
```

---

### Phase 6: Restore Broken/Missing Adapters

**For each adapter that needs restoration:**

**Important**: Restoring adapters will NOT affect:
- ✅ Your TASKS.md (task list preserved)
- ✅ Your SESSION.md (session history preserved)
- ✅ Your FLOWSTATE.md (project configuration preserved)
- ✅ Your master plan document
- ✅ Your plans/ and logs/ directories

**Restoration process:**

1. **Detect filename mode** (from Phase 5B)
2. **Read appropriate template** from TEMPLATES.md
3. **If adapter file already exists**: Back it up
   ```
   Backing up existing [adapter file] to [adapter file].backup-[timestamp]
   ```
4. **Create new adapter** from template
5. **Customize** with project-specific info if available
6. **Verify** file was created correctly

**Example restoration for Claude Code:**

```
Restoring CLAUDE.md for Claude Code (standard mode)...

Reading template from TEMPLATES.md...
✅ Template loaded

Creating CLAUDE.md...
✅ Created CLAUDE.md (v2.5.0 SE configuration)
   - FlowState SE command handling: ✅
   - References FLOWSTATE.md, TASKS.md, SESSION.md: ✅
   - 13 Meta-Rules included: ✅

CLAUDE.md restored. Please restart Claude Desktop app to ensure
the new adapter file is loaded.
```

**After restoration for current platform:**

```
✅ [Platform] adapter RESTORED

FlowState is now configured for [platform].

**IMPORTANT**: Please restart [VS Code / Cursor / Claude Desktop] 
to ensure the new adapter files are loaded.

After restarting, verify by saying: "Resume FlowState"
```

**If restoring adapters for multiple platforms:**

```
✅ Multi-platform adapters RESTORED

Created:
- CLAUDE.md (Claude Code)
- .cursor/rules/flowstate.mdc (Cursor)
- AGENTS.md (Copilot/Codex)

FlowState is now available in all three platforms.

Restart your AI tools to load the new adapters, then verify
with "Resume FlowState" in each tool.
```

**STOP HERE** - User should restart tools and verify.

---

## ❓ If an Upgrade Stalled or the AI Got Confused

If a previous FlowState **SE upgrade** attempt was interrupted, partially completed, or the AI seems confused about which steps have run, use this command:

```
Read UPGRADE.md (in the FlowState SE upgrade folder) and UPGRADE-STATE.md (in this project root). Then resume the upgrade from the first step that is not marked completed in UPGRADE-STATE.md. Do not repeat any steps that are already marked completed unless I explicitly ask you to.
```

**AI Instructions (if you are an AI reading this):**

1. Locate the FlowState SE upgrade folder in the project root and open `UPGRADE.md`.
2. Locate `UPGRADE-STATE.md` in the project root (create it only if it truly does not exist and this is the first upgrade run).
3. Read `UPGRADE-STATE.md` and determine which steps (0–7) are marked `completed`.
4. Resume execution from the **first step that is not completed**.
5. After completing each step, update `UPGRADE-STATE.md` to mark that step as `completed`.
6. Do **not** re-run completed steps unless the user explicitly requests it.
7. If anything looks inconsistent or unsafe, stop and explain the situation clearly to the user before proceeding.

---

### Phase 7: Platform Configuration Issues

**You've reached this phase if:**
- ✅ FlowState core files exist
- ✅ Adapter files exist with correct content
- ❌ But you (the AI) still aren't reading them

**This is a platform/settings issue, not a file issue.**

**Platform-specific troubleshooting:**

**If Claude Code:**
```
🔍 Claude Code Platform Issue

CLAUDE.md exists and looks correct, but I'm not reading it.

Checklist for user:
□ In Claude Desktop → Projects → Verify this folder is added as project
□ Check project settings → Ensure CLAUDE.md is in the include list
□ Restart Claude Desktop app
□ After restart, try: "Resume FlowState"

If still not working:
- Check Claude Desktop version (need latest)
- Try removing and re-adding project
- Check Claude Desktop logs for file access errors
```

**If Cursor:**
```
🔍 Cursor Platform Issue

.cursor/rules/flowstate.mdc exists and looks correct, but I'm not reading it.

Checklist for user:
□ Cursor Settings → Rules → Enable "Use rules from .cursor/rules/"
□ Verify path is set to ".cursor/rules" (not ".cursor" or other path)
□ Check "Always apply rules" is enabled
□ Restart Cursor
□ After restart, try: "Resume FlowState"

If still not working:
- Check Cursor version (need v0.40+)
- Try creating .cursorrules in project root (legacy fallback)
- Check Cursor logs: Help → Show Logs
```

**If Copilot:**
```
🔍 GitHub Copilot Platform Issue

AGENTS.md exists and looks correct, but I'm not reading it.

Checklist for user:
□ VS Code Settings → Search "Copilot Agents"
□ Enable "GitHub Copilot: Enable Agents"
□ Verify "Agents for Workspace" is checked
□ Restart VS Code
□ After restart, try: "@workspace Resume FlowState"

If still not working:
- Check Copilot extension version (need latest)
- Try disabling/re-enabling Copilot extension
- Check if Agent Mode is available in your Copilot plan
- Check VS Code output: View → Output → GitHub Copilot
```

**If Codex:**
```
🔍 OpenAI Codex Platform Issue

AGENTS.md exists and looks correct, but I'm not reading it.

Checklist for user:
□ Verify Codex CLI is latest version
□ Check AGENTS.md is in current directory or parent directory
□ Try explicit reference: "@AGENTS.md Resume FlowState"
□ Restart Codex session

If still not working:
- Check Codex session logs
- Try using absolute path to AGENTS.md
- Verify file permissions (must be readable)
```

---

## 📋 QUICK ISSUE FINDER

**Find your symptom, jump to the solution:**

### "FlowState commands don't work"
- AI doesn't respond to "FlowState SE" or "Resume FlowState"
- AI doesn't read FLOWSTATE.md/TASKS.md/SESSION.md
- Works in one tool but not another

### "Something broke after..."
- VS Code / Cursor / Copilot updated
- I pulled changes from Git
- I cloned the repo on a new machine
- I edited a FlowState file manually

### "I want to..."
- Use FlowState in multiple AI tools
- Switch from standard to obfuscated filenames
- Switch from private to team privacy mode
- Verify everything is configured correctly

### "Advanced issues"
- Manual verification (AI can't access files)
- FlowState seems to work but context is wrong
- Git privacy configuration broken

---

## 🔧 COMMON ISSUES & SOLUTIONS

### AI Doesn't Respond to FlowState Commands

**Symptoms:**
- Say "FlowState SE" → AI responds generically, doesn't enter FlowState mode
- Say "Resume FlowState" → AI says "I don't have context" or similar
- AI doesn't reference FLOWSTATE.md, TASKS.md, or SESSION.md automatically

**Quick fix:**
```
Read TROUBLESHOOTING.md and follow its AI instructions.
```

This runs the bootstrap protocol which will diagnose and usually fix the issue automatically.

**What the bootstrap protocol will find:**
- Platform adapter missing (never created or deleted)
- Platform adapter overwritten by tool update
- Platform adapter exists but missing FlowState content
- Platform settings issue (adapters not being read)

**After diagnosis, AI will:**
- Restore missing/broken adapter files from templates
- Tell you if platform settings need adjustment
- Guide you through any necessary restart steps

---

### After Tool Update

**Scenario:** "FlowState worked yesterday. Today I updated [VS Code / Cursor / Copilot / Claude] and now it doesn't work."

**What happened:**
Tool updates can:
- Overwrite custom adapter files (CLAUDE.md, AGENTS.md)
- Reset settings to defaults (disable rules/agents)
- Change how files are read (.cursor/rules/ path changes)

**Solution:**
```
Read TROUBLESHOOTING.md and follow its AI instructions.
```

AI will detect which adapter was affected and restore it from template.

**Your existing work is safe:**
- ✅ TASKS.md (task list) not affected
- ✅ SESSION.md (session history) not affected
- ✅ FLOWSTATE.md (project config) not affected
- ✅ Plans and logs not affected

**Prevention for next time:**
- Keep FlowState framework files in version control
- Run health check after tool updates: "FlowState status"
- Consider obfuscated filename mode (files less likely to be detected/modified)

---

### Works in One Tool, Not Another

**Scenario:** "FlowState works great in Claude Code, but when I open the same project in Cursor, it doesn't work."

**Why this happens:**
Each AI tool needs its own adapter file. FlowState working in Claude means CLAUDE.md exists, but Cursor needs `.cursor/rules/flowstate.mdc`.

**Solution:**
```
Add FlowState to Cursor
```

AI will:
1. Detect you're in Cursor
2. Check if Cursor adapter exists
3. Create `.cursor/rules/flowstate.mdc` from template
4. Preserve your existing CLAUDE.md (for Claude Code)

**Result:** FlowState works in both tools, sharing the same FLOWSTATE.md, TASKS.md, SESSION.md

**Multi-platform checklist:**
- [ ] Each tool you use has its adapter file installed
- [ ] All adapters reference the same core files
- [ ] Filename mode is consistent across all adapters
- [ ] Git privacy settings respect all adapter files

---

### After Git Pull / New Machine Setup

**Scenario:** "I cloned the repo / pulled latest changes. FlowState files exist but nothing works."

**Why this happens:**
- If `privacy_mode = "private"`, adapter files weren't committed
- Even if `privacy_mode = "team"`, some teams gitignore adapter files
- New machine = fresh AI tool installation = no adapter cache

**Solution:**
```
Read TROUBLESHOOTING.md and follow its AI instructions.
```

AI will:
1. Detect FlowState is initialized (core files present)
2. Detect platform adapters are missing
3. Restore adapters for your current platform
4. Ask if you use multiple platforms

**This is a RESTORE operation, not initialization:**
- ✅ Keeps existing TASKS.md (your task list)
- ✅ Keeps existing SESSION.md (your history)
- ✅ Keeps existing FLOWSTATE.md (your project config)
- ✅ Only recreates adapter files

**Alternative (if you know which adapters you need):**
```
Add FlowState to [platform]
```

Example: "Add FlowState to Cursor"

---

### After Manual Edits

**Scenario:** "I edited [CLAUDE.md / AGENTS.md / flowstate.mdc / FLOWSTATE.md] and now things are broken."

**Common mistakes:**
- Removed required sections (FlowState command handling)
- Changed file references to wrong names
- Broke Markdown/MDC syntax
- Mixed filename modes (referencing FLOWSTATE.md in obfuscated setup)

**Solution:**
```
Read TROUBLESHOOTING.md and follow its AI instructions.
```

AI will validate adapter content and offer to restore from template.

**You'll be asked:**
```
⚠️  [adapter file] exists but validation failed:
    - Missing "FlowState SE" command handler
    - References "FLOWSTATE.md" but actual file is ".project-config.md"

Likely cause: Manual edits broke required structure

Options:
[A] Restore from template (your edits will be backed up)
[B] Show me what's wrong (I'll try to fix manually)
[C] Cancel (no changes)
```

**If you restore:** Your custom edits are backed up to `[file].backup-[timestamp]`

---

## 🎯 SPECIFIC SCENARIOS

### Multi-Platform Setup

**Goal:** Use FlowState in Claude Code, Cursor, Copilot, JetBrains AI, and Windsurf

**Steps:**

1. **Initialize FlowState once** (in any tool):
   ```
   Read flowstate-ai-se-framework-v2.5.0.md and execute FlowState SE initialization
   ```

2. **Add adapters for other platforms:**
   ```
   Add FlowState to Cursor
   Add FlowState to Copilot
   Add FlowState to JetBrains
   Add FlowState to Windsurf
   ```

3. **Verify each platform:**
   - In Claude Code: "Resume FlowState"
   - In Cursor: "Resume FlowState"
   - In Copilot: "@workspace Resume FlowState"
   - In JetBrains AI: "Resume FlowState"
   - In Windsurf: "FlowState status"

**Result:**
- All tools share: FLOWSTATE.md, TASKS.md, SESSION.md
- Each tool has its own adapter: CLAUDE.md, .cursor/rules/flowstate.mdc, AGENTS.md
- Work in any tool, context preserved across all

**Git consideration:**
If `privacy_mode = "private"`, adapters won't be committed. Each team member needs to run:
```
Read TROUBLESHOOTING.md and follow its AI instructions.
```
Then specify which platforms they use.

---

### Changing Filename Modes

**Scenario:** Want to switch from standard (FLOWSTATE.md) to obfuscated (.project-config.md) or vice versa

**⚠️ Warning:** This is a migration operation. Backup first.

**See:** `flowstate-ai-se-framework-v2.5.0.md` § "Changing Filename Mode After Initialization"

This is **not** a recovery operation—it's a deliberate migration with different command.

---

### Changing Privacy Modes

**Scenario:** Want to switch from private to team mode or vice versa

**Commands:**
- `"Make FlowState visible"` (private → team)
- `"Make FlowState private"` (team → private)

**See:** `flowstate-ai-se-framework-v2.5.0.md` § "Git Privacy Migration"

This is **not** a recovery operation—it's a deliberate migration with different command.

---

### Proactive Health Check

**When to run:**
- ✅ After any AI tool update
- ✅ Once a week (if actively developing)
- ✅ Before starting work in a new environment
- ✅ After pulling major changes from team
- ✅ When switching between AI tools

**Command:**
```
FlowState status
```

**What it checks:**
- Framework files accessible
- FlowState initialized (core files present)
- All platform adapters present and valid
- Git privacy configuration (if applicable)

**Healthy output looks like:**
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FLOWSTATE HEALTH CHECK SUMMARY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Framework Installation: ✅
FlowState Runtime: ✅
Platform Integration: ✅
Git Integration: ✅

Overall Status: HEALTHY ✅
No issues found.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**If issues found:**
```
Would you like me to run "FlowState doctor" to diagnose and offer fixes?
```

**"FlowState verify" vs "FlowState status" vs "FlowState doctor":**
- **Verify** [NEW in v2.5]: File existence check — reads each core file to confirm it exists and has valid headers. Use after initialization or if files seem missing. Aliases: `FS verify`, `Verify FlowState`, `Check FlowState files`
- **Status**: Read-only health check — verifies accessibility and configuration, no changes made
- **Doctor**: Diagnose + repair — runs checks and offers to restore broken configuration

---

## 🔍 MANUAL VERIFICATION

**If AI can't read files** (filesystem access restricted), verify manually:

### Check 1: Framework Files Present
```bash
# Should all exist:
ls flowstate-ai-se-framework-v2.5.0.md
ls QUICKSTART.md
ls TROUBLESHOOTING.md  # This file
ls REFERENCE.md
ls TEMPLATES.md
```

### Check 2: FlowState Initialized
```bash
# Standard mode:
ls FLOWSTATE.md TASKS.md SESSION.md docs/*-master-plan.md plans/ logs/

# Obfuscated mode:
ls .project-config.md .tasks.md .session-state.md docs/.master-plan.md plans/ logs/
```

### Check 3: Platform Adapters Present

**For Claude Code:**
```bash
# Standard:
ls CLAUDE.md
grep "FlowState SE" CLAUDE.md

# Obfuscated:
ls .ai-adapter.md
grep "FlowState SE" .ai-adapter.md
```

**For Cursor:**
```bash
# Standard:
ls .cursor/rules/flowstate.mdc
grep "alwaysApply: true" .cursor/rules/flowstate.mdc

# Obfuscated:
ls .cursor/rules/project.mdc
grep "alwaysApply: true" .cursor/rules/project.mdc
```

**For GitHub Copilot / OpenAI Codex:**
```bash
# Standard:
ls AGENTS.md
grep -A5 "FlowState" AGENTS.md

# Obfuscated:
ls .ai-adapter.md
grep -A5 "FlowState" .ai-adapter.md
```

### Check 4: Adapter Content Validation

**Every adapter must contain:**
1. FlowState version (2.5.0 SE)
2. Command handlers: "FlowState SE" and "Resume FlowState"
3. References to core files (matching your filename mode)
4. Instructions to read FLOWSTATE/TASKS/SESSION before responding

**Check specific adapter:**
```bash
# Check CLAUDE.md has required sections:
grep "Version: 2.3" CLAUDE.md
grep "FlowState SE" CLAUDE.md
grep "Resume FlowState" CLAUDE.md
grep "FLOWSTATE.md" CLAUDE.md  # Or .project-config.md if obfuscated
```

**If any missing:** Restore adapter from TEMPLATES.md

---

## 🆘 WHEN TO ASK FOR HELP

**You've tried everything in this guide and:**
- Bootstrap protocol reports all files OK
- Manual verification shows all files present and correct
- Restarted AI tool multiple times
- Checked tool settings (rules/agents enabled)
- Still doesn't work

**Before asking for help, gather:**
1. Output of bootstrap protocol (or "FlowState doctor")
2. Which AI tool(s) you're using (name + version)
3. Operating system
4. What command doesn't work (exact text)
5. Exact AI response when it fails
6. Screenshot if helpful

**Where to ask:**
- Email: abe@flowstateai.dev
- Discord: https://discord.gg/FWx5swdCMK

---

## 🔄 ROUTINE MAINTENANCE

### When to Run Health Checks
- ✅ After any AI tool update
- ✅ Once a week (if actively developing)
- ✅ Before starting work in a new environment
- ✅ After pulling major changes from team
- ✅ When switching between AI tools

### Healthy System Checklist
- [ ] "FlowState status" reports all green
- [ ] "Resume FlowState" loads context instantly
- [ ] AI references `.flowstate/config.md`, `.flowstate/tasks.md`, `.flowstate/session.md` automatically
- [ ] Multi-platform setup works consistently
- [ ] Git privacy configuration matches your preference

---

## 📚 RELATED DOCUMENTATION

- **[QUICKSTART.md](QUICKSTART.md)** - Initial setup and first-time use
- **[flowstate-ai-se-framework-v2.5.0.md](flowstate-ai-se-framework-v2.5.0.md)** - Complete system reference
- **[REFERENCE.md](REFERENCE.md)** - Deep dives on specific components
- **[TEMPLATES.md](TEMPLATES.md)** - File templates for manual restoration
- **[CHANGELOG.md](CHANGELOG.md)** - Version history and migration guides

---

**End of TROUBLESHOOTING.md**
