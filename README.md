这是一份专为 **ComfyUI 一键部署项目** 设计的 GitHub `README.md` 模板。它包含了徽章、核心特性、多平台（本地、Docker、云端 GPU）一键部署指南、预置插件/模型清单以及常见问题排查，你可以直接复制并根据你的实际仓库名称和脚本路径进行微调。

```markdown
<div align="center">

# 🚀 ComfyUI One-Click Deploy (一键部署工具包)

**零门槛、全自动、开箱即用的 ComfyUI 极速部署方案**  
内置主流节点插件 | 自动配置 Python 环境 | 支持本地 / Docker / 云端算力平台

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10%2B-green.svg)](https://www.python.org/)
[![PyTorch 2.1+](https://img.shields.io/badge/PyTorch-2.1%2B-orange.svg)](https://pytorch.org/)
[![CUDA 12.1+](https://img.shields.io/badge/CUDA-12.1%2B-brightgreen.svg)](https://developer.nvidia.com/cuda-toolkit)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

[功能特性](#-核心特性) • [环境要求](#-环境要求) • [一键部署](#-快速开始一键部署) • [预置插件](#-预置插件与模型说明) • [常见问题](#-常见问题-faq)

</div>

---

## ✨ 核心特性

* ⚡ **真正的一键部署**：告别繁琐的依赖报错，自动完成虚拟环境创建、PyTorch 匹配与依赖安装。
* 🧩 **开箱即用的插件生态**：默认集成 `ComfyUI-Manager`、汉化插件、图像增强及视频生成等高频自定义节点。
* 🌐 **国内网络加速优化**：自动配置 GitHub 镜像源、HuggingFace 镜像 (`hf-mirror`) 与 Pip 清华/阿里源，大幅提升下载速度。
* 🐳 **多平台无缝支持**：支持 Windows 本地批处理、Linux Shell 脚本、Docker 容器化部署，以及 AutoDL / 阿里云 PAI / RunPod 等云算力平台。
* 💾 **模型软链接支持**：支持与 Stable Diffusion WebUI (A1111 / Forge) 共享模型目录，节省宝贵硬盘空间。

---

## 💻 环境要求

| 硬件/系统 | 最低配置 | 推荐配置 |
| :--- | :--- | :--- |
| **操作系统** | Windows 10/11, Ubuntu 20.04+, macOS (M系列) | Windows 11 / Ubuntu 22.04 LTS |
| **显卡 (GPU)** | NVIDIA GTX 1660 (6GB 显存) | NVIDIA RTX 3060 (12GB) / RTX 4090 (24GB) |
| **内存 (RAM)** | 16 GB | 32 GB 及以上 |
| **硬盘空间** | 40 GB 可用空间 (SSD) | 200 GB+ NVMe SSD |

---

## 🚀 快速开始（一键部署）

请根据你的使用场景选择对应的部署方式（部署前请将仓库地址 `your-username/comfyui-one-click` 替换为实际项目地址）：

### 方式一：Windows 本地一键部署

1. 确保已安装 [Git](https://git-scm.com/)。
2. 打开终端（PowerShell 或 CMD），执行以下命令克隆本项目并运行安装脚本：

```powershell
git clone [https://github.com/your-username/comfyui-one-click.git](https://github.com/your-username/comfyui-one-click.git)
cd comfyui-one-click
.\install_windows.bat

```

3. 安装完成后，双击运行根目录下的 **`run_gpu.bat`** 即可自动在浏览器打开 `http://127.0.0.1:8188`。

---

### 方式二：Linux / 云算力平台（AutoDL / 恒源云等）一键脚本

直接复制以下单行命令到终端执行（已针对国内网络环境自动开启镜像加速）：

```bash
curl -fsSL [https://raw.githubusercontent.com/your-username/comfyui-one-click/main/deploy_linux.sh](https://raw.githubusercontent.com/your-username/comfyui-one-click/main/deploy_linux.sh) | bash

```

**常用启动命令：**

```bash
# 默认启动（监听本地 8188 端口）
bash start.sh

# 云端/局域网开放访问（监听 0.0.0.0 并开启端口 6006，适配 AutoDL 自定义服务）
bash start.sh --listen 0.0.0.0 --port 6006

```

---

### 方式三：Docker 容器化一键部署（推荐生产环境）

确保已安装 [Docker](https://www.docker.com/) 和 [NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html)。

```bash
git clone [https://github.com/your-username/comfyui-one-click.git](https://github.com/your-username/comfyui-one-click.git)
cd comfyui-one-click
docker compose up -d

```

服务启动后，访问 `http://localhost:8188` 即可使用。所有模型与输出图片均已挂载至宿主机的 `./models` 和 `./output` 目录。

---

### 方式四：云端 Notebook 快速启动

无需本地显卡，点击下方徽章即可在云端免费/按需算力平台一键拉起环境：

| 平台 | 启动入口 | 说明 |
| --- | --- | --- |
| **Google Colab** | [](https://www.google.com/search?q=https://colab.research.google.com/github/your-username/comfyui-one-click/blob/main/notebooks/ComfyUI_Colab.ipynb) | 免费 T4 显卡体验，支持 Google Drive 挂载 |
| **Kaggle** | [](https://www.google.com/search?q=https://kaggle.com/kernels/welcome%3Fsrc%3Dhttps://github.com/your-username/comfyui-one-click/blob/main/notebooks/ComfyUI_Kaggle.ipynb) | 每周 30 小时免费双卡 T4 / P100 算力 |

---

## 📦 预置插件与模型说明

### 1. 默认内置节点 (Custom Nodes)

本整合包在部署时会自动拉取并配置以下核心插件：

* **[ComfyUI-Manager](https://github.com/ltdrdata/ComfyUI-Manager)**：插件与缺失节点一键管理器。
* **[AIGODLIKE-ComfyUI-Translation](https://github.com/AIGODLIKE/AIGODLIKE-ComfyUI-Translation)**：多语言全界面汉化插件。
* **[ComfyUI-Custom-Scripts](https://github.com/pythongosssss/ComfyUI-Custom-Scripts)**：工作流辅助增强（自动补全、对齐、画布缩放等）。
* **[ComfyUI-Impact-Pack](https://github.com/ltdrdata/ComfyUI-Impact-Pack)**：面部修复、局部重绘与节点细化工具包。
* **[ComfyUI-VideoHelperSuite](https://github.com/Kosinkadink/ComfyUI-VideoHelperSuite)**：视频合成、帧处理与动图导出核心节点。

### 2. 目录结构说明

```text
comfyui-one-click/
├── ComfyUI/                  # ComfyUI 核心主目录
│   ├── custom_nodes/         # 自定义节点插件目录
│   ├── models/               # 模型存放根目录
│   │   ├── checkpoints/      # 大模型 (SD1.5 / SDXL / Flux 等)
│   │   ├── clip/             # CLIP / T5 文本编码器
│   │   ├── controlnet/       # ControlNet 模型
│   │   ├── loras/            # LoRA 微调模型
│   │   └── vae/              # VAE 模型
│   ├── input/                # 输入图像/视频目录
│   └── output/               # 生成结果输出目录
├── scripts/                  # 自动化环境检测、模型下载与更新脚本
├── docker-compose.yml        # Docker 编排文件
├── extra_model_paths.yaml    # 外部模型路径共享配置文件
└── start.sh / run_gpu.bat    # 一键启动入口

```

---

## ⚙️ 进阶配置

### 与 WebUI 共享模型目录

如果你电脑上已经安装了 Stable Diffusion WebUI，无需重复下载模型：

1. 打开根目录下的 `extra_model_paths.yaml`。
2. 将 `base_path:` 修改为你的 `stable-diffusion-webui` 绝对路径。
3. 重启 ComfyUI 即可自动识别所有已有模型。

### 一键下载常用基础模型

运行内置的模型下载向导，按提示输入数字即可通过高速镜像自动下载对应模型到正确目录：

```bash
python scripts/download_models.py

```

---

## ❓ 常见问题 (FAQ)

这通常是因为驱动版本过低或安装了 CPU 版本的 PyTorch。

1. 请确保你的 NVIDIA 显卡驱动版本 >= 535.xx。
2. 运行项目自带的修复脚本重新安装对应 CUDA 版本的 PyTorch：
```bash
bash scripts/fix_torch.sh

```



1. 点击右侧菜单栏的 **Manager (管理器)**。
2. 点击 **Install Missing Custom Nodes (安装缺失节点)**。
3. 全选列表中的插件并点击安装，完成后点击 **Restart (重启)** 并刷新浏览器页面。

你可以在启动脚本中添加以下启动参数来降低显存占用：

* `--lowvram`：适用于显存小于 6GB 的显卡（拆分模型加载，速度略降但防爆显存）。
* `--medvram`：适用于 6GB - 8GB 显存显卡。
* `--fp8_e4m3fn-unet`：在使用大型模型（如 Flux）时开启 FP8 量化推理。

---

## 🤝 贡献与支持

欢迎提交 Issue 或 Pull Request 来帮助完善这个一键部署项目！

* 如果这个项目帮到了你，请点亮右上角的 ⭐ **Star** 支持一下！

## 📄 开源协议

本项目基于 [GPL-3.0 License](https://www.google.com/search?q=LICENSE) 开源。底层核心基于 [ComfyUI](https://github.com/comfyanonymous/ComfyUI) 构建。

```

### 💡 使用微调建议：
1. **替换占位符**：将文中的 `your-username/comfyui-one-click` 批量替换为你自己的 GitHub 用户名和仓库名。
2. **定制插件列表**：如果你的一键包主打特定方向（例如专攻视频工作流或人像工作流），可以在“默认内置节点”部分把对应的核心节点列出来，吸引精准用户。
3. **配合真实脚本**：如果你还没有写好配套的 `deploy_linux.sh` 或 `install_windows.bat` 一键部署脚本，随时告诉我你的目标平台（比如是针对 AutoDL 还是 Windows 本地便携包），我可以直接帮你把对应的部署脚本也写出来。

<ElicitationsGroup message="如果你需要配套的部署代码或进一步定制，可以选择：">
  <Elicitation label="编写配套的 Linux / AutoDL 一键部署 Shell 脚本" query="帮我编写与这个 README 配套的 deploy_linux.sh 一键部署脚本，包含自动创建虚拟环境、国内镜像加速、拉取 ComfyUI 及常用插件。"/>
  <Elicitation label="编写配套的 Docker Compose 与 Dockerfile" query="帮我编写用于一键部署 ComfyUI 的 Dockerfile 和 docker-compose.yml 配置文件，支持 GPU 调用和模型目录挂载。"/>
  <Elicitation label="生成双语（中英对照）版本的 README" query="帮我将这份 ComfyUI 一键部署的 README 改写为中英双语版本，方便海外开发者阅读。"/>
</ElicitationsGroup>

```
