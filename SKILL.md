---
name: claw-cli-mp4-to-mp3
description: |-
  批量将指定目录下的 .mp4 视频文件提取音频转为 .mp3。
  支持指定源目录和输出目录，未指定输出时默认创建 [源目录]_audio 文件夹。
  自动管理 Python 虚拟环境，保持文件夹层级结构，兼容 python3 和 python。
  高频触发词：mp4转mp3、视频转音频、批量提取音频、mp4 to mp3、extract audio from videos、听视频、提取网课音频、把视频里的声音抠出来、视频转mp3、帮我把 mp4 转 mp3、把视频里的音频提取出来、批量转换视频音频、mp4音频提取。
---

# MP4 to MP3 Extractor

## 技能目标

当用户提到"mp4转mp3"、"批量提取视频音频"、"把 mp4 转为音频"等意图时，本技能自动完成：
1. 扫描源目录（含子文件夹）中的所有 `.mp4` 文件
2. 使用 FFmpeg 提取音频为 `.mp3`（192kbps）
3. 在目标目录重建相同的子文件夹结构
4. 自动处理环境依赖（venv、ffmpeg）

## 执行步骤

### 1. 解析参数

识别用户提供的源目录（必须）和目标目录（可选）。

- 源目录：从用户描述中提取绝对路径，如 `~/Videos`、`F:\命理学`、`./course` 等
- 目标目录：用户未指定时，默认使用 `[源目录]_audio`（与源目录同层级）

### 2. 调用转换脚本

在技能目录下执行转换脚本：

```bash
cd <skill-path>/scripts
python3 extract.py "<源目录>" "[目标目录]"
```

或自动选择 Python：

```bash
python3 scripts/extract.py "<源目录>" "[目标目录]"
```

### 3. 环境与依赖

`extract.py` 会自动处理：
- Python 版本检查（3.10~3.12）
- venv 虚拟环境创建和切换
- FFmpeg 自动检测和下载（如未安装）
- 所需 Python 包（tqdm、pydub、ffmpeg-downloader）

### 4. 日志与进度

- 进度条实时显示处理文件名和当前状态
- 日志写入 `<skill-path>/logs/skill_execution.log`
- 任务结束后汇总成功/失败数量

## 输出结构

```
目标目录/
├── video1.mp3
├── subfolder/
│   ├── video2.mp3
│   └── video3.mp3
```

完全保持源目录的子文件夹层级。

## 错误处理

- 单个文件失败不影响其他文件（try-except 隔离）
- FFmpeg 报错记录到日志并继续
- 未发现 .mp4 文件时优雅退出并提示

## 触发检测

用户提到以下内容时触发本技能：
- "mp4转mp3"、"mp4 转 mp3"、"mp4 to mp3"
- "批量提取音频"、"批量提取视频音频"
- "视频转mp3"、"视频转音频"
- "把视频里的声音抠出来"、"提取网课音频"
- "extract audio from mp4"
- 用户提供了 .mp4 文件所在目录，要求提取音频
