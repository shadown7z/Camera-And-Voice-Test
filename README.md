# 📷 摄像头与音视频采集测试工具

> 一款基于 Web 的摄像头、麦克风设备状态及音视频采集质量检测工具。纯前端实现，无需安装任何依赖。

## ✨ 功能特性

| 模块 | 功能 | 技术实现 |
|------|------|----------|
| 🔐 **权限检测** | 检测浏览器摄像头/麦克风授权状态 | `getUserMedia()` + `Permissions API` |
| 🎥 **设备检测** | 枚举系统中所有音视频输入设备 | `enumerateDevices()` |
| 🖥️ **画面测试** | 黑屏、闪屏、画面颠倒、分辨率、亮度、对比度 | Canvas 逐帧分析 |
| 🎤 **音频同步** | 麦克风收音检测、实时频谱可视化、音画同步评估 | Web Audio API + AnalyserNode |
| 📋 **测试报告** | 结构化报告生成，支持 JSON/Markdown 导出 | 自动汇总 + Blob 下载 |

## 🚀 快速开始

### 方式一：直接打开（推荐）

```bash
# 克隆或下载本项目后，直接用浏览器打开 index.html
# 注意：摄像头 API 需要 localhost 或 HTTPS 环境
```

### 方式二：使用本地服务器

```bash
# Python 3
python -m http.server 8080

# Node.js
npx serve .

# 然后访问 http://localhost:8080
```

## 📖 使用指南

按 5 步流程依次操作：

```
步骤 1: 权限检测 → 步骤 2: 设备检测 → 步骤 3: 画面测试 → 步骤 4: 音频同步 → 步骤 5: 测试报告
```

1. **点击「检测权限」** — 浏览器会弹出摄像头/麦克风权限请求，请点击允许
2. **点击「检测设备」** — 自动识别系统中所有摄像头和麦克风设备
3. **点击「开启摄像头」→「分析画面」** — 实时预览并分析画面质量
4. **点击「开启麦克风」→「测试音画同步」** — 检测音频输入并评估同步
5. **查看测试报告** — 可导出 JSON / Markdown 或复制到剪贴板

## 🖥️ 界面预览

- **暗色主题** — 护眼深色背景（`#0f172a`），蓝色系主色调
- **卡片式布局** — 5 个功能卡片按步骤排列，清晰直观
- **进度导航** — 顶部 5 步进度条，实时显示测试进度
- **实时反馈** — 视频预览、音频波形可视化、运行日志面板
- **响应式设计** — 支持桌面端和移动端
<img width="1383" height="947" alt="image" src="https://github.com/user-attachments/assets/8fbad13b-6438-40b3-873d-6130722ef9b7" />
<img width="1383" height="947" alt="image" src="https://github.com/user-attachments/assets/9bfa51b8-1bff-4ae1-a367-9ea2404449eb" />
<img width="1383" height="947" alt="image" src="https://github.com/user-attachments/assets/06178e2a-2a77-4375-a818-e94d2acd9edd" />

## 🧪 检测项说明

### 画面检测
| 检测项 | 判定标准 |
|--------|----------|
| 黑屏检测 | 分析 60 帧画面亮度，黑帧率 > 80% 判定为黑屏 |
| 闪屏检测 | 帧间亮度突变次数 > 30% 判定为闪烁 |
| 画面颠倒 | 比较画面上下半区平均亮度差异 |
| 镜像模式 | CSS `scaleX(-1)` 实现镜像显示 |
| 分辨率 | 通过 `MediaTrackSettings` 获取实际分辨率 |

### 音频检测
| 检测项 | 判定标准 |
|--------|----------|
| 麦克风收音 | 3 秒采样周期内检测到有效音频信号 |
| 音量等级 | 平均音量百分比（0-100%） |
| 音画同步 | 基于音频信号存在的定性评估 |

## 📦 导出格式

### JSON
```json
{
  "timestamp": "2026-05-09T15:00:00.000Z",
  "summary": { "passed": 4, "total": 4, "cameras": 1, "microphones": 1 },
  "permission": { "camera": true, "microphone": true },
  "devices": { "cameras": [...], "microphones": [...] },
  "video": { "resolution": "1280×720", "isBlack": false, ... },
  "audio": { "hasAudio": true, "audioLevel": 45, ... }
}
```

### Markdown
生成结构化的 Markdown 报告，包含表格形式的测试结果。

## ⚙️ 技术栈

- **HTML5** — 语义化标签 + Canvas API
- **CSS3** — Flexbox/Grid 布局 + 暗色主题 + 响应式设计
- **JavaScript (ES6+)** — 异步编程 + Web API 调用
- **Web APIs** — `getUserMedia` / `enumerateDevices` / `Permissions API` / `Canvas API` / `Web Audio API`

## ⚠️ 注意事项

1. **环境要求**: 需要 `localhost` 或 `HTTPS` 环境（浏览器安全策略）
2. **浏览器兼容**: 支持 Chrome、Edge、Firefox 最新版本
3. **权限授权**: 首次使用需手动允许摄像头/麦克风权限
4. **隐私安全**: 所有媒体流在使用后立即释放，不存储任何音视频数据

## 📁 项目结构

```
CameraTest/
├── index.html              # 主页面（完整测试工具）
├── README.md               # 本文件
└── PRD/
    └── camera-test-tool-prd.md  # 需求文档
```

## 📄 许可证

MIT License
