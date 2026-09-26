# MindDock

> 给 AI Agent 和 AI 创作者使用的可审查、可备份、可迁移的外部记忆工作流。

[English README](README.en.md)

MindDock 把项目知识、稳定偏好、待确认候选和日常记录整理成普通 Markdown 文件，让 Codex 可以按需读取，也让人可以直接用 Obsidian 打开、检查和备份。

它不是“永久记忆”魔法，而是一套边界清晰的工作流：知识进入 `inbox/`，重要事实保留来源，冲突等待人工确认，Native 定时任务只在能力可用时启用。

## 核心能力

- 项目级 `codex-memory/` 知识库，默认位于当前项目根目录。
- Obsidian 兼容的 Markdown 结构，不绑定数据库或专用插件。
- `inbox-first`：新事实、偏好和决策先进入候选区，再经过确认和提升。
- 全局 `AGENTS.md` 路由规则，帮助 Codex 在任务开始时读取正确的项目记忆。
- Native 每日和每周维护任务；能力不可用时提供准确的手动参数，并报告 `PARTIAL`。
- 幂等配置：保留已有笔记、等价规则和冲突任务，不静默覆盖。

## 快速开始

### 1. 安装 Skill

PowerShell：

```powershell
$skillsDir = Join-Path $env:USERPROFILE '.codex\skills'
New-Item -ItemType Directory -Force -Path $skillsDir | Out-Null
Copy-Item -Recurse -LiteralPath '.\skills\codex-memory-workflow' -Destination (Join-Path $skillsDir 'codex-memory-workflow')
```

POSIX shell：

```sh
mkdir -p "$HOME/.codex/skills"
cp -R ./skills/codex-memory-workflow "$HOME/.codex/skills/codex-memory-workflow"
```

如果目标目录已经存在，请先审查现有安装，再明确决定是否更新，不要直接覆盖。

### 2. 调用

```text
$codex-memory-workflow Configure this project using the portable defaults.
```

默认值：

- 知识库：`<当前项目根目录>/codex-memory`
- 每日维护：本地时间 22:00
- 每周维护：本地时间周日 22:30
- 新增长期信息：先进入 `inbox/`

### 3. 查看 Skill 细节

- [Skill 入口](skills/codex-memory-workflow/SKILL.md)
- [安装与验证](skills/codex-memory-workflow/README.md)
- [知识库结构与路由](skills/codex-memory-workflow/references/vault-layout.md)
- [每日提示词](skills/codex-memory-workflow/references/daily-prompt.md)
- [每周提示词](skills/codex-memory-workflow/references/weekly-prompt.md)
- [Native 配置与故障降级](skills/codex-memory-workflow/references/install-and-verify.md)

## 安全边界

MindDock 不读取或复制 Codex 会话数据库、完整聊天记录、密钥、Cookie、证书、客户敏感数据或外部账号数据；不创建替代后台服务，也不把外部知识库伪装成 Codex 原生 Memories。

配置成功不等于定时任务已经实际运行。Native 任务的首次真实运行需要在用户自己的 Codex 环境中单独观察和验证。

## 关于作者

Enhe（恩禾）是一名产品设计师、个人公司实践者和 AI Builder，持续探索如何用 AI 构建更高效、更自由的个人工作系统。

![关于作者：Enhe（恩禾）](assets/about-author.png)

图片授权说明：`assets/about-author.png` 为经作者授权用于本项目展示的个人与品牌视觉资料，不纳入 MIT License；未经许可不得复用。

## 许可证

本仓库中的 Skill、Markdown 文档、提示词和模板采用 [MIT License](LICENSE) 发布。`assets/about-author.png` 不在该许可证授权范围内。

## 项目定位

MindDock 的名字来自 “Mind” 与 “Dock”：让项目知识、AI Agent 和创作者工作流在一个清晰的入口停靠、连接和持续积累。
