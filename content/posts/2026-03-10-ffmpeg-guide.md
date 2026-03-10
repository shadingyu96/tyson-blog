---
title: FFmpeg 入门到实战：一篇就够了
date: 2026-03-10
summary: 从零掌握 FFmpeg 常用命令，搭配 5 个实战案例，小白也能快速上手视频处理。
---

很多人第一次听到 FFmpeg 时，都会觉得这是个"高大上"的命令行工具。其实它没那么神秘，今天这篇帮你快速上手。

## 什么是 FFmpeg？

FFmpeg 是一套**免费开源的多媒体框架**，可以处理音频、视频、字幕几乎所有格式。不管是转换格式、裁剪画面、提取音频、还是加字幕，它都能搞定。

核心组件：
- `ffmpeg`：视频编解码核心
- `ffplay`：播放器
- `ffprobe`：多媒体分析工具

## 安装

### macOS
```bash
brew install ffmpeg
```

### Linux
```bash
sudo apt install ffmpeg    # Debian/Ubuntu
sudo yum install ffmpeg    # CentOS
```

### Windows
直接去 [ffmpeg.org](https://ffmpeg.org/download.html) 下载，或用 winget：
```bash
winget install ffmpeg
```

安装后验证：
```bash
ffmpeg -version
```

## 5 个实战案例

### 1. 视频格式转换
最常用的场景，把 MOV 转 MP4：
```bash
ffmpeg -i input.mov output.mp4
```

### 2. 压缩视频大小
在不影响画质的前提下大幅缩小体积：
```bash
ffmpeg -i input.mp4 -vcodec libx264 -crf 23 -acodec aac -b:a 128k output.mp4
```
说明：
- `-crf 23`：质量参数，数值越大文件越小（18-28 推荐）
- `-b:a 128k`：音频码率

### 3. 裁剪视频画面
只保留画面中间区域（去除水印常用）：
```bash
ffmpeg -i input.mp4 -vf "crop=宽度:高度:X坐标:Y坐标" output.mp4
```
例子：裁剪中间 1280x720 区域：
```bash
ffmpeg -i input.mp4 -vf "crop=1280:720:0:0" output.mp4
```

### 4. 提取音频
把视频里的声音保存为 MP3：
```bash
ffmpeg -i input.mp4 -vn -acodec libmp3lame -q:a 2 output.mp3
```

### 5. 批量处理
用脚本一次性处理文件夹里所有视频：
```bash
for file in *.mp4; do
    ffmpeg -i "$file" -vcodec libx264 -crf 23 "${file%.mp4}_new.mp4"
done
```

## 常用参数速查

| 参数 | 作用 |
|---|---|
| `-i` | 输入文件 |
| `-o` | 输出文件 |
| `-c:v` | 视频编码 |
| `-c:a` | 音频编码 |
| `-ss` | 开始时间 |
| `-t` | 持续时间 |
| `-r` | 帧率 |
| `-s` | 分辨率 |

## 进阶技巧

### 合并多个视频
```bash
# 先建一个文件列表
echo "file '1.mp4'" > list.txt
echo "file '2.mp4'" >> list.txt
# 合并
ffmpeg -f concat -safe 0 -i list.txt -c copy output.mp4
```

### 截取 GIF 动图
```bash
ffmpeg -ss 5 -t 3 -i input.mp4 -vf "fps=10,scale=480:-1" output.gif
```

### 添加水印
```bash
ffmpeg -i input.mp4 -i watermark.png -filter_complex "overlay=10:10" output.mp4
```

## 常见问题

**Q: 转换后画质变差？**
A: 试试 `-crf 18` 或直接用 `-c copy` 不重新编码（最快）。

**Q: 命令执行很慢？**
A: 加 `-threads 4` 指定多线程，或者用 GPU 加速（需要硬件支持）。

**Q: 中文文件名乱码？**
A: 试试加 `-encodings` 或用英文文件名。

## 总结

FFmpeg 学起来并不难，掌握这几个核心命令就能解决 80% 的日常需求。关键是多动手实践——先挑一个简单场景练起来，慢慢就熟练了。

如果你有特定的使用场景（比如直播推流、批量加水印），欢迎留言，我可以针对性的再写一篇。
