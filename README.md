# YOLOv5-Lite · YOLOv8 通道（规划中）— 仓库 yolov5-lite-v8-5090

> 「5090」为本机 AI 推理产品线统一后缀；本仓库对应 **YOLOv8** 版本通道。
> 版本号区间（详见主仓库路线图）：**2.0.1 – 2.9.8**

## 状态
🚧 规划中 / 待实施。当前为占位与方案备份仓库，尚未包含可编译代码。

## 背景
主仓库 [yolov5-lite-v5-5090](https://github.com/g101400/yolov5-lite-v5-5090) 已完成 YOLOv5（v5lite）安卓版 v1.2.1。
本仓库将承接 **YOLOv8** 接入，版本号从 **2.0.1** 起。

## 关键改造点
- YOLOv8 为 **anchor-free**，输出形状与解码方式（DFL / 端到端 NMS）与 v5 不同，**不能复用 v5 后处理**；
- 建议先在主仓库抽 `ModelRuntime` 接口，本仓库只新增 `Yolov8Runtime` 实现，Java/UI 零改动；
- 推理后端仍为 ncnn（需导出 v8 的 ncnn 模型）或 OpenCV DNN / ONNX Runtime（Windows 版）。

## 实施步骤（参考主仓库 规划与方案.md 第四节）
1. 抽 `ModelRuntime` 接口，迁移 v5 逻辑；
2. 导出 YOLOv8 ncnn / ONNX 权重（放入 `assets/`）；
3. 实现 `Yolov8Runtime` 后处理；
4. 复用主仓库的中文标签、状态栏、CSV 落盘、帮助/关于菜单；
5. 安卓 `./gradlew assembleRelease` + Windows PyInstaller/NSIS 打包。

## 许可
沿用主仓库约定（ncnn BSD-3-Clause + 上游 demo 许可）。
