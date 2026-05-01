# MP4 to MP3 Extractor

批量将指定目录下的 .mp4 视频文件提取音频转为 .mp3，支持指定源目录和输出目录，未指定输出时默认创建 `[源目录]_audio` 文件夹。自动管理 Python 虚拟环境，保持文件夹层级结构。

## 核心特性

- **批量转换**：递归扫描源目录（含子文件夹）中的所有 `.mp4` 文件
- **结构保持**：目标目录完美复现源目录的子文件夹层级
- **自启动环境**：首次运行自动创建 venv 虚拟环境，无需手动安装依赖
- **高质量输出**：FFmpeg 提取，192kbps MP3
- **进度可见**：实时进度条 + 日志记录，便于无人值守排查

## 触发方式

当用户提到以下意图时自动调用本技能：

- mp4 转 mp3 / mp4to3 / extract audio from videos
- 批量提取视频音频 / 视频转音频
- 把视频里的声音抠出来 / 提取网课音频
- 先下载视频再提取音频

## 系统要求

- Python 3.10 ~ 3.12
- FFmpeg（技能会自动检测，如未安装则自动下载）

## 使用方法

### 在 Claude Code 中

```
帮我把 ~/Downloads/video 文件夹里的所有 mp4 转成 mp3
```

或者指定输出目录：

```
把 /home/ai-wmr/videos 里的 mp4 批量转音频，输出到 /home/ai-wmr/audio
```

### 命令行手动运行

```bash
cd ~/.claude/skills/claw-cli-mp4-to-mp3/scripts
python3 extract.py "/path/to/source" "/path/to/destination"
```

未指定目标目录时，默认在源目录同层级创建 `[源目录]_audio` 文件夹。

## 输出结构

```
目标目录/
├── video1.mp3
├── subfolder/
│   ├── video2.mp3
│   └── video3.mp3
```

## 日志

详细日志保存在技能目录下的 `logs/skill_execution.log`，滚动保留最近 3 天记录。
