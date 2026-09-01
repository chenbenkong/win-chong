# win-chong · 伪 Live2D 桌宠模型生成器

上传一张照片、动态 GIF 或多张姿势图，一键生成可导入**定制版 BongoCat** 的伪 Live2D 模型文件夹。全程浏览器本地处理，素材不上传服务器。

## 在线使用

直接打开：**https://chenbenkong.github.io/win-chong/**

（或下载 `index.html` 双击本地打开，效果相同）

## 功能

- 单张图片 → 呼吸起伏 + 轻微摇摆 + 鼠标跟随
- 动态 GIF（自动拆帧，保留原始节奏，上限 60 帧）/ 多张姿势图 → 按时间线轮播动作，切换带淡入淡出
- 可选 AI 抠图去背景（MediaPipe Selfie Segmentation，多 CDN 自动切换，失败自动降级不阻断导出）
- 一键导出文件夹（File System Access API）或 ZIP 压缩包
- 内置实时预览，所见即所得

## 导入 BongoCat

1. 生成的模型文件夹（或解压 ZIP 得到的文件夹）
2. 打开**定制版** BongoCat → 偏好设置 → 模型管理 → 导入该文件夹
3. 在模型列表中点击启用

> 注意：此伪模型格式（`.pseudo.json` + `layers/` 分层 PNG）需要配合修改版 BongoCat 渲染器，官方原版不支持。

## 模型格式

```
模型名/
├── 模型名.pseudo.json   # 入口：画布、图层、动画轨道、物理参数
└── layers/
    ├── frame_0.png      # 每帧一张分层图
    ├── frame_1.png
    └── ...
```

`pseudo.json` 支持：图层位移/缩放/旋转/透明度的参数绑定（`ParamAngleX` 鼠标跟随、`ParamBreath` 呼吸等）、关键帧动画轨道（`animation.tracks`）、眨眼与呼吸物理。

## 定制版 BongoCat

基于开源 [ayangweb/BongoCat](https://github.com/ayangweb/BongoCat)（MIT）修改：新增伪模型渲染器（`src/utils/pseudo.ts`）与双格式分发加载。修改版安装包不在本仓库分发，需要请自行按上述改动编译。

## License

MIT
