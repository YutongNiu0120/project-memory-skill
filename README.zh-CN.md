# Codex Project Bootstrap Skills

[English README](README.md)

这是两个面向 Codex 的纯文本项目启动技能，用来把一个代码仓库快速变成“适合长期协作”的工作空间：

- `project-init`：初始化仓库，创建或刷新 `AGENTS.md` 和 `.project-memory`
- `project-memory`：维护仓库级项目记忆，区分可重建上下文与长期人工沉淀

没有 Python 运行时依赖。没有额外脚本后端。没有隐藏状态。只有 AI 可以直接读写、你也能直接检查的 Markdown。

如果这套思路能帮你少走很多“每次都重新扫仓库”的重复路，欢迎点个 Star。

## 为什么做这个仓库

很多 agent skill 明明只是维护几份项目文档，却要额外带一套脚本、CLI，甚至本地 backend。结果就是：

- 使用链路变重
- 可读性下降
- 状态不透明
- 定制成本更高

这个仓库反过来做：

- 以文本为中心
- 让模型直接处理自己看得懂的文件
- 让所有状态对用户完全透明
- 保留人工沉淀，而不是一刷新就覆盖

这样更轻、更直观，也更适合真实项目长期使用。

## 仓库包含什么

### `project-init`

适合第一次接手一个仓库时使用，让 Codex 快速把项目初始化到“可重复协作”的状态。

特点：

- 基于真实仓库信息创建或刷新 `AGENTS.md`
- 直接初始化 `.project-memory`，不依赖脚本
- 自动保持 `AGENTS.md` 里的项目记忆区块一致
- 优先刷新，不做粗暴重写

### `project-memory`

适合在后续开发过程中持续维护仓库级记忆，让跨会话上下文积累下来。

特点：

- 明确区分可重建内容和长期人工内容
- 把可刷新信息放在 `.project-memory/generated/`
- 把长期沉淀放在 `.project-memory/memory/`
- 刷新时保留人工积累区
- 默认中文输出，更适合中文研发协作

## 核心优势

- 纯文本优先：AI 直接读写 Markdown
- 可审计：所有记忆都是明文文件
- 更安全的刷新方式：可重建内容和长期内容分层管理
- 更贴近真实项目：不是 demo 风格，而是面向长期仓库协作
- 中文友好：项目文档默认中文，但保留代码标识和路径原文

## 目录结构

```text
.
├── project-init/
│   ├── agents/
│   │   └── openai.yaml
│   └── SKILL.md
└── project-memory/
    ├── agents/
    │   └── openai.yaml
    ├── references/
    │   └── file-guides.md
    ├── templates/
    │   ├── README.md
    │   ├── agents-block.md
    │   ├── generated/
    │   └── memory/
    └── SKILL.md
```

## 安装方式

把两个 skill 目录放到你的 Codex skills 目录下：

```text
~/.codex/skills/project-init
~/.codex/skills/project-memory
```

如果你习惯维护单一工作副本，也可以用软链接。

## 推荐用法

1. 第一次接手仓库时使用 `project-init`
2. 让它创建或刷新 `AGENTS.md`
3. 让它初始化 `.project-memory/`
4. 后续开发中使用 `project-memory` 持续刷新生成内容，并沉淀长期项目知识

## 适合谁

- 需要跨多个仓库使用 Codex 的工程师
- 希望保留项目上下文，但不想引入额外工具链的团队
- 更信任明文 Markdown，而不是黑盒自动化的人
- 希望项目说明优先中文，但代码、路径、配置保持原文的协作场景

## 设计原则

- 只写经过验证的事实，不写空洞模板
- 能刷新就刷新，不轻易覆盖
- 生成内容和人工内容严格分层
- Markdown 优先
- 项目文档默认中文，除非用户明确切换语言

## 值得先看的文件

- `project-init/SKILL.md`
- `project-memory/SKILL.md`
- `project-memory/references/file-guides.md`
- `project-memory/templates/`

## 为什么这类仓库更值得 Star

这个仓库有意保持“小”，而“小”本身就是优势：

- 几分钟就能看懂整套机制
- 所有规则都能直接审阅
- 模板可直接改，不需要改代码
- 不需要排查本地脚本或后台状态

如果你也希望 Codex skill 保持轻量、透明、可长期演化，这个仓库就是按这个方向设计的。
