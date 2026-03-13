# project-memory-skill

[English README](README.md)

`project-memory` 是一个面向 Codex 的纯文本 skill，用来给代码仓库建立项目级记忆，让上下文能够跨会话持续积累。

这个仓库的主角是 `project-memory`。`project-init` 只是一个配套技能，用来在第一次接手仓库时顺手把初始化做好。

## `project-memory` 解决什么问题

很多时候，agent 在一个项目里最浪费 token 的部分，不是改代码，而是反复做这些事情：

- 重新理解项目是干什么的
- 重新定位核心模块和入口
- 重新确认项目约定和已有决策
- 重新大面积扫描代码找线索

`project-memory` 的目标就是把这些反复发生的“项目理解成本”沉淀下来，变成仓库自己的长期记忆。

这样在后续会话再次进入项目时，agent 可以先读 `.project-memory`，再决定要不要继续大范围扫描代码。

## 核心能力

- 在仓库内维护项目级记忆，而不是只停留在当前对话
- 用 Markdown 直接保存和更新记忆，结构清晰，可人工审阅
- 区分“可重新生成的项目概览”和“需要长期保留的项目历史”
- 沉淀项目的当前关注点、关键决策、里程碑和方法论
- 在跨会话再次访问项目时，优先参考 `.project-memory` 的历史记录
- 减少重复的大面积扫描，降低 token 浪费

## 目录结构

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

各部分作用：

- `generated/`：可根据当前仓库状态刷新的项目概览和导航文档
- `memory/`：长期保留的项目历史记录，不应被刷新覆盖
- `README.md`：下次进入项目时的阅读顺序入口

## 再次进入项目时的推荐流程

当 agent 在后续会话再次进入同一个项目时，推荐顺序是：

1. 先读 `AGENTS.md`
2. 再读 `.project-memory/README.md`
3. 再读 `generated/project-summary.md`
4. 再读 `generated/development-playbook.md`
5. 再读 `generated/feature-index.md`
6. 按任务需要补读 `memory/` 下的历史记录
7. 最后才决定是否还需要大范围扫描代码

这也是这个 skill 最核心的价值来源：优先复用历史理解，而不是每次从头探索。

## 配套技能：`project-init`

仓库里也包含 `project-init`，但它只是辅助角色。

它的用途主要是第一次初始化项目时省事一些，在 Codex `/init` 的基础上，继续把 `project-memory` 也一起初始化好。它负责：

- 创建或刷新 `AGENTS.md`
- 初始化 `.project-memory`
- 对齐 `AGENTS.md` 里的项目记忆区块

初始化完成后，后续主要依赖的应该还是 `project-memory`。

## 仓库结构

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

把这两个 skill 放到你的 Codex skills 目录：

```text
~/.codex/skills/project-memory
~/.codex/skills/project-init
```

## 使用方式

1. 新仓库第一次接入时，用 `project-init`
2. 让它创建或刷新 `AGENTS.md`，并初始化 `.project-memory/`
3. 后续会话中，把 `project-memory` 作为项目上下文的默认入口
4. 在大范围扫描仓库前，优先先看 `.project-memory` 的历史记录
5. 每次做完比较重要的任务后，按需更新生成内容或长期记忆

## 主要优势

- 让 agent 更快理解项目
- 形成项目级记忆，并且可以持续沉淀
- 减少重复的大面积扫描，节省 token
- 项目知识透明、可编辑、可审阅
- 让后续会话更快进入“项目内工作状态”

## 建议先看

- `project-memory/SKILL.md`
- `project-memory/references/file-guides.md`
- `project-memory/templates/`
- `project-init/SKILL.md`
