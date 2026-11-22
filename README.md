<div align="center">

# cli-quota-collaboration

**主模型（Antigravity / Codex）+ 本机免费编码 CLI（CodeBuddy CLI 等）常态化协同省额度方案**

[简体中文](./README.md) · [English](./README.en.md) · [一键接入提示词](./SETUP_PROMPT.md) · [Release Notes](./RELEASE_NOTES.md)

<img src="./assets/hero.jpg" alt="Gemini & Hunyuan Collaboration" width="460" />

*“老板再多派点轻量活，主模型只管架构拆解和验收，重体力活交给我！”*

</div>

---

## 为什么做这个项目？

在日常 AI 辅助研发中，**长日志分析、单测补齐、批量样式/文案修改、独立脚本编写、文档与日报生成**往往最消耗主模型（Gemini / Claude / GPT）的高级套餐额度，但这些工作其实并不需要最强推理模型亲自逐行输出。

`cli-quota-collaboration` 提供一套**开箱即用、全脱敏、经过真实高频开发验证**的双模型协同工作流：
- **主模型（Antigravity / Codex）**：聚焦需求澄清、架构设计、跨模块耦合重构、浏览器/MCP/视觉协同与**分级验收**。
- **本机免费/低成本 CLI（如 CodeBuddy CLI `hy4flash-free`）**：常态化承接边界清晰、独立性强、机械重复或高输出消耗的执行任务。

---

## 核心特性

- **常态化优先委派（无论剩余额度多少）**：每次执行任务前先拆解轻量/独立子任务外包给本地 CLI，不等到额度见底才临时补救。
- **清晰的任务决策表**：明确区分“主模型直出 / 必须委派 CLI / 主模型一条 shell 命令解决（如纯文件移动与跨盘扫描）”。
- **实战避坑固化**：
  - **Windows PowerShell 防转义**：长提示词先写入临时文件再通过管道传入（`Get-Content -Raw prompt.md | codebuddy -p ...`），彻底避免原生 `.exe` 参数剥离双引号。
  - **精确参考路径注入**：派单时直接附上精确参考文件路径，显著压低 CLI 盲找试错轮数与非致命工具报错。
  - **写前检查点与安全红线**：`acceptEdits` 前先核对 Git 状态或备份；严禁删目录、`git push`、`reset --hard` 及触碰密钥/运行时缓存。
  - **失败 2 次兜底 + 分级验收**：同一任务最多重试 2 次，失败立即由主模型接手；验收先看 `git diff --stat` 与测试结论，仅细查核心 diff。

---

## 实测效果参考

在一次真实多项目日常开发周期中（连续 **22 次**业务派单，全部运行在免费模型 `hy4flash-free`，`credit: 0`）：

| 指标 | 实测结果 |
| :--- | :--- |
| **任务一次通过率** | **19 / 22** 直接成功（仅 3 次因沙盒权限/跨盘限制触发兜底由主模型接手） |
| **累计分担交互** | **348 轮**模型调用，总耗时约 **47.9 分钟** |
| **实测分担 Tokens** | 输入 **1,828 万** + 输出 **28.8 万**（合计 **1,857 万 Tokens**） |
| **主模型额度节省（估算）** | 约 **600 万～900 万等效 Tokens**，其中最耗额度的 **28.8 万**长文/代码输出几乎 100% 转移到免费额度 |

---

## 30 秒快速开始

### 方式一：直接丢给 Antigravity / Codex 自动配置（推荐）
1. 确认本机已安装并登录至少一个本地编码 CLI（例如 [CodeBuddy CLI](https://www.codebuddy.ai/)）。
2. 将本仓库中的 **[SETUP_PROMPT.md](./SETUP_PROMPT.md)** 全文发送给你的 **Antigravity** 或 **Codex** 客户端。
3. 客户端会自动探测 CLI、安装 `SKILL.md`、追加全局规则并完成冒烟测试。

### 方式二：手动安装 Skill
- **Antigravity**：将 `SKILL.md` 复制到 `~/.gemini/config/skills/cli-quota-collaboration/SKILL.md`
- **Codex**：将 `SKILL.md` 复制到 `~/.codex/skills/cli-quota-collaboration/SKILL.md`

---

## 仓库结构

```text
cli-quota-collaboration/
├── assets/
│   └── hero.jpg                     # 主图（Gemini 娘 & 混元娘协同插画）
├── README.md                        # 中文发布页
├── README.en.md                     # English Release Page
├── RELEASE_NOTES.md                 # v1.0.0 GitHub Release 发布说明
├── SETUP_PROMPT.md                  # 丢给 Antigravity / Codex 直接使用的一键接入提示词
├── SKILL.md                         # 标准 Skill 规范文件（全脱敏）
├── LICENSE                          # MIT 开源协议
├── .gitignore
└── templates/
    ├── CLI_PROJECT_RULES.md         # 项目级规则模板（可重命名为 CODEBUDDY.md / AGENTS.md）
    └── dispatch_log.csv             # 派单效果复盘日志模板
```

---

## License

[MIT](./LICENSE)
