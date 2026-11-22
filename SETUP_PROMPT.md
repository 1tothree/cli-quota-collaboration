# 一键接入文档（直接丢给 Antigravity 或 Codex 客户端使用）

> **使用方式**：把本文件全文复制发送给你的 **Antigravity** 或 **Codex** 客户端（或作为附件/路径引用），客户端会自动检测你本机已安装的免费/低成本 CLI，为你配置好技能、全局记忆与派单日志。

---

## 请 AI 客户端按以下步骤为我配置「主模型 + 本地 CLI 协同省额度工作流」：

### 第 1 步：探测本机可用的免费/低成本编码 CLI
请帮我检查本机当前操作系统，并探测是否已安装以下任一本地编码 CLI（优先顺序）：
1. **CodeBuddy CLI**（Windows 常见路径：`%LOCALAPPDATA%\codebuddy\bin\codebuddy.exe` 或 `codebuddy`；macOS/Linux：`which codebuddy`）
2. **其他用户指定的本地 CLI**（如 `gemini`、`qwen`、`opencode` 等）

探测时请确认：
- 可执行文件的绝对路径；
- 非交互静默参数（例如 `--model hy4flash-free --no-session-persistence --output-format json`）；
- 运行一次 1 句话的只读冒烟测试（如返回 `{"ok": true}`），确认无需人工交互即可正常输出。
- **若未检测到或未登录**：请暂停并提示我先安装/登录对应的 CLI，再继续后续步骤。

### 第 2 步：落盘 `cli-quota-collaboration` Skill
根据我当前使用的客户端，将本仓库的 `SKILL.md` 写入对应技能目录（并将 `<CLI_BIN>`、`<FREE_OR_LOW_COST_MODEL>` 替换为第 1 步实测通过的值）：
- **Antigravity 客户端**：写入 `~/.gemini/config/skills/cli-quota-collaboration/SKILL.md`
- **Codex 客户端**：写入 `~/.codex/skills/cli-quota-collaboration/SKILL.md`（或当前工作区 `.agents/skills/cli-quota-collaboration/SKILL.md`）

### 第 3 步：写入全局记忆 / 规则文件（不覆盖已有内容，仅追加协同章节）
在我的全局规则文件末尾追加以下精简规范（Antigravity 对应 `~/.gemini/GEMINI.md`，Codex 对应 `~/.codex/AGENTS.md`）：

```markdown
# 通用协作与工具委派偏好

- **常态化优先委派本地 CLI（无论剩余额度多少）**：每次执行任务前，先评估并拆解出轻量/独立子任务（单测、文档、日志/同盘目录初筛、独立脚本、批量机械修改及 1~2 个文件内的明确编码任务），优先委派给本机 `<CLI_BIN>`（非交互模式 + 免费/低成本模型 `<FREE_OR_LOW_COST_MODEL>`，写操作加 `--permission-mode acceptEdits`）。Windows PowerShell 传长提示词时先写入临时文件再通过管道传入（`Get-Content -Raw prompt.md | <CLI_BIN> -p ...`），避免剥离双引号；派单时直接附上精确参考文件路径以减少 CLI 试错轮数。
- **主模型聚焦与分级验收**：主模型仅负责需求拆解、复杂跨模块/架构决策、浏览器/MCP/视觉任务、纯文件移动/跨盘列目录（用一条 shell 命令完成）及分级验收（先看 `git diff --stat` 与测试结果，仅细查核心 diff）。
- **安全与失败兜底**：写操作前先确认 Git 工作区干净或建立检查点（非 Git 先备份）；禁止 CLI 删除目录、执行 `git push`/`reset --hard` 或触碰密钥与运行时缓存；同一子任务最多派单 2 次，仍失败则由主模型接手，验收后追加一行到 `dispatch_log.csv`。
```

### 第 4 步：初始化派单日志并汇报结果
1. 在我的工作区或 scratch 目录创建 `dispatch_log.csv`，表头为：
   `date,project,task_type,mode,first_pass_success,retries,notes`
2. 写入第 1 条冒烟测试基线记录。
3. 向我汇报：检测到的 CLI 路径与模型、Skill 与规则写入路径、以及冒烟测试结果。
