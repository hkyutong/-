SoraWatermarkCleanerEnglish | 中文 本项目提供了一种优雅的方式来移除 Sora2 生成视频中的 Sora 水印。 <table>  <tr>    <td width="50%">      <h3 align="center">水印已移除</h3>      <video src="https://github.com/user-attachments/assets/8cdc075e-7d15-4d04-8fa2-53dd287e5f4c" width="100%"></video>    </td>    <td width="50%">      <h3 align="center">原始视频</h3>      <video src="https://github.com/user-attachments/assets/4f032fc7-97da-471b-9a54-9de2a434fa57" width="100%"></video>    </td>  </tr></table>⭐️: 我们现在支持批量处理。针对带用户名的新的水印，Yolo 权重已更新，请尝试使用新版本的水印检测模型，效果会更好。我们已将标注数据集上传至 Huggingface，请查看此数据集。欢迎训练您自己的自定义检测器模型或改进我们的模型！一键便携式构建版本可用 — 在此下载，适用于 Windows 用户！无需安装。💝 如果您觉得本项目有帮助，请考虑给我买杯咖啡来支持开发！1. 方法SoraWatermarkCleaner（我们后续称其为 SoraWm）由两个部分组成：SoraWaterMarkDetector（Sora 水印检测器）：我们训练了一个 yolov11s 版本来检测 Sora 水印。（感谢 yolo！）WaterMarkCleaner（水印清除器）：我们参考了 iopaint 使用 lama 模型进行水印去除的实现。  (此代码库来自 https://github.com/Sanster/IOPaint#，感谢他们出色的工作！)我们的 SoraWm 纯粹由深度学习驱动，并在许多生成的视频中取得了不错的效果。2. 安装视频处理需要 FFmpeg，请首先安装它。我们强烈建议使用 uv 来安装环境：安装：uv sync
现在环境将安装在 .venv 目录下，您可以使用以下命令激活环境：source .venv/bin/activate
下载预训练模型：训练好的 yolo 权重将存储在 resources 目录中作为 best.pt，它将自动从 https://github.com/linkedlist771/SoraWatermarkCleaner/releases/download/V0.0.1/best.pt 下载。Lama 模型将从 https://github.com/Sanster/models/releases/download/add_big_lama/big-lama.pt 下载，并存储在 torch 缓存目录中。这两个下载都是自动的，如果失败，请检查您的网络连接状态。批量处理使用 cli.py 进行批量处理python cli.py [-h] -i INPUT -o OUTPUT [-p PATTERN] [--quiet]
示例：# 处理输入文件夹中的所有 .mp4 文件
python batch_process.py -i /path/to/input -o /path/to/output
# 处理所有 .mov 文件
python batch_process.py -i /path/to/input -o /path/to/output --pattern "*.mov"
# 处理所有视频文件 (mp4, mov, avi)
python batch_process.py -i /path/to/input -o /path/to/output --pattern "*.{mp4,mov,avi}"
# 不在 sorawm 处理过程中显示 Tqdm 进度条。
python batch_process.py -i /path/to/input -o /path/to/output --quiet
3. 一键便携式版本对于喜欢即开即用解决方案，无需手动安装的用户，我们提供了一个包含所有预配置依赖项的 一键便携式分发包。下载链接Google Drive:从 Google Drive 下载百度网盘 (Baidu Pan) - 适用于中国用户：链接: https://pan.baidu.com/s/1onMom81mvw2c6PFkCuYzdg?pwd=jusu提取码: jusu特点✅ 无需安装✅ 包含所有依赖项✅ 预配置环境✅ 开箱即用只需下载、解压并运行！4. 演示要进行基本使用，请尝试运行 example.py：
from pathlib import Path
from sorawm.core import SoraWM


if __name__ == "__main__":
    input_video_path = Path(
        "resources/dog_vs_sam.mp4"
    )
    output_video_path = Path("outputs/sora_watermark_removed.mp4")
    sora_wm = SoraWM()
    sora_wm.run(input_video_path, output_video_path)

我们还为您提供了一个基于 streamlit 的交互式网页，请尝试使用以下命令运行它：streamlit run app.py
<img src="resources/app.png" style="zoom: 25%;" />现在也支持批量处理，您可以拖动一个文件夹或选择多个文件进行处理。<img src="assests/streamlit_batch.png" style="zoom: 50%;" />5. Web 服务器在这里，我们提供了一个 基于 FastAPI 的 Web 服务器，可以快速将此水印去除工具转换为一个服务。只需运行：python start_server.py
Web 服务器将启动在端口 5344 上。您可以查看 FastAPI 文档以获取更多详情。有三个可用路由：submit_remove_task (提交移除任务)   > 上传视频后，将返回一个任务 ID，并且视频将立即开始处理。<img src="resources/53abf3fd-11a9-4dd7-a348-34920775f8ad.png" alt="image" style="zoom: 25%;" />get_results (获取结果)您可以使用上面获得的任务 ID 来检查任务状态。它将显示视频处理完成的百分比。完成后，返回的数据将包含一个 下载 URL。download (下载)您可以使用步骤 2 中的 下载 URL 来检索清理后的视频。6. 数据集我们已将标注数据集上传至 Huggingface，请查看此链接 https://huggingface.co/datasets/LLinked/sora-watermark-dataset。欢迎训练您自己的自定义检测器模型或改进我们的模型！7. API已打包为 Cog 并发布到 Replicate 以供简单的基于 API 的使用。8. 许可证 Apache 许可证9. 引用如果您使用了本项目，请引用：@misc{sorawatermarkcleaner2025,
  author = {linkedlist771},
  title = {SoraWatermarkCleaner},
  year = {2025},
  url = {[https://github.com/linkedlist771/SoraWatermarkCleaner](https://github.com/linkedlist771/SoraWatermarkCleaner)}
}
10. 致谢IOPaint 提供的 LAMA 实现Ultralytics YOLO 提供的目标检测
