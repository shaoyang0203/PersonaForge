# PersonaForge

**Character Reasoning Framework for Long-Form Roleplay**

> Character cards define who a character is.
> PersonaForge helps determine how that character interprets, decides, acts, changes, and remembers across long-form roleplay.

角色卡决定人物是谁。PersonaForge 处理的是：已经确定的这个人，在当前处境下会如何理解事件、作出判断、采取行动，如何改变，以及留下了什么仍然成立的状态。

这是一套纯 Markdown 的角色行为推导与状态管理框架，通过 RP Core、按需加载的 Skills 与 Runtime Memory，把静态设定转化为连贯、有因果、有自主性的长期角色表现。

## 它不是什么

- 不是角色卡，也不含角色卡模板。
- 不是世界书，也不含世界书模板。
- 不是成人内容生成模板——本框架不规定题材。
- 不是小说写作框架或编剧模板。
- 不是固定文风 Prompt，不约束句子怎么写。
- 不是好感度 / RPG 数值系统，没有任何计分、等级、阶段表。

它处理人物一致性、关系、情绪、对话、角色自主性、剧情因果与长期状态。题材属于独立的可选层，不进入 RP Core。

## 仓库与 Skill 的关系

PersonaForge 是一个 **roleplay framework repository**，不是一个单独的 Skill。`skills/` 下的五个目录各自是可以独立封装、独立使用的 Skill。

```text
PersonaForge
│
├── RP Core                常驻：底层原则
├── Runtime                状态：Story Memory / Active State
├── References             诊断：quality-check
├── Examples               说明：三个端到端示例
│
└── Skills                 五个可独立封装的能力域
    ├── character-performance
    ├── dialogue-subtext
    ├── relationship-emotion
    ├── character-agency
    └── story-progression
```

每个 Skill 自带 `SKILL.md`、`references/`、`agents/openai.yaml`，并且**不引用自己目录以外的任何文件**——被单独复制出去也能正常理解与执行。与框架层一起使用时，它们能读到 RP Core 与 Runtime Memory 提供的长期状态，效果更好；这是叠加，不是依赖。

## 运行结构

```text
Character Card / World State
            │
            ▼
         RP Core
            │
            ▼
     Relevant RP Skills
            │
            ▼
       Active State
            │
            ▼
       Roleplay Output
            │
            ▼
       Consequences
            │
            ▼
      Story Memory
            │
            └──────────► Next Scene
```

| 层 | 负责 | 位置 |
| --- | --- | --- |
| Character Card | 这个人是谁 | 由使用者提供，本仓库不含模板 |
| RP Core | 永久有效的最低层角色扮演原则 | `rp-core.md` |
| Skills | 按当前场景按需加载的具体表演能力 | `skills/*/SKILL.md` + `references/` |
| Active State | 从长期记忆中提取当前场景真正参与推理的信息 | `runtime/active-state.md` |
| Story Memory | 保存长期事实、关系、知识边界、错误理解、承诺与未闭合事务 | `runtime/story-memory.md` |
| Quality Check | 出问题时的诊断手册 | `references/quality-check.md` |

## 核心因果链

```text
经历
↓
理解
↓
判断
↓
行为
↓
后果
↓
新状态
```

大多数模块都挂在这条链上。跳过"理解"，人物就会突变；跳过"后果"，世界就没有记忆。同一句设定在不同处境下推出不同行为，这是本框架的基本假设：**角色卡给的是原因，不是动作。**

## Memory 的三层模型

多数长期角色扮演崩在这里：模型知道一切，于是角色也跟着知道一切。

```text
Objective Fact
≠
Character Knowledge
≠
Character Belief / Interpretation
```

```text
客观发生了什么
≠
角色知道什么
≠
角色如何理解
```

例：

```text
事实：
B 与 C 私下见过面。

A 知道：
B 与 C 私下见过。

A 的理解：
B 和 C 可能正在隐瞒某件事。
```

第三层完全可能是错的。只要角色还没拿到足以推翻它的新证据，这个错误的理解就应该继续影响他的判断与行为。完整字段与维护规则见 `runtime/story-memory.md`，端到端示例见 `examples/knowledge-and-beliefs.md`。

## 五个 Skill

| Skill | 负责 | 关键边界 |
| --- | --- | --- |
| [character-performance](skills/character-performance/SKILL.md) | 从性格、经历、处境和内部矛盾推导人物行为 | 不要为了让人物显得更复杂而使用 |
| [dialogue-subtext](skills/dialogue-subtext/SKILL.md) | 人物语言习惯、自然对白、表达代价与潜台词 | 不要求所有人物含蓄 |
| [relationship-emotion](skills/relationship-emotion/SKILL.md) | 关系的多维变化与情绪连续性 | 不使用好感度数值；情绪残留不必每轮显性表现 |
| [character-agency](skills/character-agency/SKILL.md) | 防止角色退化成等待用户输入的被动 NPC | 自主性不等于不断制造事件 |
| [story-progression](skills/story-progression/SKILL.md) | 从已有目标、摩擦、选择与后果中产生剧情推进 | 低频能力，不要因为场面安静就触发 |

## 安装与使用

本项目是纯 Markdown：没有代码、没有依赖、没有安装程序。加载方式取决于你的环境。

### A. 使用完整 PersonaForge 框架

适合能够组合以下三件事的环境：

```text
RP Core（常驻）
+ Skills（按需注入当前相关的能力域）
+ Runtime Memory（在场景之间维护状态文本）
```

`rp-core.md` 约 1100 中文字，作为全局常驻片段。需要时整段追加某个 `SKILL.md`（各约 900–1300 中文字），用完撤掉。状态按 `runtime/` 描述的结构由你或你的应用维护。

不建议把五个 Skill 与全部 references 一次性常驻：那会让低频规则长期占用上下文，也正是本项目分层结构的初衷（见 `docs/architecture.md`）。

### B. 单独使用某个 Skill

如果环境支持独立的 Agent Skills，可以只安装你需要的那几个目录：

```text
skills/character-performance/
skills/dialogue-subtext/
skills/relationship-emotion/
skills/character-agency/
skills/story-progression/
```

**单独 Skill 可以独立工作**：每个 Skill 内部自足，不读取目录外文件。**完整框架额外提供 RP Core 的底层原则与 Runtime Memory 的长期状态管理**——尤其是跨场景的信息边界与错误理解，那部分不属于任何单个 Skill。

`skills/*/SKILL.md` 顶部带 `name` 与 `description` frontmatter，`description` 同时写明"何时该加载"和"何时不该加载"；`agents/openai.yaml` 提供 OpenAI Skill 格式所需的 UI metadata。请按你所用客户端官方文档支持的方式挂载。本仓库**不声称任何具体客户端已经验证兼容**，实际状态见 `COMPATIBILITY.md`。

## 仓库内容

```text
rp-core.md                    全局常驻核心原则
skills/<name>/SKILL.md        五个能力域的核心推导方法（各自带 frontmatter）
skills/<name>/references/     详细展开、边界与例子（按需，一层）
skills/<name>/agents/         OpenAI Skill UI metadata
runtime/story-memory.md       长期状态结构与维护规则
runtime/active-state.md       当前场景工作集
references/quality-check.md   十二项失败模式诊断手册
examples/                     三个端到端示例
docs/architecture.md          分层理由、移植规则与修订约定
COMPATIBILITY.md              验证状态（含"未验证"的诚实说明）
CHANGELOG.md                  版本记录
LICENSE                       MIT
```

## 状态

v1.0.0。方法论已通过内容审查；**尚未经过完整的长轮次实跑验证**，兼容性也未系统性测试。发现问题欢迎提 issue，说明挂载方式、上下文预算、跑过的轮数，以及观察到哪一类失败模式（可用 `references/quality-check.md` 对号）。
