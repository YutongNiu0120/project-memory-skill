# project-memory-skill

[English README](README.md)

## 1. 项目一句话

`project-memory` 是一个面向 Codex 的 skill，用来给代码仓库建立项目级持久记忆，让 agent 在跨会话再次进入项目时可以复用上下文，而不是每次从头重建。

## 2. 解决什么问题

agent 再次进入同一个仓库时，很多 token 消耗并不来自真正的编码，而是来自反复做这些事情：

- 重新理解项目是做什么的
- 重新定位真正的入口和关键模块
- 重新确认项目里的约定和架构限制
- 为了恢复上下文，再次大面积扫描代码

`project-memory` 的目标，就是把这种重复发生的项目理解成本，沉淀成仓库内部可以持续复用的项目记忆。

## 3. 核心功能

- 在仓库内部维护项目级持久记忆
- 生成项目概览、功能索引和开发方法论文档
- 记录当前关注点、里程碑和架构决策
- 区分可刷新的项目上下文和长期保留的项目历史
- 在后续会话中优先复用 `.project-memory`
- 减少重复的大面积扫描，降低 token 消耗
- 默认中文输出项目文档，同时保留代码标识、路径和配置原文

## 4. 工作流程

```text
session 1
   ↓
扫描仓库
   ↓
生成项目记忆
   ↓
写入 .project-memory/

后续 session
   ↓
读取 .project-memory/
   ↓
跳过不必要的大范围扫描
   ↓
更快进入编码状态
```

再次进入项目时，推荐顺序是：

1. 先读 `AGENTS.md`
2. 再读 `.project-memory/README.md`
3. 再读 `generated/project-summary.md`
4. 再读 `generated/development-playbook.md`
5. 再读 `generated/feature-index.md`
6. 按任务需要补读 `memory/` 下的历史记录
7. 最后再决定是否还需要大范围扫描代码

## 5. 安全设计

- 项目记忆直接保存在仓库内的 Markdown 文件中
- 可刷新内容和长期历史内容分目录管理
- `.project-memory/memory/` 下的长期内容在刷新时不应被覆盖
- `generated/development-playbook.md` 的人工积累区应被保留
- 所有项目记忆都可人工审阅、编辑和校验

## 6. 技术实现

`project-memory` 采用纯文本优先设计：

- `.project-memory/generated/` 存放可刷新的项目上下文
- `.project-memory/memory/` 存放长期保留的项目历史
- `.project-memory/README.md` 作为后续会话的阅读入口
- `project-memory/templates/` 提供默认模板
- `project-memory/references/file-guides.md` 约束文件职责和更新方式

项目记忆目录结构：

```text
.project-memory/
  README.md
  generated/
    project-summary.md
    feature-index.md
    development-playbook.md
  memory/
    milestones.md
    decisions.md
    current.md
```

仓库里也包含 `project-init`，但它只是初始化辅助。它的作用是在 Codex `/init` 的基础上，把 `.project-memory` 也一起初始化好。

## 7. 快速开始

把 skill 放到 Codex skills 目录：

```text
~/.codex/skills/project-memory
~/.codex/skills/project-init
```

推荐用法：

1. 新仓库第一次接入时，运行 `project-init`
2. 让它创建或刷新 `AGENTS.md`，并初始化 `.project-memory/`
3. 后续会话中，把 `project-memory` 作为项目上下文的默认入口
4. 在大范围扫描仓库前，优先先看 `.project-memory`
5. 每次做完比较重要的任务后，按需刷新生成内容或补充长期记忆
