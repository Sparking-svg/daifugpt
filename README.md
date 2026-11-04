<p align="center"><img src="DaiFuGPT.png" alt="DaiFuGPT" width="96"></p>

# DaiFuGPT

一个简洁的本地 API 配置器。选择站点、选择 Claude 或 Codex、填写密钥、勾选模型，然后导入。

**v0.1.10** · [下载](https://github.com/Sparking-svg/daifugpt/releases/tag/v0.1.10) · [反馈问题](https://github.com/Sparking-svg/daifugpt/issues) · [官网](https://daifu.men/) · [MIT 许可](LICENSE)

## 下载与使用

| 系统 | 下载 | 打开方式 |
| --- | --- | --- |
| Windows 10 / 11 · x64 | [Windows 免安装 ZIP](https://github.com/Sparking-svg/daifugpt/releases/download/v0.1.10/DaiFuGPT.zip) | 全部解压，双击 `DaiFuGPT.exe` |
| macOS 12+ · Apple Silicon | [Mac ZIP](https://github.com/Sparking-svg/daifugpt/releases/download/v0.1.10/DaiFuGPT-0.1.10-macOS-arm64.zip) | 解压后打开 `DaiFuGPT.app`，也可拖入「应用程序」 |

本页使用 [GitHub Releases](https://github.com/Sparking-svg/daifugpt/releases) 分发安装包，[SHA-256 校验值](https://github.com/Sparking-svg/daifugpt/releases/download/v0.1.10/SHA256SUMS.txt)也位于同一版本下。Mac 包仅支持 M 系列芯片，不支持 Intel Mac。运行时无需安装 Node.js 或 Rust。Windows 需要系统具备 Microsoft Edge WebView2 Runtime；缺少时从[微软官网](https://developer.microsoft.com/microsoft-edge/webview2/)安装。

Windows 包尚未进行发布者签名；Mac 包采用 ad-hoc 签名，尚未完成 Apple Developer ID 签名与公证。构建与测试范围见 [VERIFICATION.md](VERIFICATION.md)。

### 下载与打开提示

请从本仓库的 Release 下载，完整解压后运行。遇到系统提示时先核对文件来源、版本及摘要；校验值用于检查文件完整性。反馈时附上提示原文，不要附上 API 密钥。

### 配置步骤

1. **选择站点**：默认 [DaiFuGPT](https://daifu.men/dashboard)，也可添加自己的站点，一次使用一个。
2. **选择客户端**：选择 Claude 或 Codex，再按需要选择桌面版、终端版或 VS Code 扩展。
3. **输入 API Key**：从[本站密钥页](https://daifu.men/keys)获取个人密钥，点击获取可用模型。
4. **勾选模型并导入**：选择所需模型、指定默认模型，核对预览后导入。

导入后完全退出目标客户端，再重新打开并新建会话。Claude 在 Windows 上可能留在托盘，需要从托盘菜单退出。需要撤回时，点击“恢复原配置”，选择客户端后恢复。删除配置器不会自动恢复客户端设置。

## 支持的客户端

| 客户端 | 配置方式 |
| --- | --- |
| Claude 桌面版 | 支持第三方推理模式的客户端配置 |
| Claude Code 终端版 | 用户配置中的 API 地址、默认模型与可用模型 |
| Claude Code · VS Code | 支持范围内的扩展设置与 Claude Code 配置 |
| Codex 桌面版与终端版 | 本地 provider、API 认证与所选模型目录 |

适配范围是支持本地 API 配置的客户端版本，不包含网页版、手机端或云端任务。Windows 版配置 Windows 本机客户端；WSL、Remote SSH 等环境需要分别配置。

本站模型和协议权限由密钥分组决定。读取模型列表和写入配置成功，不等于所有对话与工具功能已验证；导入后请在新会话中确认，并到[本站使用记录](https://daifu.men/usage)核对请求。

## 配置与数据

- 默认连接 DaiFuGPT，站点地址为 `https://daifu.men`。
- API 密钥用于选定站点的请求和客户端配置，不保存在站点偏好列表中。
- 导入前备份原配置，支持恢复。导入前请核对软件展示的变更。
- 恢复记录使用独立的 `.daifugpt` 用户目录。
- 认证配置与恢复记录可能包含凭据，请勿公开上传。
- 支持浅色与深色界面，应用、窗口及包内程序统一使用 DaiFuGPT 名称和紫色大写 D 图标。

## 开发与构建

源码包：[DaiFuGPT-0.1.10-source.zip](DaiFuGPT-0.1.10-source.zip)。解压并进入 `DaiFuGPT-source`，准备 Node.js 22+、pnpm 10 与稳定版 Rust。macOS 需要 Xcode Command Line Tools，Windows 需要 MSVC Build Tools 与 Windows SDK。

```bash
pnpm install --frozen-lockfile
pnpm check
pnpm test:ui
cargo test --manifest-path src-tauri/Cargo.toml --no-default-features --locked
```

`pnpm dev:web` 用于界面预览。原生应用开发使用 `pnpm dev`。打包：

```bash
# macOS Apple Silicon（在 Mac 环境执行）
rustup target add aarch64-apple-darwin
pnpm build:macos

# Windows x64 免安装包（在 Windows 环境执行）
pnpm build:windows
```

产物位于 `release/`。[Mac 构建流程](https://github.com/Sparking-svg/daifugpt/actions/workflows/build-macos-0110.yml)核对源码摘要，执行检查后验证应用名称、图标、版本、arm64 架构和 ad-hoc 签名。

## 隔离测试

自动测试使用隔离目录和虚构密钥，不调用真实付费模型。本地开发请使用独立测试目录，避免覆盖日常客户端配置。真实端到端客户端验证的范围见 [VERIFICATION.md](VERIFICATION.md)。

反馈问题时请说明系统、DaiFuGPT 与客户端版本、操作步骤和错误原文；不要上传 API 密钥、认证文件或完整恢复记录。

## 开源与许可

采用 MIT 许可，保留相关版权与许可证。使用 React、Tauri 和 Rust；详细说明见 [LICENSE](LICENSE) 与 [THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md)。本项目独立维护，不是 Claude 或 Codex 的官方客户端。
