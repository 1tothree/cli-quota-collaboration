# v1.0.0 — Initial Public Release

## 中文说明

首次公开发布 **cli-quota-collaboration**：一套让 **Antigravity / Codex 主模型** 与 **本机免费编码 CLI（如 CodeBuddy CLI）** 常态化协同工作的 Skill 与工程规范。

### 本次包含内容
- **标准 Skill（`SKILL.md`）**：涵盖任务决策表、6 段式派单模板、PowerShell 管道防转义、精确路径注入、写前 Git 检查点、失败 2 次兜底及分级验收。
- **一键接入文档（`SETUP_PROMPT.md`）**：直接丢给 Antigravity 或 Codex 客户端，即可自动完成 CLI 探测、Skill 安装、全局记忆追加与冒烟测试。
- **项目模板（`templates/`）**：提供 `CLI_PROJECT_RULES.md`（可重命名为 `CODEBUDDY.md` / `AGENTS.md`）与 `dispatch_log.csv` 复盘日志模板。
- **中英文双语发布页**：`README.md` 与 `README.en.md`。

---

## English

Initial public release of **cli-quota-collaboration**: an always-on workflow and Skill for pairing a primary coding agent (**Antigravity / Codex**) with a free/low-cost local coding CLI (such as **CodeBuddy CLI**) to cut premium token consumption.

### What's Included
- **Standard Skill (`SKILL.md`)**: Task decision matrix, 6-part dispatch template, Windows PowerShell stdin piping fix, exact reference path injection, pre-edit Git checkpoints, 2-retry fallback, and tiered diff review.
- **One-Click Setup (`SETUP_PROMPT.md`)**: Paste directly into Antigravity or Codex to auto-detect your local CLI, install the Skill, append global rules, and run a smoke test.
- **Templates (`templates/`)**: `CLI_PROJECT_RULES.md` (`CODEBUDDY.md` / `AGENTS.md` template) and `dispatch_log.csv`.
- **Bilingual Documentation**: `README.md` (zh-CN) and `README.en.md` (en).
