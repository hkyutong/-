# Sora Watermark Cleaner (SoraWm)

**⚡️ 一键移除 OpenAI Sora 生成视频中的官方水印（含用户名）**  
**⚡️ One-click removal of official watermarks (including username) from OpenAI Sora videos**

<p align="center">
  <a href="#english">English</a> • 
  <a href="#中文版">中文版</a>
</p>

![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python&logoColor=white)
![License](https://img.shields.io/github/license/linkedlist771/SoraWatermarkCleaner)
![Stars](https://img.shields.io/github/stars/linkedlist771/SoraWatermarkCleaner?style=social)
![Forks](https://img.shields.io/github/forks/linkedlist771/SoraWatermarkCleaner?style=social)

> Pure deep-learning solution | YOLOv11s precise detection + LaMA seamless inpainting | Batch processing | EXE / Web / API deployment  
> 纯深度学习驱动 | YOLOv11s 精准检测 + LaMA 无痕修复 | 支持批量处理 | 提供 EXE / Web / API 多部署方式

---

## ✨ Features / 核心特性

| Module / 功能模块      | Technology / 技术细节                           | Advantage / 特点优势                  |
|------------------------|------------------------------------------------|---------------------------------------|
| Watermark Detector     | YOLOv11s (fine-tuned for latest username watermarks) | Extremely accurate, near-zero misses |
| 水印检测器             | YOLOv11s（已针对最新含用户名水印微调）          | 定位极准，漏检率接近 0                |
| Watermark Remover      | LaMA inpainting (based on IOPaint)             | Intelligent filling, seamless result |
| 水印清除器             | LaMA 大模型修复（基于 IOPaint）                 | 智能填充，自然无痕                    |
| Batch Processing       | Native folder/multi-file support               | Process hundreds of videos at once   |
| 批量处理               | 原生支持文件夹/多文件拖拽                       | 一键处理数百个视频                    |
| Deployment Options     | EXE / Streamlit / FastAPI                      | One-click EXE or deploy as service   |
| 多端部署               | EXE / Streamlit / FastAPI                      | 无需环境一键运行或部署为在线服务      |

---

## 🎬 Before & After / 效果对比

<p align="center">
  <table>
    <tr>
      <td align="center"><b>Original (with watermark)<br>原始视频（带水印）</b></td>
      <td align="center"><b>Cleaned (seamless)<br>移除后（无痕）</b></td>
    </tr>
    <tr>
      <td>
        <a href="https://github.com/user-attachments/assets/4f032fc7-97da-471b-9a54-9de2a434fa57">
          <img src="https://github.com/user-attachments/assets/4f032fc7-97da-471b-9a54-9de2a434fa57" width="100%" alt="Original Video">
        </a>
      </td>
      <td>
        <a href="https://github.com/user-attachments/assets/8cdc075e-7d15-4d04-8fa2-53dd287e5f4c">
          <img src="https://github.com/user-attachments/assets/8cdc075e-7d15-4d04-8fa2-53dd287e5f4c" width="100%" alt="Cleaned Video">
        </a>
      </td>
    </tr>
    <tr>
      <td align="center"><small>点击播放原始视频 🔗</small></td>
      <td align="center"><small>点击播放处理后视频 🎯</small></td>
    </tr>
  </table>
</p>

> **GitHub 自动将 `.mp4` 附件渲染为可播放视频**，点击缩略图即可播放！

---

## 🚀 Quick Start / 快速开始

### 1. One-Click Portable Version (Windows Recommended)  
1. 一键便携版（Windows 推荐）

无需 Python，下载解压即用。

| Platform / 平台     | Download Link / 下载链接                                                                 | Password / 提取码 | Notes / 备注             |
|---------------------|------------------------------------------------------------------------------------------|-------------------|--------------------------|
| Google Drive        | [Click to download](https://drive.google.com/file/d/...)（请替换真实链接）               | -                 | 国际用户推荐             |
| 百度网盘            | https://pan.baidu.com/s/1onMom81mvw2c6PFkCuYzdg?pwd=jusujusu                            | jusu              | 中国大陆加速             |

### 2. Python Environment Installation  
2. Python 环境安装（开发者 / Linux / Mac）

```bash
# 1. 安装 FFmpeg（必需）
# Windows: https://www.gyan.dev/ffmpeg/builds/
# macOS: brew install ffmpeg
# Linux: sudo apt install ffmpeg -y

# 2. 克隆并安装依赖（推荐 uv，超快）
git clone https://github.com/linkedlist771/SoraWatermarkCleaner.git
cd SoraWatermarkCleaner
uv sync    # 自动创建 .venv 并安装所有依赖
