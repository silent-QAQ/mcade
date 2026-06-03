# MCADE

<p align="center">
  <img src="icons/mcade-logo.png" width="128" height="128" alt="MCADE Logo">
</p>

<h3 align="center">Minecraft Community AI Development Environment</h3>
<p align="center">面向 Minecraft 社区开发者的 AI 集成开发环境 —— 基于 VSCodium 深度定制</p>

<p align="center">
  <strong>开箱即用 · AI 驱动 · 专注 Minecraft 开发</strong>
</p>

---

## 目录

- [项目简介](#项目简介)
- [核心特性](#核心特性)
- [目标用户](#目标用户)
- [项目架构](#项目架构)
- [项目结构](#项目结构)
- [构建指南](#构建指南)
  - [环境要求](#环境要求)
  - [本地构建](#本地构建)
  - [GitHub Actions 云端构建](#github-actions-云端构建)
  - [环境变量说明](#环境变量说明)
- [品牌定制指南](#品牌定制指南)
- [开发路线图](#开发路线图)
- [参与贡献](#参与贡献)
- [许可证](#许可证)
- [致谢](#致谢)

---

## 项目简介

**MCADE**（Minecraft AI Development Environment）是一款面向 Minecraft 社区开发者的 AI 集成开发环境。基于 VSCodium 深度定制，内置 AI 编程助手、Mod/插件开发工具链、服务器管理工具和本地测试启动器，致力于打造「开箱即用」的 Minecraft 开发体验。

> **核心理念：** VSCodium 提供成熟的 IDE 底座，自研 **Hermes** 提供 AI 能力，自研扩展集合提供 MC 开发工具链，开源启动器提供本地测试能力。

### 与竞品的差异

| 对比项 | MCADE | MCreator | IntelliJ + MinecraftDev | VS Code 自行配置 |
|--------|-------|----------|------------------------|-----------------|
| 定位 | 专业开发者 IDE | 可视化编程工具 | 通用 Java IDE | 通用编辑器 |
| AI 集成 | 深度内置 | 无 | 需额外配置 | 需手动安装 |
| MC 工具链 | 开箱即用 | 内置 | 需安装插件 | 需手动配置 |
| 服务器管理 | 内置面板 | 无 | 无 | 需手动 |
| 本地测试 | 内置启动器 | 内置 | 无 | 需手动 |
| 扩展兼容 | 兼容 VS Code 生态 | 封闭生态 | 兼容 IntelliJ 生态 | 兼容 VS Code 生态 |
| 许可证 | MIT 开源 | 专有软件 | 商业授权 | MIT 开源 |

---

## 核心特性

### AI 助手 — Hermes
- **Hermes 自定义面板：** 比通用 ACP Client 更优的 UI 体验，专为 Minecraft 开发者设计的 AI 交互界面
- **Skill 市场：** 用户之间分享/下载 AI Skills，实现"收集 → 审核 → 分发"的进化闭环
- **云端 Skill 同步：** 用户 Skill 可同步至云端，审核后分发给更多开发者
- **项目上下文感知：** 自动读取当前项目的结构、依赖和配置，提供精准的 AI 辅助
- 支持对接 DeepSeek API / Ollama 本地模型等后端

### Mod/插件开发工具
- **项目脚手架：** 一键创建 Forge / Fabric / NeoForge / Paper 项目
- **代码片段库：** 涵盖 Forge、Fabric、Paper、Bukkit 等平台的常用代码片段
- **Gradle 深度集成：** 可视化 Task 管理，一键 Build → 输出 JAR
- **资源文件编辑器：** JSON 可视化编辑（Recipe、Loot Table、Advancement 等）
- **调试器配置：** 一键配置 Java Debug + Minecraft 专用调试

### 服务器管理
- 侧边栏服务器管理面板
- 创建/启停/重启本地 Minecraft 服务器
- 支持 Vanilla / Forge / Fabric / Paper / Spigot 等服务端
- 实时控制台（WebSocket 连接 stdin/stdout）
- 服务器配置在线编辑
- 自动备份

### 本地 MC 启动器
- 集成 Prism Launcher CLI，一键启动测试实例
- 快速启动、自动连接调试器
- 长期目标：自研轻量测试启动器

---

## 目标用户

- **Minecraft Java Edition Mod 开发者**（Forge / Fabric / NeoForge / Quilt）
- **Minecraft 服务器插件开发者**（Paper / Spigot / Bukkit / BungeeCord / Velocity）
- **Bedrock Edition Addon 开发者**（行为包 / 资源包 / 脚本）
- **数据包（Datapack）开发者**
- **服务器运维人员**

---

## 项目架构

```
┌──────────────────────────────────────────────────┐
│                    MCADE IDE                       │
│  ┌──────────────────────────────────────────────┐ │
│  │         VSCodium Core (Electron)             │ │
│  │  ┌─────────┐ ┌─────────┐ ┌───────────────┐  │ │
│  │  │ AI 助手  │ │ MC 开发  │ │ 服务器管理    │  │ │
│  │  │ (Hermes) │ │ 工具集   │ │ 面板          │  │ │
│  │  │          │ │         │ │               │  │ │
│  │  └─────────┘ └─────────┘ └───────────────┘  │ │
│  └──────────────────────────────────────────────┘ │
│                       │                           │
│         ┌─────────────┼─────────────┐             │
│         ▼             ▼             ▼             │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐         │
│  │ 本地 LLM  │ │ Gradle/  │ │ MC 启动器 │         │
│  │ (Ollama) │ │ Maven    │ │ (Prism/  │         │
│  │          │ │          │ │  自研)   │         │
│  └──────────┘ └──────────┘ └──────────┘         │
│                       │                           │
│         ┌─────────────┼─────────────┐             │
│         ▼             ▼             ▼             │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐         │
│  │ Java 运行 │ │ MC 服务器 │ │ MC 客户端 │         │
│  │ 时       │ │ 实例     │ │ 实例     │         │
│  └──────────┘ └──────────┘ └──────────┘         │
└──────────────────────────────────────────────────┘
```

### 技术栈

| 层级 | 技术 | 说明 |
|------|------|------|
| 基础框架 | VSCodium (Electron + TypeScript) | IDE 主体 |
| AI 引擎 | Hermes（自研，TypeScript） | AI 助手核心，Skill 市场与云端同步 |
| AI 模型 | DeepSeek / Ollama 本地模型 | 默认模型配置 |
| 扩展开发 | TypeScript + VS Code Extension API | 自定义扩展 |
| 构建工具 | Gradle / Maven 集成 | MC 项目构建 |
| 启动器 | Prism Launcher CLI / 自研 Rust+Tauri | 本地测试启动 |
| 服务器管理 | Node.js 子进程 + WebSocket | 服务端控制 |
| 打包分发 | Electron Builder | 跨平台打包 |

---

## 项目结构

```
mcade/
├── icons/                        # MCADE 图标资源
│   ├── mcade-logo.png            # MCADE Logo（您的图标）
│   ├── stable/                   # 稳定版 SVG 图标
│   ├── insider/                  # 预览版 SVG 图标
│   └── build_icons.sh            # 图标生成脚本
│
├── src/                          # 平台资源文件
│   ├── mcade-stable/             # MCADE 稳定版资源（品牌定制）
│   │   ├── resources/
│   │   │   ├── darwin/           # macOS 图标 (.icns)
│   │   │   ├── linux/            # Linux 桌面文件、图标
│   │   │   ├── server/           # Web 服务图标
│   │   │   └── win32/            # Windows 图标 (.ico, .bmp)
│   │   └── src/vs/workbench/     # 内置图标和欢迎页资源
│   ├── mcade-insider/            # MCADE 预览版资源
│   ├── stable/                   # VSCodium 稳定版资源（原始）
│   └── insider/                  # VSCodium 预览版资源（原始）
│
├── patches/                      # VSCodium 补丁
│   └── user/                     # 用户自定义补丁
│
├── build/                        # 构建脚本和安装包配置
│   └── windows/                  # Windows MSI 安装包配置
│
├── dev/                          # 开发构建环境
│   ├── build.sh                  # 构建入口脚本
│   └── build.env                 # 构建环境变量
│
├── .github/workflows/            # GitHub Actions CI/CD
│   ├── ci-build-*.yml            # CI 构建工作流（linux/macos/windows）
│   └── publish-*.yml             # 发布工作流
│
├── product-mcade.json            # MCADE 产品配置
├── prepare_vscode.sh             # 构建准备脚本（已修改支持 MCADE）
├── undo_telemetry.sh             # 遥测禁用脚本
└── utils.sh                      # 工具函数
```

---

## 构建指南

### 环境要求

| 工具 | 版本 | 说明 |
|------|------|------|
| Git | 任意 | 用于拉取子模块 |
| Node.js | >= 22.x | JavaScript 运行时 |
| npm | >= 10.x | 包管理器 |
| Python | 3.x | 构建依赖 |
| jq | 任意 | JSON 处理工具 |
| Visual Studio | 2022 | Windows 构建需要 MSVC 编译器 |

### 本地构建

> **注意：本地构建非常耗时（30-60分钟），建议使用 GitHub Actions 云端构建。**

```bash
# 1. 克隆仓库（含子模块）
git clone https://github.com/silent-QAQ/mcade.git
cd mcade
git submodule update --init --recursive

# 2. 进入 vscodium 目录
cd vscodium

# 3. 设置环境变量（可选，使用 VSCodium 默认版时跳过）
export APP_NAME="MCADE"
export VSCODE_QUALITY="stable"  # 或 "insider"

# 4. 执行构建
bash ./dev/build.sh
```

**Windows 本地构建参考：**

```powershell
# 在 PowerShell 中设置环境变量
$env:APP_NAME = "MCADE"
$env:VSCODE_QUALITY = "stable"

# 通过 Git Bash 执行构建
& "C:\Program Files\Git\bin\bash.exe" ./dev/build.sh
```

### GitHub Actions 云端构建

此仓库已预配置完整的 GitHub Actions CI/CD 工作流，推荐使用云端构建：

1. **推送代码到 GitHub 仓库**

```bash
git push origin master
```

2. **在 GitHub 仓库页面触发构建**
   - 进入 `Actions` 选项卡
   - 选择 `CI Build (Windows/Linux/macOS)`
   - 点击 `Run workflow`
   - 输入环境变量：
     - `APP_NAME`: `MCADE`（构建 MCADE 版本）
     - `VSCODE_QUALITY`: `stable` 或 `insider`
   - 点击 `Run workflow` 确认

3. **等待构建完成**
   - 构建通常需要 30-60 分钟
   - 完成后在对应 workflow run 的 Artifacts 或 Release 中下载安装包

### 发布的触发方式

| 触发方式 | 说明 |
|---------|------|
| `workflow_dispatch` | 手动触发（推荐） |
| tag 推送 | 自动触发发布流程（`git tag v1.0.0` 并推送） |
| 定时构建 | 配置 cron 定时触发（可选） |

### 环境变量说明

| 变量 | 可选值 | 说明 |
|------|--------|------|
| `APP_NAME` | `MCADE` / `VSCodium` | 构建的品牌版本 |
| `VSCODE_QUALITY` | `stable` / `insider` | 稳定版或预览版 |
| `SHOULD_BUILD` | `yes` / `no` | 是否执行构建 |
| `SKIP_SOURCE` | `yes` / `no` | 是否跳过源码拉取 |
| `SKIP_ASSETS` | `yes` / `no` | 是否跳过资源打包 |
| `SKIP_BUILD` | `yes` / `no` | 是否跳过编译阶段 |
| `DISABLE_UPDATE` | `yes` / `no` | 是否禁用自动更新 |
| `CI_BUILD` | `yes` / `no` | 是否为 CI 环境构建 |
| `OS_NAME` | `osx` / `linux` / `windows` | 目标操作系统 |

---

## 品牌定制指南

### 已完成的品牌修改

- [x] **产品标识：** `product-mcade.json` 定义了 MCADE 的名称、图标名、协议、GUID 等
- [x] **构建脚本：** `prepare_vscode.sh` 支持 `APP_NAME=MCADE` 模式
- [x] **资源目录：** 创建了 `src/mcade-stable/` 和 `src/mcade-insider/` 资源目录
- [x] **Logo：** 已添加到 `icons/mcade-logo.png`

### 自定义 product.json

编辑 `product-mcade.json` 可自定义：

```json
{
  "nameShort": "MCADE",
  "nameLong": "Minecraft Community AI Development Environment",
  "applicationName": "mcade",
  "win32DirName": "MCADE",
  "win32AppUserModelId": "MCADE.MCADE",
  "darwinBundleIdentifier": "com.mcade.MCADE",
  "extensionsGallery": {
    "serviceUrl": "https://open-vsx.org/vscode/gallery"
  }
}
```

### 替换图标

1. 将图标 PNG 文件放到 `icons/mcade-logo.png`
2. 运行图标生成脚本生成各平台格式：

```bash
# 需要安装 ImageMagick、icns2png、icotool 等工具
bash icons/build_icons.sh
```

3. 或通过 GitHub Actions 自动处理图标转换

### 添加自定义补丁

在 `patches/user/` 目录添加 `.patch` 文件：

```bash
# 在 vscode 目录生成补丁
cd vscode
git diff --relative > ../patches/user/my-customization.patch
```

补丁会在构建时自动应用。

---

## 开发路线图

### 第一阶段：MVP（进行中）

| 任务 | 状态 | 说明 |
|------|------|------|
| 1.1 Fork VSCodium，品牌定制 | ✅ 已完成 | 修改品牌、图标、应用名 |
| 1.2 开发 Hermes AI 扩展 | 🔄 进行中 | 自研 AI 助手，含 Skill 市场与云端同步 |
| 1.3 MC 项目脚手架 | ⏳ 待开始 | 一键创建项目模板 |
| 1.4 代码片段库 | ⏳ 待开始 | MC 开发 Snippets |
| 1.5 Gradle 集成 | ⏳ 待开始 | 构建可视化 |
| 1.6 构建流水线 | ⏳ 待开始 | 一键 Build → JAR |
| 1.7 打包与自动更新 | ⏳ 待开始 | 跨平台安装包 |

### 第二阶段：核心功能

| 任务 | 说明 |
|------|------|
| 2.1 MC 专用 AI Chat 参与者 | 内置 MC 开发知识库 |
| 2.2 本地 LLM 集成 | 一键安装 Ollama |
| 2.3 服务器管理面板 | 侧边栏管理 MC 服务器 |
| 2.4 实时控制台 | WebSocket 连接 |
| 2.5 启动器集成 | 集成 Prism Launcher |
| 2.6 资源文件编辑器 | JSON 可视化编辑 |
| 2.7 调试器配置 | 一键 Java Debug |

### 第三阶段：高级功能

| 任务 | 说明 |
|------|------|
| 3.1 自研轻量启动器 | 专为测试优化 |
| 3.2 可视化资源编辑器 | 纹理/模型预览 |
| 3.3 Mod 发布助手 | 一键发布到 CurseForge/Modrinth |
| 3.4 团队协作 | Git 深度集成 |
| 3.5 插件市场 | 第三方扩展/模板 |
| 3.6 多语言支持 | 中、英、日、韩等 |

---

## 参与贡献

我们欢迎各种形式的贡献！无论是报告 Bug、提交功能建议、改进文档，还是提交代码。

### 如何开始

1. Fork 本仓库
2. 创建特性分支：`git checkout -b feature/my-feature`
3. 提交修改：`git commit -am 'Add my feature'`
4. 推送分支：`git push origin feature/my-feature`
5. 提交 Pull Request

### 开发规范

- 提交信息请使用英文，保持简洁清晰
- 代码风格遵循项目现有规范
- 添加新功能时请同时更新文档
- 确保补丁保持最小化，便于上游同步

---

## 许可证

本项目基于 MIT 许可证开源。

- VSCodium 部分遵循 MIT 许可证
- VS Code 部分遵循 MIT 许可证（Microsoft 的 VS Code）
- 自定义扩展和脚本遵循 MIT 许可证

完整的许可证信息请参见 [LICENSE](LICENSE) 文件。

---

## 致谢

- [VSCodium](https://github.com/VSCodium/vscodium) - 提供自由的 VS Code 构建
- [Continue.dev](https://github.com/continuedev/continue) - 开源 AI 编程助手
- [Microsoft VS Code](https://github.com/microsoft/vscode) - 优秀的代码编辑器
- [Prism Launcher](https://github.com/PrismLauncher/PrismLauncher) - 开源 Minecraft 启动器
- 所有 Minecraft 开发者和社区贡献者

---

<p align="center">
  由 ❤️ 和 Minecraft 社区驱动<br>
  Made with love for the Minecraft developer community
</p>