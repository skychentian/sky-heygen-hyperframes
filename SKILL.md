---
name: sky-heygen-hyperframes
description: Sky 的数字人口播成片工作流。只要用户提到 HeyGen、数字人、数字分身、克隆声音、HyperFrames、动效包装、横竖版封面、视频号封面、发布文案或“做成之前那种视频”，就使用本 Skill。它负责把口播文案变成 HeyGen 母版，再用 HyperFrames 做信息化视觉包装，用 image2 生成 Sky 个人 IP 风格封面，并在交付前完成内容、字幕、画面、音频、比例和文件规格质检。即使用户只说“做个数字人视频”，也优先按这套流程执行，除非用户明确要求只生成 HeyGen 母版。
compatibility: Requires an authenticated HeyGen workflow, HyperFrames CLI and skills, image2, ffmpeg/ffprobe, and local media preview. Never put API keys, private URLs, personal paths, or client materials in this skill.
---

# Sky HeyGen + HyperFrames

把中文口播文案变成可发布的 Sky 数字人口播视频：内容检查 → HeyGen 母版 → HyperFrames 包装 → image2 封面 → 发布文案 → 全量质检。

## 何时使用

- 用户说“用 HeyGen 做数字人/数字分身/克隆声音”。
- 用户说“用 HyperFrames 做之前那种视频、加动效、配截图或 B-roll”。
- 用户要求横版/竖版成片、视频号封面、发布标题、正文或标签。
- 用户要求先生成数字人母版：此时只做 HeyGen，停止在母版验收，不调用 HyperFrames、不发布。

## 不变原则

1. 先检查开头 3 秒、观点完整性和结尾收束，再消耗 HeyGen Credits。
2. 每条文案只提交一次 HeyGen 生成；保存真实视频 ID 和 completed 状态。
3. 数字人和 Sky 的个人观点是主叙事，视觉包装不能把内容做成机构宣传片。
4. HyperFrames 负责解释观点和组织节奏，不用特效掩盖口播或剪辑问题。
5. 生成、包装、发布分阶段执行；没有明确确认不对外发布。
6. 不把用户素材、私有链接、Cookie、密钥或本机绝对路径写进 Skill。

## 默认配置

- HeyGen：使用本机已认证的 HeyGen 工作流、已确认的 `sky` digital twin 和 Sky 中文男声。
- 竖屏视频：9:16，默认 1080×1920。
- 横屏视频：16:9，默认 1920×1080。
- 视觉基调：白底/浅灰底，深森林绿、亮蓝、荧光黄绿，轻网格与线路节点。
- 口播优先级高于 BGM；字幕只能来自正确的口播声轨。

## 三套比例必须分开

| 资产 | 展示/视频比例 | 默认尺寸 |
|---|---:|---:|
| 竖屏视频 | 9:16 | 1080×1920 |
| 横屏视频 | 16:9 | 1920×1080 |
| 个人主页卡片封面 | 3:4 | 1080×1440 |
| 分享卡片封面 | 4:3 | 1440×1080 |

封面不能把 9:16/16:9 视频画面直接拉伸或硬裁成所有入口通用图。平台若给出新像素要求，保留入口比例并按平台规格导出。

## 工作流

### 1. 文案和素材检查

确认口播文案、生产模式、视频方向、封面入口、截图/B-roll 和发布要求。文案有弱铺垫、重复或未完成结尾时先修正或标注，不把未经确认的事实写进脚本。

### 2. HeyGen 母版

单次提交 HeyGen，等待真实 `completed` 后保存视频 ID。任务需要完整母版时输出带字幕 MP4、无字幕 MP4 和 SRT，并检查时长、分辨率、帧率、音轨、首尾、字幕遮挡、异常静音和口型。只要用户要求母版，到这里停止并标记待验收。

### 3. HyperFrames 包装

先做时间轴/分镜，再进入 HyperFrames workflow。黄金 3 秒先说完整观点；数字人全屏讲核心内容，需要证据时缩到左下或一侧；截图、流程图、关键词和数据图只解释正在讲的内容；结尾保留完整结论。避免每句话切一次、强卡点、厚重封面、京剧特效和机构化包装。

使用 HyperFrames 时先读取对应的 `hyperframes`、`hyperframes-core`、`hyperframes-animation`、`hyperframes-creative`、`media-use`、`hyperframes-cli` Skill，并按项目 CLI 检查、渲染、预览；不要凭记忆重建命令或把 HTML 截图当最终视频。

### 4. image2 封面

从 HeyGen 母版选自然表情、眼睛睁开、头顶和肩部完整的人物参考，分别生成 3:4 个人主页卡片和 4:3 分享卡片。沿用“左侧大标题、右侧 Sky 半身人物”的版式：白底、轻网格、深绿标签、亮蓝强调词、荧光黄绿高亮条、少量线路节点。不要深色大色块、近距离大脸、无意义小字、乱码、二维码或虚构数据。image2 返回后必须校正到准确尺寸并做图像预览。

### 5. 发布文案

输出一个短而直给的主标题、两到三个备选标题、一版正文和 6–8 个标签。正文按“结果/反常识 → 原因 → 方法或证据 → 行动建议 → 互动问题”组织，不增加视频没有讲过的事实。

## 交付与质检

默认在主题输出目录整理：HeyGen 带字幕/无字幕 MP4、SRT、HyperFrames 成片（如请求）、3:4 和 4:3 封面、发布文案、素材清单、交付质检报告。检查内容完整性、字幕断句、UTF-8/乱码、人物与字幕遮挡、首尾、黑屏、长静音、音轨、分辨率、完整解码和封面入口比例。

封面和包装的细则读取 [references/cover-style.md](references/cover-style.md)；最终检查读取 [references/production-checklist.md](references/production-checklist.md)；评测用例在 [evals/evals.json](evals/evals.json)。
