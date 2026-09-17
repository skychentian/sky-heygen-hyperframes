# Sky HeyGen + HyperFrames

这是一套把中文口播文案做成数字人口播成片的标准 Skill：

`文案检查 → HeyGen 数字人母版 → HyperFrames 信息化包装 → image2 封面 → 文案标签 → 全量质检`

## 它解决什么问题

- 固定 HeyGen、HyperFrames、image2 三段工作流，避免每次重新讨论。
- 记录 Sky 个人 IP 的白底、深绿、亮蓝、荧光黄绿视觉系统。
- 区分视频的 9:16/16:9 和封面入口的 3:4/4:3。
- 把数字人视频的字幕、音频、黑屏、乱码、布局和首尾完整性纳入交付标准。
- 支持“只生成 HeyGen 母版”和“直接做完整包装成片”两种模式。

## 使用示例

```text
用 HeyGen 做数字人母版，先不要调用 HyperFrames。
```

```text
用之前的风格，把这条 HeyGen 数字人口播做成 HyperFrames 成片，并生成 3:4 个人主页封面和 4:3 分享卡片封面。
```

```text
这条视频要发视频号，按 Sky 的封面风格做两种比例，最后把标题、正文和标签整理出来，但先不要发布。
```

## 关键规格

| 类型 | 比例 | 默认尺寸 |
|---|---:|---:|
| 竖屏视频 | 9:16 | 1080×1920 |
| 横屏视频 | 16:9 | 1920×1080 |
| 个人主页卡片封面 | 3:4 | 1080×1440 |
| 分享卡片封面 | 4:3 | 1440×1080 |

## 隐私边界

Skill 不包含 API Key、Cookie、私有飞书地址、个人本机路径、客户素材或机构内部资料。数字人和声音使用本机已经认证的工作流，但认证信息不写入仓库。


## 安装

将本仓库下载或克隆到所用 Agent 的 Skills 目录，目录名使用 `sky-heygen-hyperframes`。

Codex 示例（目标目录不存在时执行）：

```bash
git clone https://github.com/skychentian/sky-heygen-hyperframes.git ~/.codex/skills/sky-heygen-hyperframes
```

Claude Code 可放在 `~/.claude/skills/sky-heygen-hyperframes`。安装后重新开启会话，并明确调用 `$sky-heygen-hyperframes`。

也可从 GitHub Release 下载 ZIP，解压后把其中的 `sky-heygen-hyperframes` 目录放进 Skills 目录。已有同名安装时先比较内容，避免覆盖本地修改。

## 运行依赖

这是工作流 Skill，依赖需要在使用环境中另行配置：

- 已认证的 HeyGen 工作流，以及获授权使用的数字人与声音；Sky 的数字人和声音不随包分发，其他使用者需配置自己的身份。
- HyperFrames CLI，以及 `hyperframes`、`hyperframes-core`、`hyperframes-animation`、`hyperframes-creative`、`media-use`、`hyperframes-cli` Skills。
- image2 生图能力，以及 ffmpeg / ffprobe 和媒体预览工具。

本包不含上述第三方工具、认证配置、人物素材或成片工程。`reports/validation-summary.md` 是原 Skill 的历史校验记录，不代表新环境已通过视频生成测试。
