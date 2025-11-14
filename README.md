SoraWatermarkCleanerEnglish | 中文 本项目提供了一种优雅的方式来移除 Sora2 生成视频中的 Sora 水印。 <table>  <tr>    <td width="50%">      <h3 align="center">水印已移除</h3>      <video src="https://github.com/user-attachments/assets/8cdc075e-7d15-4d04-8fa2-53dd287e5f4c" width="100%"></video>    </td>    <td width="50%">      <h3 align="center">原始视频</h3>      <video src="https://github.com/user-attachments/assets/4f032fc7-97da-471b-9a54-9de2a434fa57" width="100%"></video>    </td>  </tr></table>⭐️: 批量处理已支持。针对包含用户名的最新水印，我们已更新 Yolo 权重，建议使用新版水印检测模型以获得更优效果。已将标注数据集上传至 Hugging Face，请查阅此数据集。欢迎训练您的自定义检测器或改进现有模型！一键便携式构建版本已就绪 — Windows 用户在此下载！无需任何安装步骤。💝 如果您认为本项目有价值，请考虑给我买杯咖啡来支持持续开发！1. 方法原理SoraWatermarkCleaner（简称 SoraWm）由以下两个核心模块构成：SoraWaterMarkDetector（Sora 水印检测器）：我们训练了一个 yolov11s 模型来精确检测 Sora 水印。（感谢 YOLO 的强大能力！）WaterMarkCleaner（水印清除器）：我们借鉴了 iopaint 使用 LAMA 模型进行水印去除的实现。    (该代码库源自 https://github.com/Sanster/IOPaint#，感谢他们出色的工作！)我们的 SoraWm 完全基于深度学习驱动，在处理许多生成的视频时表现优异。2. 安装指南本项目需要 FFmpeg 进行视频处理，请务必首先安装。我们强烈推荐使用 uv 来安装依赖环境：安装依赖：uv sync
环境将安装在 .venv 目录下。您可以使用以下命令激活环境：source .venv/bin/activate
下载预训练模型：训练好的 Yolo 权重 (best.pt) 将自动从 https://github.com/linkedlist771/SoraWatermarkCleaner/releases/download/V0.0.1/best.pt 下载，并存储在 resources 目录中。Lama 模型则从 https://github.com/Sanster/models/releases/download/add_big_lama/big-lama.pt 下载，存储于 Torch 缓存目录。所有模型下载均为自动，如遇失败，请检查网络连接。批量处理：    使用 cli.py 进行批量视频处理。python cli.py [-h] -i INPUT -o OUTPUT [-p PATTERN] [--quiet]
示例：# 处理输入文件夹中的所有 .mp4 文件
python batch_process.py -i /path/to/input -o /path/to/output
# 处理所有 .mov 文件
python batch_process.py -i /path/to/input -o /path/to/output --pattern "*.mov"
# 处理所有视频文件 (mp4, mov, avi)
python batch_process.py -i /path/to/input -o /path/to/output --pattern "*.{mp4,mov,avi}"
# 在 SoraWm 处理过程中不显示 Tqdm 进度条
python batch_process.py -i /path/to/input -o /path/to/output --quiet
3. 一键便携式版本为了方便不愿手动安装的用户，我们提供了一个预配置了所有依赖项的 一键便携式分发包。下载链接Google Drive:从 Google Drive 下载百度网盘 (Baidu Pan) - 适用于中国用户：链接: https://pan.baidu.com/s/1onMom81mvw2c6PFkCuYzdg?pwd=jusu提取码: jusu特点✅ 无需安装✅ 包含所有依赖✅ 预配置环境✅ 开箱即用只需下载、解压即可运行！4. 演示示例要进行基础功能测试，请尝试运行 example.py：
from pathlib import Path
from sorawm.core import SoraWM


if __name__ == "__main__":
    input_video_path = Path(
        "resources/dog_vs_sam.mp4"
    )
    output_video_path = Path("outputs/sora_watermark_removed.mp4")
    sora_wm = SoraWM()
    sora_wm.run(input_video_path, output_video_path)


我们同时提供了一个基于 streamlit 的交互式网页应用，您可以使用以下命令启动它：streamlit run app.py
<img src="resources/app.png" style="zoom: 25%;" />现在也支持批量处理功能，您可以拖入一个文件夹或选择多个文件进行处理。<img src="assests/streamlit_batch.png" style="zoom: 50%;" />5. Web 服务器我们提供了一个 基于 FastAPI 的 Web 服务器，可以将水印去除功能快速部署为一项服务。运行以下命令即可启动：python start_server.py
Web 服务器将启动在 5344 端口。您可以查看 FastAPI 文档以获取接口详情。提供以下三个路由：submit_remove_task (提交移除任务)   > 上传视频后，系统将返回一个任务 ID，并立即开始处理视频。<img src="resources/53abf3fd-11a9-4dd7-a348-34920775f8ad.png" alt="image" style="zoom: 25%;" />get_results (获取结果)您可以使用上一步获取的任务 ID 来检查处理状态。它将显示视频处理完成的百分比。完成后，返回数据中将包含一个 下载 URL。download (下载)您可以使用步骤 2 中的 下载 URL 来下载已清理水印的视频。6. 数据集我们已将标注数据集上传至 Hugging Face，请查阅此链接 https://huggingface.co/datasets/LLinked/sora-watermark-dataset。欢迎自由训练您的自定义检测器模型或对我们的模型进行改进！7. API 接口本项目已打包为 Cog 并发布到 Replicate，支持简便的 API 调用。8. 许可证Apache 许可证9. 引用如果您在工作中使用本项目，请引用：@misc{sorawatermarkcleaner2025,
  author = {linkedlist771},
  title = {SoraWatermarkCleaner},
  year = {2025},
  url = {[https://github.com/linkedlist771/SoraWatermarkCleaner](https://github.com/linkedlist771/SoraWatermarkCleaner)}
}
10. 致谢IOPaint 提供的 LAMA 实现Ultralytics YOLO 提供的目标检测
