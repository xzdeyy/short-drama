# Flexible Short Drama & Animation Screenplay Skill

一个面向短剧、短篇动画、微型连续短剧与长篇微短剧的灵活编剧 Skill。

这个版本在原 `short-drama` 基础上扩展了：

- 用户脑洞 / 用户梗概正式输入
- 原著 / 民间故事改编
- 已有剧本重写
- 剧情锁定 `mustKeep`
- 单篇动画 3–6 分钟
- 微型连续短剧 2–5 集，每集默认约 2 分钟
- 短篇连续剧 6–12 集
- 原长篇微短剧 40–100 集
- 古代志怪、民间奇谈、黑色寓言、古代悬疑、人性寓言
- 9–15 秒动画制作分段 `/segments`

---

## 体量模式

| 模式 | 集数 | 默认时长 |
|---|---:|---:|
| 单篇动画 | 1 集 | 总长 3–6 分钟 |
| 微型连续短剧 | 2–5 集 | 每集约 2 分钟；允许 90–150 秒 |
| 短篇连续剧 | 6–12 集 | 每集约 1–3 分钟 |
| 长篇微短剧 | 40–100 集 | 每集约 1–3 分钟 |
| 自定义 | 用户指定 | 用户指定 |

---

## 创作来源

`/start` 支持五种入口：

1. AI原创
2. 用户脑洞
3. 用户梗概
4. 原著 / 民间故事改编
5. 已有剧本重写

用户只给一句脑洞也可以开始。

例如：

```text
一个书生同时遇上一狐一鬼，
两个女人都说对方不是人，
书生却以为她们只是在争风吃醋。
```

Skill 会围绕该脑洞补全故事，而不是自动换成另一个故事。

---

## 剧情锁定

新增核心字段：

```json
{
  "storyIdea": "",
  "mustKeep": [],
  "canChange": [],
  "forbiddenChanges": [],
  "endingPreference": ""
}
```

`mustKeep` 优先级高于题材、爽点、反派、付费卡点等模板。

---

## 原著改编

支持四档忠实度：

- A 高度忠实 `faithful`
- B 保留核心情节，允许压缩 `core_compression`
- C 保留人物与核心矛盾，大幅重构 `major_restructure`
- D 仅取灵感 `inspired`

例如：

```text
创作来源：原著改编
原著：《聊斋志异·莲香》
主题材：古代志怪
副题材：情感 + 悬疑
忠实度：B
```

---

## 新增题材

在原有都市情感、霸总、甜宠、重生穿越、悬疑、喜剧等基础上，新增：

- 古代志怪
- 民间奇谈
- 黑色寓言
- 古代悬疑
- 人性寓言

“聊斋改编”属于创作来源，不单独作为题材；具体作品通常归入“古代志怪”。

---

## 推荐工作流

### 单篇动画

```text
/start
→ /story
→ /plan
→ /characters
→ /outline
→ /script
→ /segments
→ /review
→ /export
```

### 微型连续短剧

```text
/start
→ /story
→ /plan
→ /characters
→ /outline
→ /episode 1-N
→ /segments
→ /review
→ /export
```

默认 2–5 集，每集约 2 分钟。

### 长篇微短剧

```text
/start
→ /story（可选）
→ /plan
→ /characters
→ /outline
→ /episode
→ /review
→ /compliance
→ /export
```

长篇模式继续保留原版付费卡点、爽点、钩子、反派层级等方法论，但这些模板不能覆盖用户锁定的剧情。

---

## `/segments` 动画制作分段

把完整剧本拆成 9–15 秒制作段：

```text
【分段1】00:00-00:12｜12秒
剧情功能：开场钩子
首态：……
动作 / 对白：……
末态：……
连续性锁定：下一段必须从……开始

【分段2】00:12-00:25｜13秒
……
```

核心规则：

- 每段默认 9–15 秒
- 不机械固定 12 秒
- 后一段首态必须承接上一段末态
- 人物站位、手中物、伤势、门窗、道具位置保持连续
- 不在完整动作或完整句子中间恶意切断

---

## 安装

### 全局安装

```bash
# macOS / Linux
git clone https://github.com/xzdeyy/short-drama.git ~/.claude/skills/short-drama

# Windows (Git Bash)
git clone https://github.com/xzdeyy/short-drama.git "$USERPROFILE/.claude/skills/short-drama"
```

### 项目级安装

```bash
cd your-project
git clone https://github.com/xzdeyy/short-drama.git .claude/skills/short-drama
```

---

## 主要参考文件

```text
references/
├── story-source.md
├── adaptation-rules.md
├── short-form-rhythm.md
├── segment-rules.md
├── genre-guide.md
├── opening-rules.md
├── rhythm-curve.md
├── paywall-design.md
├── satisfaction-matrix.md
├── villain-design.md
├── hook-design.md
└── compliance-checklist.md
```

---

## License

保留原项目许可证，详见 `LICENSE`。
