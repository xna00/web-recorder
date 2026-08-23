# 浏览器录屏工具 / Browser Screen Recorder

纯前端、单文件、零依赖的屏幕录制工具。直接在浏览器里运行，无需安装任何软件、无需服务器、无需构建。

## 功能

- 录制**屏幕 / 应用窗口 / 浏览器标签页**
- **系统声音 + 麦克风混音**（各自可选）
- **摄像头画中画**：圆角浮窗，四角可选，带实时预览
- 暂停 / 继续、停止自动收尾
- 录制中实时预览、停止后回放与下载
- 格式自适应：优先 MP4（Chrome/Edge/Safari），不支持时回退 WebM
- 状态指示、计时、日志

## 用法

直接用桌面端浏览器（推荐 Chrome / Edge）打开 `index.html` 即可。

## 跨平台音频说明（重要）

系统音频能否录到，取决于**系统版本 + 浏览器 + 分享弹窗里是否勾选「共享音频」**三者叠加：

| 平台 | 系统音频 | 说明 |
|---|---|---|
| Windows | ✅ | Chrome/Edge 走 WASAPI loopback，勾选「共享音频」即可 |
| macOS | ⚠️ | 14.2+ 且 Chrome 141+ 才支持；旧系统不支持；需勾「共享系统音频」 |
| Linux | ❌ | 多数发行版/浏览器无法采集系统音频，建议用麦克风混音或 PipeWire monitor 虚拟设备 |
| Safari | ❌ | 对 `getDisplayMedia` 音频支持弱 |

> 所有平台共通：若分享弹窗**未勾选「共享音频 / Share audio」**，结果都只有画面没声音——这是操作问题，与系统无关。

## 技术

- `getDisplayMedia` + `MediaRecorder` + `AudioContext` 混音
- 摄像头画中画：`canvas.captureStream()` + `requestVideoFrameCallback`（rVFC）事件驱动重绘，并带 Web Worker 兜底计时器，缓解页面最小化时的冻结

## 在线地址

- 自建域名：<https://rec.xna00.top>
- Cloudflare Pages：<https://web-recorder.pages.dev>

## 许可

MIT
