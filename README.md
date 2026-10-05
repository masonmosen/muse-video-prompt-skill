# Muse Video Prompt Skill

**Muse 内置视频（Muse Video）提示词实战 Skill：从提示词到成片的完整闭环**

[English](#english) | [简体中文](#简体中文)

---

## 简体中文

做 AI 短视频最难的不是点"生成"，而是**提示词写得准、长片拼得连贯、人物不崩**。
这个 skill 是一套为 Muse 内置视频打磨的实战工作流：

- **六段式提示词模板**：时长画幅 / 人物 / 场景 / 节拍时间轴 / 镜头语言 / 声音 / 对白 / 限制清单，另有 POV 生活流、口播、多段长片三个变体
- **多段拼接**：单条 10 秒是硬上限？按节拍拆段，用 snapshot 接续保连贯，ffmpeg 无损拼成 30 秒+
- **抽帧验证**：每段自动抽帧自查，哪些吃进提示词、哪些偏了，白纸黑字写清楚
- **诚实线**：内置视频锁脸弱、参考图不一定像——动手前先说边界，不拿话术包装
- **案例库**：每个实验沉淀一张案例卡（提示词要点 / 结果 / 偏差 / 教训），随用随长

### 和 `muse-video-skill` 的区别

[LuoJiangYong/muse-video-skill](https://github.com/LuoJiangYong/muse-video-skill)（MIT）是优秀的**前期策划引擎**（剧本/分镜/美术 → 编译成下游模型指令），它的工程化思想（thin center + 按需加载 + 确定性脚本）是本 skill 的架构蓝本。
本 skill 定位不同：**内置视频的实战闭环**——写完提示词直接生成、拼接、验证，全流程在一套里跑完，不依赖下游工具。

### 目录结构

```
muse-video-prompt-skill/
├── SKILL.md                  # 入口：工作流 + 操作规则（通用 Agent Skills 格式）
├── CONSTITUTION.md           # 设计宪法：诚实线 / 用户定稿 / 短闭环 / 沉淀 / 精益
├── README.md
├── LICENSE                   # MIT
├── references/               # 按需加载的领域知识
│   ├── prompt-template.md    # 六段式提示词模板 + 三个变体
│   ├── model-notes.md        # 内置 Muse Video 能力边界（实测）
│   ├── consistency.md        # 人物一致性实战策略
│   ├── dialogue.md           # 对白规范（默认台湾腔国语）
│   ├── stitch-workflow.md    # 分段生成 → 拼接 → 验证
│   └── cases/                # 案例库（INDEX + 按日期归档的案例卡）
└── bin/
    └── extract_frames.py     # 抽帧自查脚本
```

### 安装

```bash
git clone https://github.com/masonmosen/muse-video-prompt-skill.git
# 放入所用 Agent 的 skills 目录，例如：
#   Claude Code → ~/.claude/skills/muse-video-prompt-skill/
```

### 适用与不适用

- ✅ 视频提示词实验、短视频生成、多段拼长片、提示词写法打磨
- ❌ 需要强锁脸的项目 → 走 Seedance / 第三方视频模型（本 skill 会明确告诉你）

---

## English

A battle-tested workflow skill for Muse's built-in video generation (Muse Video): prompt writing with a six-part template, multi-segment generation with snapshot chaining, lossless stitching, and frame-extraction verification — a complete loop from prompt to final cut.

- **Six-part prompt template** (+ POV / talking-head / multi-segment variants)
- **Multi-segment stitching** for videos beyond the ~10s single-clip limit
- **Frame-extraction verification** after every generation
- **Honesty-first**: face-lock is weak on built-in video — stated upfront, never oversold
- **Growing case library**: every experiment becomes a case card

Architecture inspired by [LuoJiangYong/muse-video-skill](https://github.com/LuoJiangYong/muse-video-skill) (MIT); all content here is original, battle-tested against real generations.

## License

MIT © 2026 Mason Mosen
