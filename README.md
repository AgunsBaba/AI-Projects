# FlowState AI Framework SE v2.5.0 – Concept Teaching + Sync Protocol + .flowstate/ Directory

**Created**: 2025-11-24
**Status**: ✅ Production Ready

**⚡ NEW in v2.5.0**: **Contextual Concept Teaching + FlowState Sync + .flowstate/ Directory + Task Archival** — AI teaches you language/framework concepts as you work, reconciles state after off-reservation work, organizes files in a dedicated directory, and auto-archives completed tasks.

**🔄 Preserved from v2.4**: **Quality Mode System + Execution Loop Contract + Proceed Commands** — independently control work rigor (Fast / Balanced / Methodical), keep a persistent task loop visible, and use `proceed` commands for bounded automation.

**🆘 Preserved from v2.3.x**: **Emergency Recovery + Scaffolding Levels + Automated Upgrades** — self-contained bootstrap protocol, AI teaching depth control, and one-prompt upgrades.

---

## 🎯 What's Now Possible (v2.5.0)

### 🎓 Learn While You Build

**Before v2.5**: You either knew the tech stack or struggled in silence.

**Now**: Set your **Concept Level** and the AI teaches you ~1 concept per session as you work.

**Try it**:
- `"Change concept level to Novice"` — Maximum teaching (new technology)
- `"Change concept level to Apprentice"` — Gradual teaching (default)
- `"Change concept level to Fluent"` — No teaching (you're an expert)

---

### 🔄 Catch Up After Working Offline

**Before v2.5**: If you coded without FlowState, your task list drifted out of sync.

**Now**: Say **"FlowState sync"** and the AI scans git changes, matches them to tasks, and helps you reconcile.

**Try it**: `"Sync up"` or `"Catch up"` or `"I did work without you"`

---

### 📦 Find Old Decisions and Completed Work

**Before v2.5**: Completed tasks cluttered TASKS.md forever.

**Now**: Tasks **auto-archive** after phase transitions. Search with natural language.

**Try it**: `"FlowState find task authentication"` or `"Search archived tasks for API"`

---

### 📁 Cleaner Project Root

**Before v2.5**: FLOWSTATE.md, TASKS.md, SESSION.md cluttered your project root.

**Now**: Everything lives in **`.flowstate/`** by default:
```
.flowstate/
├── config.md (was FLOWSTATE.md)
├── tasks.md
├── session.md
├── archive/
└── version.txt
```

---

### 🆘 Get Unstuck with Guided Debugging

**Before v2.5**: When stuck, you either asked "just fix it" or struggled alone.

**Now**: **Learner MAX** mode offers three paths:
- **"Just fix it"** — AI solves it, explains briefly
- **"Walk me through"** — AI asks guiding questions
- **"Explain first"** — AI teaches the concept first

---

### ✅ Verify Everything Worked

**Before v2.5**: If initialization failed silently, you'd only discover it later.

**Now**: The **`FlowState verify`** command checks all files exist anytime.

**Try it**: `"FlowState verify"` or `"FS verify"` or `"Check FlowState files"`

---

### 🚀 Quick Reference: New Commands

| Command | What it does |
|---------|--------------|
| `FlowState sync` | Reconcile after working offline |
| `FlowState verify` | Check all FlowState files exist |
| `FlowState find task [query]` | Search archived tasks |
| `FlowState handoff` | Generate context for another dev/AI |
| `Change concept level to [level]` | Adjust teaching depth |
| `Learner MAX` | Activate guided problem-solving |

---

## 📦 What's in SE v2.5.0

### Framework Files (7 Files)

These are the files you copy into a project when you install SE v2.5.0:

```text
v2.5.0/
├── flowstate-ai-se-framework-v2.5.0.md   (Main framework spec + meta-rules + protocols)
├── UPGRADE.md                            (Upgrade automation: v2.4.x → v2.5.0)
├── TROUBLESHOOTING.md                    (Emergency recovery + diagnostics)
├── QUICKSTART.md                         (5-minute onboarding)
├── REFERENCE.md                          (Meta-rules deep dives, examples, protocols)
├── TEMPLATES.md                          (All templates)
└── CHANGELOG.md                          (Version history + migration guide)
```

---

## 🚀 What's New in v2.5.0 (SE Edition)

### 1. Contextual Concept Teaching (CCT)

AI now teaches language/framework/library concepts gradually over time.

- **Concept Levels**: Novice / Apprentice (default) / Practitioner / Fluent
- **Per-technology tracking**: Different mastery levels for each technology
- **~1 concept per session**: Brief, contextual, non-blocking teaching
- **Independent from Scaffolding**: Scaffolding = AI orchestration; Concept Levels = domain knowledge

---

### 2. FlowState Sync Protocol

Reconcile FlowState with reality after off-reservation work.

- **7-phase sync protocol**: Detects drift between tasks and actual code
- **Git integration**: Scans changes since last session
- **Guided reconciliation**: Asks what to mark as done
- **Rich aliases**: `FS sync`, `Sync up`, `Catch up`, etc.

---

### 3. .flowstate/ Directory Structure (New Default)

All FlowState files now live in `.flowstate/` by default.

- **Cleaner project root**: No conflicts with your README.md
- **Easier privacy configuration**: One directory to manage
- **Automatic migration**: Upgrade process offers to migrate existing files

Structure:
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

### 4. Task Archival System

Automatic archival of completed tasks.

- **Triggers**: >15 done tasks, phase transition, manual request
- **Searchable**: `FlowState find task [query]`
- **Historical context**: Find how you implemented something months ago

---

### 5. Learner MAX Mode

Guided problem-solving for users who get stuck.

- **Three options**: "Just fix it" / "Walk me through" / "Explain first"
- **Diagnostic frameworks**: Structured debugging questions
- **Always escapable**: Say "just fix it" anytime

---

### 6. Additional v2.5.0 Features

- **Velocity Metrics**: Progress analytics at top of `.flowstate/session.md`
- **Handoff Generation**: `FlowState handoff` creates context documents
- **Phase Retrospectives**: Learning capture at phase transitions
- **Self-Verification Protocol**: Mandatory file verification during initialization
- **Knowledge Currency Protocol**: AI self-assesses knowledge freshness

---

### 7. Preserved from v2.4.0

These features continue to work exactly as before:

- **Quality Mode System**: Fast / Balanced / Methodical rigor control
- **Execution Loop Contract (Meta-Rule 14)**: Persistent task visibility
- **Proceed Commands**: `proceed`, `proceed next`, `proceed all`, `ultrathink`, `pause`

---

### 8. Preserved from v2.3.x

- **Automated Upgrade System (v2.3.2)**: One-prompt upgrades
- **Emergency Recovery (v2.3.1)**: Bootstrap protocol in TROUBLESHOOTING.md
- **Scaffolding Levels (v2.3)**: Learner / Growth / Balanced / Expert teaching depth

See `CHANGELOG.md` for complete version history.

---

## 🧭 How to Use SE v2.5.0

**New SE project**
1. Copy all SE v2.5.0 framework files into your project root.
2. Follow `QUICKSTART.md` (≈5 minutes).
3. Choose a **Concept Level**, **Scaffolding Level**, and **Quality Mode** when prompted.

**Existing SE FlowState project (v2.4.x)**
1. Place SE v2.5.0 files into a temporary upgrade folder (e.g., `flowstate-upgrade/`).
2. Run the `UPGRADE.md` prompt.
3. Confirm Concept Level, directory structure preference, and other settings.

**If something stops working**
- Run: `Read TROUBLESHOOTING.md and follow its AI instructions to diagnose and restore FlowState SE framework functionality`.

---

## 🧱 File-Level Map (SE Edition)

- `flowstate-ai-se-framework-v2.5.0.md`
  Primary SE spec, initialization protocol, meta-rules, CCT system, Sync Protocol.

- `QUICKSTART.md`
  Fast start guide for SE initialization and day-to-day use.

- `TROUBLESHOOTING.md`
  SE-specific recovery flows, including multi-platform adapter fixes.

- `TEMPLATES.md`
  Templates for `.flowstate/config.md`, `.flowstate/tasks.md`, `.flowstate/session.md`, and adapters.

- `REFERENCE.md`
  Meta-rules deep dive, proceed-command workflows, SE-specific protocols.

- `CHANGELOG.md`
  Full version history plus the v2.5.0 feature breakdown and migration guide.

- `UPGRADE.md`
  Orchestrates upgrades from v2.3.x / v2.4.x to v2.5.0.

---

## 🎯 SE Edition Focus

SE Edition focuses on:

- Turning your AI assistant into a **self-executing engineering partner**.
- Keeping `.flowstate/config.md`, `.flowstate/tasks.md`, and `.flowstate/session.md` as the single source of truth.
- Enforcing pragmatic SE guardrails (small diffs, tests, docs, refactor cycles) without heavy process.
- Supporting multi-platform setups (Claude, Cursor, Copilot, Codex) via adapters.

v2.5.0 adds **concept teaching**, **state synchronization**, and **cleaner organization** on top of the v2.4 execution controls, making FlowState both more powerful and easier to manage.

---

## 📞 Support

**For questions or issues:**
- Email: abe@flowstateai.dev
- Discord: https://discord.gg/FWx5swdCMK

---

**Version**: 2.5.0
**Last Updated**: 2025-11-24
**Framework Created By**: Abe Burnett, Mythgate
