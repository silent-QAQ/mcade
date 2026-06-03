# MCADE - Minecraft Community AI Development Environment

基于 VSCodium 定制的 Minecraft 社区开发者 AI 集成开发环境。

## 构建说明

### 本地构建（不推荐，很慢）

由于本地构建需要较长时间，建议使用 GitHub Actions 进行云端构建。

### GitHub Actions 云端构建

1. 把此项目推送到您的 GitHub 仓库
2. 在 GitHub Actions 中手动触发构建，或通过 tag 触发
3. 构建完成后会在 Release 中提供下载

### 环境变量

- `APP_NAME`: 设置为 `MCADE` 以构建 MCADE 版本，否则构建 VSCodium
- `VSCODE_QUALITY`: 设置为 `stable` 或 `insider`

## 项目结构

```
vscodium/
├── src/mcade-stable/       # MCADE 稳定版的资源文件
├── src/mcade-insider/      # MCADE 预览版的资源文件
├── product-mcade.json      # MCADE 产品配置
├── icons/mcade-logo.png    # MCADE 图标
└── prepare_vscode.sh       # 构建准备脚本（已修改以支持 MCADE）
```

## 自定义品牌

目前已完成的品牌修改：
- [x] product.json - 应用名称、协议、标识符等
- [x] prepare_vscode.sh - 构建脚本支持 APP_NAME=MCADE 模式
- [ ] 图标转换（需要在 GitHub Actions 中处理）
- [ ] 更多自定义...

## 后续开发计划

请查看项目根目录的 `项目计划书.md` 获取完整的开发计划。
