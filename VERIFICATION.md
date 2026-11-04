# DaiFuGPT 0.1.10 验证记录

## Windows

- Windows x64 原生 release 编译完成，产品名和文件说明均为 DaiFuGPT，版本为 0.1.10。
- 完整包内含 DaiFuGPT.exe、使用说明和许可证；使用说明已去掉本次要求移除的两行。
- 已核对 PE 架构、GUI 子系统、依赖、文件名、字节数和 SHA-256。

## macOS

- 在 GitHub 的 Apple Silicon 原生环境编译，18 项前端测试、类型检查和隔离原生核心测试通过。
- 版本 0.1.10、应用名 DaiFuGPT.app、标识 men.daifu.daifugpt、arm64 架构均已核对。
- 紫色 D 图标与项目源图一致，ad-hoc 签名通过检查，最终 Mach-O 代码页摘要也已核对。
- 包内使用说明仅提供本站官网、教程和本仓库入口；必需许可证完整保留。

## 验证范围

尚未完成全部真实客户端的端到端导入、对话与工具调用测试。Windows 未作发布者代码签名；macOS 未完成 Apple Developer ID 签名及公证。Mac 包仅适用于 macOS 12+ 的 Apple Silicon 电脑。

完整校验值见 Release 的 SHA256SUMS.txt。
