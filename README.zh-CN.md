# Materializr（本机构建副本）

> 本仓库是上游开源项目 [materializr-cad/materializr](https://github.com/materializr-cad/materializr)
> 的一个**本地构建副本**，用于在 Android/Termux 上编译与调试 APK。
> 上游英文说明见 [README.md](README.md)；许可条款见 [LICENSE](LICENSE)。

## 这是什么

Materializr 是一个开源的参数化 3D CAD 建模工具（类似 OpenSCAD 的即时预览体验），
使用 C++ 编写核心，Android 端通过 JNI + 原生渲染层运行。本副本保留了上游的
`src/`、`assets/`、`tests/`、`tools/`、`docs/` 与 `android/` 工程，用于在手机上出包。

## 目录结构

```
materializr-main/
├── src/             C++ 核心（几何内核、脚本解释器、渲染、UI）
├── assets/          内置示例模型与资源
├── android/         Android 壳工程（Gradle + JNI + CMake）
│   └── app/src/main/{java,jni,assets,res}
├── tests/           单元测试与集成测试
├── tools/           构建与打包脚本
├── docs/            架构与开发文档
├── CMakeLists.txt   桌面端 / 交叉编译入口
└── Dockerfile       可复现构建环境
```

## 构建（Android）

```bash
cd android
./gradlew assembleDebug          # 产出 app/build/outputs/apk/debug/
./gradlew assembleRelease        # 需要自行配置签名
```

需要 Android SDK（platform 35）、NDK、JDK 17。首次构建会通过 CMake 拉取
`third_party`（imgui / glfw / glm），因此需要网络。

## 说明

- `android/app/build/`、`android/app/.cxx/`、`android/.gradle/` 等构建产物不入库。
- 本副本的修改（若有）与上游保持同步，提交前请以向上游提交 PR 为首选。
