# Changelog

## v1.0.0

PersonaForge initial public release.

### Framework

- **RP Core** — 全局常驻的十条底层原则与优先级（`rp-core.md`）。
- **Story Memory** — 十段长期状态结构；事实 / 知识 / 理解三层分离；取代式更新规则。
- **Active State** — 当前场景工作集提取，场景结束即弃。
- **Quality Check** — 四种根因、十二项失败模式（问题 / 根因 / 修正）、症状定位表。

### Skills

Five modular roleplay skills, each self-contained (`SKILL.md` + `references/`, no dependency outside its own directory):

- **Character Performance** — 性格推导链、特质冲突取舍、反差来源、默认不解释反差。
- **Dialogue & Subtext** — 四层过滤、直接性先由人后由代价、潜台词形状库、对白身份差异。
- **Relationship & Emotion** — 多维关系、关系变化链与三条并列来源、情绪持续、压住与消失的区分。
- **Character Agency** — 角色自有生活、被动与抢戏两端的判据、三层目标、目标来源与边界。
- **Story Progression** — 目标不相容引擎、新事件三检验、节奏与密度、伏笔与悬念。

### Metadata & Docs

- Added OpenAI Skill metadata structure (`skills/*/agents/openai.yaml`，仅 UI 字段：`display_name`、`short_description`)。这是格式适配，不代表已通过任何环境的运行验证。
- **Examples** — `basic-roleplay.md`、`relationship-continuity.md`、`knowledge-and-beliefs.md`。
- **Architecture** — `docs/architecture.md`：分层理由、框架层与 Skill 层的可移植性规则、修订约定。
- **Compatibility** — `COMPATIBILITY.md`：Tested / Conceptually Compatible / Not Yet Verified 三档，Tested 目前为空。

### 不含内容

题材扩展层（成人向、战斗、RPG 数值、角色卡与世界书模板）、任何代码、脚本、安装器或自动路由器。
