```markdown
# SoraWatermarkCleaner

[English](README.md) | **中文**

> **优雅、纯深度学习驱动的 Sora 视频水印移除工具**

---

<table>
  <tr>
    <td width="50%" align="center">
      <h3>✨ 移除水印后</h3>
      <video src="https://github.com/user-attachments/assets/8cdc075e-7d15-4d04-8fa2-53dd287e5f4c" width="100%" controls autoplay loop muted></video>
    </td>
    <td width="50%" align="center">
      <h3>📹 原始视频</h3>
      <video src="https://github.com/user-attachments/assets/4f032fc7-97da-471b-9a54-9de2a434fa57" width="100%" controls autoplay loop muted></video>
    </td>
  </tr>
</table>

---

## 🌟 核心亮点

| 功能 | 说明 |
|------|------|
| **批量处理** | 一键处理整个文件夹 |
| **支持用户名水印** | 升级 YOLOv11s 模型，可识别动态用户名水印 |
| **公开标注数据集** | [Hugging Face 数据集](https://huggingface.co/datasets/LLinked/sora-watermark-dataset) |
| **一键绿色免装版** | 无需安装，直接运行 |

---

如果这个项目对你有帮助，欢迎[请我喝杯咖啡 ☕](mds/reward.md) 支持持续开发！

---

## 🛠️ 技术原理

`SoraWatermarkCleaner`（简称 `SoraWm`）由两大模块组成：

1. **SoraWaterMarkDetector**  
   - 基于 **YOLOv11s** 训练的水印检测器  
   - 支持静态水印与动态用户名水印

2. **WaterMarkCleaner**  
   - 使用 **LaMa 大模型补全**（Large Mask Inpainting）  
   - 核心代码来自 [IOPaint](https://github.com/Sanster/IOPaint)（鸣谢！）

> **全程深度学习，无需手动遮罩，效果自然**

---

## 🚀 安装指南

### 环境要求
- [FFmpeg](https://ffmpeg.org/)（视频处理必备）

### 推荐使用 `uv` 快速安装

```bash
# 1. 安装依赖
uv sync

# 2. 激活虚拟环境
source .venv/bin/activate
```

> 模型自动下载：
> - `best.pt` → `resources/best.pt`（GitHub Release）
> - `big-lama.pt` → PyTorch 缓存目录（IOPaint 模型源）

---

## 📦 一键绿色免装版（Windows）

**无需 Python，无需安装，开箱即用**

### 下载地址

| 平台 | 链接 |
|------|------|
| **Google Drive** | [立即下载](https://drive.google.com/file/d/1ujH28aHaCXGgB146g6kyfz3Qxd-wHR1c/view?usp=share_link) |
| **百度网盘** | `https://pan.baidu.com/s/1onMom81mvw2c6PFkCuYzdg?pwd=jusu` <br> **提取码**：`jusu` |

**特性：**
- 所有依赖已打包
- 环境预配置
- 支持拖拽上传
- 秒开即用

---

## 🎮 快速开始

### 单视频处理（Python）

```python
from pathlib import Path
from sorawm.core import SoraWM

输入路径 = Path("resources/dog_vs_sam.mp4")
输出路径 = Path("outputs/sora_watermark_removed.mp4")

sora_wm = SoraWM()
sora_wm.run(输入路径, 输出路径)
```

### 交互式 Web 界面

```bash
streamlit run app.py
```

<img src="resources/app.png" width="300" /> &nbsp;&nbsp;&nbsp; <img src="assests/streamlit_batch.png" width="400" />

> 支持 **拖拽上传**、**批量文件夹**、**实时预览**

---

## 📂 批量处理（命令行）

```bash
python cli.py -i 输入目录 -o 输出目录 [-p 文件匹配] [--quiet]
```

### 示例

```bash
# 处理所有 .mp4 文件
python cli.py -i ./input -o ./output

# 只处理 .mov 文件
python cli.py -i ./input -o ./output -p "*.mov"

# 处理多种格式
python cli.py -i ./input -o ./output -p "*.{mp4,mov,avi}"

# 静默模式（无进度条）
python cli.py -i ./input -o ./output --quiet
```

---

## 🌐 Web 服务（FastAPI）

将水印移除器部署为 **在线服务**

```bash
python start_server.py
```

服务地址：`http://localhost:5344`

### API 接口

| 接口 | 功能 |
|------|------|
| `POST /submit_remove_task` | 上传视频 → 返回 `task_id` |
| `GET /get_results?task_id=...` | 查询进度 + 获取下载链接 |
| `GET /download?file=...` | 下载处理后的视频 |

> 完整文档：[http://localhost:5344/docs](http://localhost:5344/docs)

---

## 📊 数据集

我们已开源完整标注数据集：

[https://huggingface.co/datasets/LLinked/sora-watermark-dataset](https://huggingface.co/datasets/LLinked/sora-watermark-dataset)

**可用于：**
- 训练自定义检测器
- 提升模型精度
- 实验新架构

---

## 🔗 在线 API（Replicate）

已打包为 **Cog 模型**，部署在 Replicate：

[replicate.com/uglyrobot/sora2-watermark-remover](https://replicate.com/uglyrobot/sora2-watermark-remover)

> 无需部署，直接调用 HTTP API

---

## © 开源协议

```
Apache License 2.0
```

---

## 📝 引用格式

```bibtex
@misc{sorawatermarkcleaner2025,
  author       = {linkedlist771},
  title        = {SoraWatermarkCleaner：基于深度学习的 Sora 视频水印移除工具},
  year         = {2025},
  publisher    = {GitHub},
  journal      = {GitHub 代码仓库},
  howpublished = {\url{https://github.com/linkedlist771/SoraWatermarkCleaner}}
}
```

---

## ❤️ 致谢

- **[IOPaint](https://github.com/Sanster/IOPaint)** – LaMa 补全引擎
- **[Ultralytics YOLO](https://github.com/ultralytics/ultralytics)** – 检测框架
- 所有贡献者与打赏支持者

---

<p align="center">
  <b>为 AI 生成社区而生 ❤️</b>
</p>

---

> **生成时间**：2025年11月16日 02:20（日本标准时间）  
> **用户**：@hkyutong（日本）  
> **文件**：`README-zh.md` —— 复制即用
```
