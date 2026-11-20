# Agent Skills

个人 AI Agent Skills 仓库，集中管理用于论文理解、精读、批判性分析与深度阅读的 `SKILL.md` 技能包，支持在 **云端（Antigravity）** 与 **本地（Antigravity / Claude Code / OpenCode 等）** 同步使用。

## 已收录 Skills

| Skill 名称 | 目录 | 核心用途 | 上游来源 |
| :--- | :--- | :--- | :--- |
| **paper-review** | `skills/paper-review/` | 单篇论文深度评读（CrossRef 引用核查、GRADE 证据等级计算、论证漏洞检测、偏倚风险评估） | [drpwchen/paper-review-and-digest](https://github.com/drpwchen/paper-review-and-digest) (MIT) |
| **paper-digest** | `skills/paper-digest/` | 单篇论文快速内容吸收（三层渐进式结构梳理 + 主动回忆自测卡） | [drpwchen/paper-review-and-digest](https://github.com/drpwchen/paper-review-and-digest) (MIT) |
| **how-to-read-a-paper** | `skills/how-to-read-a-paper/` | 基于 Jason Eisner 与 Keshav 三遍精读法的高效论文阅读与笔记工作流 | [thisisrick25/how-to-read-a-paper](https://github.com/thisisrick25/how-to-read-a-paper) |
| **deep-reading-analyst** | `skills/deep-reading-analyst/` | 10+ 思维框架深度阅读分析（SCQA、5W2H、批判性思维、逆向思维、第一性原理、系统思维、六顶思考帽等） | [ginobefun/deep-reading-analyst-skill](https://github.com/ginobefun/deep-reading-analyst-skill) (MIT) |

---

## 使用方式（云端 + 本地同步）

### 1. 在任意项目中本地使用
将本仓库直接克隆为项目根目录下的 `.agent` 文件夹：

```bash
git clone https://github.com/IAOinthemoon/.agent.git .agent
```

或者将本仓库克隆到个人目录后，软链接到各工具的全局 Skills 目录：

```bash
git clone https://github.com/IAOinthemoon/.agent.git ~/.agent

# 例如链接到 Claude Code / 通用工具全局目录：
mkdir -p ~/.claude/skills
ln -s ~/.agent/skills/* ~/.claude/skills/

# 或者链接到 OpenCode 全局目录：
mkdir -p ~/.config/opencode/skills
ln -s ~/.agent/skills/* ~/.config/opencode/skills/
```

更新技能时只需在仓库目录执行：

```bash
git pull
```

### 2. 在 Antigravity 云端使用
- **项目级**：在 Antigravity 项目资源中关联本仓库（或将本仓库作为项目 `.agent/` 子目录）。
- **全局级**：通过 `save_skill` 将上述 `skills/` 目录保存到云端全局 Skill 中，即可在所有云端对话中直接触发。
