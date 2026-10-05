---
name: "muse_video_prompt_skill"
description: "Prompt engineering workflow skill for Muse built-in video generation (Muse Video): six-part prompt templates → generation → multi-segment stitching → frame verification. Muse 内置视频提示词实战：写提示词 → 生成 → 拼长片 → 抽帧验证的完整闭环。"
---

# Muse Video Studio — 内置视频实战工作流

## Purpose
Muse 内置视频（Muse Video）从提示词到成片的完整闭环：写提示词、生成、长片分段拼接、抽帧验证。不做锁脸承诺；需要锁脸的线走 Seedance 第三方。

## Workflow
1. **写提示词**：按 `references/prompt-template.md` 六段式模板写。用户定稿后原样传入 `media.generate_video`，不擅自改写、扩写。用户长期默认项（台湾腔国语对白）见 `references/dialogue.md`，单独标注后附加。
2. **生成**：纯文本优先；要用参考图时，先确认文件存在且文件名为 ASCII（中文文件名上传会被上游 400 拒绝）。能力边界见 `references/model-notes.md`。
3. **长片（>10 秒）**：按节拍拆成多段，每段一个独立提示词；后一段用前一段的 `resume_from_snapshot_id` 接续，保证人物场景连贯；最后 ffmpeg 拼接。见 `references/stitch-workflow.md`。
4. **验证**：每段用 `bin/extract_frames.py` 抽帧自查；画面问题自己修。音频、口型、动态连贯性我看不见听不见，必须明说、交用户终验。
5. **沉淀**：每个实验写一张案例卡进 `references/cases/`（提示词要点、结果、偏差、教训）。

## Output Contract
- 成片视频文件（`workspace/prompt-experiments/<日期>/`）；长片额外交付拼接版，保留分段文件。
- 抽帧自查结论：哪些吃进了提示词、哪些偏了、偏差原因推测。
- 明确列出需用户终验的项（音频、口型、动态细节），不含糊。

## Operating Rules
1. 所有回复用简体中文。
2. 提示词以用户定稿为准；我写的版本先给用户看，确认后再跑。
3. 不承诺人物锁脸、不保证参考图一定像——这是模型能力边界（见 `references/consistency.md`），动手前先说。
4. 单条 10 秒是硬上限；用户要更长，主动给分段拼接方案，不只丢一条 10 秒。
5. 参考图只传 ASCII 文件名；`/tmp` 是临时的，传图前先确认文件存在。
6. 每次生成后必须抽帧看过再交付；没看过的片子不说"没问题"。
7. 任何情况下不编造画面/声音细节——没验过的就说没验过。
