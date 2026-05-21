# Novel Writer Skill — 小说写作助手

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

一个 Claude Code Agent Skill，帮助网文作者从细纲到完整章节进行创作。支持本地写作、长篇写作记忆管理、以及在线发布到番茄小说平台。

---

## 功能概览

| 功能 | 说明 |
|------|------|
| **写新章节** | 读取细纲 + 小说设定 → 生成完整章节 → 保存到本地或发布到番茄 |
| **长篇写作模式** | 配套记忆管理系统（bible / summary / recent / status / 人物卡），支持跨 session 续写 |
| **人物卡管理** | 基于人物卡的一致性校验，自动检测性格偏差并向作者确认 |
| **卡文助手** | 分析作者已有章节的文风，提供 2-3 个不同方向的简写示例（300-800字）供选择 |
| **发布到番茄** | 通过 MCP 浏览器自动上传到 fanqienovel.com，支持多章分次存草稿 |
| **续写** | 自动读取最新章节衔接生成下一章，卡文时自动转卡文助手 |
| **细纲管理** | 新建、查看、修改细纲文件 |
| **进度查看** | 展示章节列表、字数统计、写作进度 |

---

## 文件结构

```
novel-writer-skill/
├── README.md                       # 本文件
├── .gitignore
└── novel-writer/
    ├── SKILL.md                    # 技能主定义（触发条件 + 完整工作流）
    └── novel/                      # 数据目录模板
        ├── requirements.md         # 小说设定模板（题材、角色、世界观、文风要求）
        └── outlines/
            └── 示例细纲模板.md      # 细纲模板参考
```

### 完整数据目录（使用后生成）

```
novel/
├── requirements.md         # 小说设定
├── current_state.md        # 写作进度追踪
├── outlines/               # 细纲目录
├── chapters/               # 已生成的章节
├── draft/                  # 长篇写作模式章节正文
├── characters/             # 人物卡
├── memory/                 # 长篇写作模式记忆
│   ├── bible.md            # 核心设定
│   ├── outline.md          # 章节大纲列表
│   ├── summary.md          # 章节摘要（带自动压缩和文件轮转）
│   ├── recent.md           # 最近2章全文
│   └── status.md           # 进度、伏笔、人物情绪状态
└── tmp_drafts/             # 卡文助手留存素材
```

---

## 安装方式

### 作为 Claude Code Skill 安装

```bash
# 1. 克隆仓库
git clone https://github.com/xin-yi33/-novel-writer-skill.git

# 2. 将 novel-writer/ 目录放入你的 Skills 目录

# 3. 注册并启用
cd /path/to/skills-dir
mcp__skills__skills init novel-writer
mcp__skills__skills register novel-writer
```

### 手动使用

直接对 Claude 说以下关键词即可自动触发（无需额外安装）：

- 写小说 / 生成小说章节 / 帮我写小说
- 根据细纲生成文章
- 卡文了 / 写不下去了 / 不知道怎么续
- 上传到番茄 / 查看进度 / 管理细纲

---

## 快速开始

1. 对 Claude 说"我要写小说"
2. 填写 `novel/requirements.md` 中的小说设定
3. 创建第一个细纲文件放入 `novel/outlines/`
4. 开始写作！

---

## 更新日志

### v1.0.1 (2026-05-22)

- **重构 SKILL.md 结构** — 消除 A 节（写新章节）、E 节（续写）、I 节（长篇写作模式）之间的人物卡管理重复逻辑，统一收敛到 H 节（人物卡管理）为唯一权威来源
- **移除冗余的工作流引导** — 删除顶部"第一步/第二步/第三步"的固定流程（与 F 节查看进度重复），改为简洁的操作索引
- **所有人物卡操作统一引用** — A3-1 预检、A4 保存、E 续写、I3 更新流程中涉及人物卡的部分全部改为引用 H 节
- **优化 A3-2 章节末尾要求** — 将"章节末尾必须有钩子"改为"根据作者需求决定"

### v1.0.0 (2026-05-13)

- 初始发布
- 基础章节生成（本地模式 + 在线发布到番茄小说）
- 卡文助手（文风分析 + 多方向续写方案）
- 长篇写作模式（记忆文件系统 + 跨 session 续写）
- 细纲管理与进度追踪

---

## 卡文助手

当你说"卡文了"，技能会自动：

1. 读取你最近 3-5 章，分析你的文风特点
2. 询问具体的卡文点（情节走向 / 细节卡壳 / 情绪不对 / 过渡困难 / 开篇困难）
3. 生成 2-3 个不同方向的 300-800 字简写示例
4. 选中方案后可扩展为完整章节

---

## License

本项目基于 MIT 协议开源。

---

*由 Claude Code Agent Skill 构建*
