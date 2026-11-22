<div align="center">

# cli-quota-collaboration

**Always-On Quota-Saving Workflow: Main Coding Agent (Antigravity / Codex) + Local Free Coding CLI (e.g. CodeBuddy CLI)**

[简体中文](./README.md) · [English](./README.en.md) · [One-Click Setup Prompt](./SETUP_PROMPT.md) · [Release Notes](./RELEASE_NOTES.md)

<img src="./assets/hero.jpg" alt="Gemini & Hunyuan Collaboration" width="460" />

*"Delegate the heavy lifting to the free local CLI—keep your premium main model focused on architecture, debugging, and final review."*

</div>

---

## Why This Project?

In daily AI-assisted development, a huge chunk of your premium quota (Gemini / Claude / GPT) is burned on **long log triage, unit test generation, repetitive styling/copy edits, standalone utility scripts, and daily reports**—tasks that do not require frontier-level reasoning.

`cli-quota-collaboration` provides a **battle-tested, privacy-sanitized, drop-in workflow** that splits work cleanly between two tiers:
- **Main Agent (Antigravity / Codex)**: Requirements breakdown, architecture & cross-module refactoring, browser/MCP/vision tasks, and **tiered diff review**.
- **Local Free/Low-Cost CLI (e.g. CodeBuddy CLI with `hy4flash-free`)**: Self-contained coding tasks (1–2 files), unit tests, docs, log summarization, and standalone scripts.

---

## Key Features

- **Always-On Delegation (Regardless of Remaining Quota)**: Every task starts by offloading lightweight, well-scoped subtasks to the local CLI instead of waiting until your quota is nearly exhausted.
- **Clear Decision Matrix**: Defines exactly what goes to the CLI, what stays with the main agent, and what the main agent should execute in 1 second with a shell command (such as pure file moves or cross-drive directory scans).
- **Production-Tested Safeguards**:
  - **Windows PowerShell Quoting Fix**: Long prompts are written to a temporary file and piped via stdin (`Get-Content -Raw prompt.md | codebuddy -p ...`) so PowerShell never strips double quotes.
  - **Exact Reference Path Injection**: Always include exact file paths in dispatch prompts to eliminate blind CLI file-hunting loops.
  - **Pre-Edit Checkpoints & Redlines**: Require a clean `git status` or backup before `--permission-mode acceptEdits`; forbid deleting directories, `git push`, `reset --hard`, or touching secrets/runtime caches.
  - **2-Retry Fallback & Tiered Review**: Cap retries at 2 attempts before the main agent takes over; review `git diff --stat` and test results first, inspecting only core logic diffs.

---

## Real-World Benchmark

From a live multi-project sprint (**22 consecutive business dispatches** using free `hy4flash-free`, `credit: 0`):

| Metric | Observed Result |
| :--- | :--- |
| **First-Pass Success** | **19 / 22** completed directly (3 hit sandbox/cross-drive limits and fell back cleanly to the main agent) |
| **Total CLI Execution** | **348** model turns across **47.9 min** |
| **Tokens Offloaded** | **18.28M** input + **288K** output (**18.57M** total tokens) |
| **Estimated Main Quota Saved** | **~6M–9M equivalent tokens**, shifting nearly **100%** of heavy text/code output off the paid quota |

---

## 30-Second Quick Start

### Option 1: Drop `SETUP_PROMPT.md` into Antigravity or Codex (Recommended)
1. Ensure at least one local coding CLI (such as [CodeBuddy CLI](https://www.codebuddy.ai/)) is installed and signed in.
2. Paste or attach **[SETUP_PROMPT.md](./SETUP_PROMPT.md)** directly into **Antigravity** or **Codex**.
3. Your agent will auto-detect the CLI, install `SKILL.md`, append the global delegation rules, and run a smoke test.

### Option 2: Manual Skill Installation
- **Antigravity**: Copy `SKILL.md` to `~/.gemini/config/skills/cli-quota-collaboration/SKILL.md`
- **Codex**: Copy `SKILL.md` to `~/.codex/skills/cli-quota-collaboration/SKILL.md`

---

## Repository Structure

```text
cli-quota-collaboration/
├── assets/
│   └── hero.jpg                     # Hero illustration
├── README.md                        # Chinese release page
├── README.en.md                     # English release page
├── RELEASE_NOTES.md                 # v1.0.0 GitHub Release notes
├── SETUP_PROMPT.md                  # One-click setup prompt for Antigravity / Codex
├── SKILL.md                         # Sanitized Skill specification
├── LICENSE                          # MIT License
├── .gitignore
└── templates/
    ├── CLI_PROJECT_RULES.md         # Per-repo rules template (rename to CODEBUDDY.md / AGENTS.md)
    └── dispatch_log.csv             # Dispatch tracking log template
```

---

## License

[MIT](./LICENSE)
