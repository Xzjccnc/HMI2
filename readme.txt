项目名称：车载手势交互系统（VISION OS V1.0）

项目简介：
- 基于浏览器的车载手势控制系统，使用摄像头识别手势，实现界面切换、地图缩放、音量调节等交互
- 技术栈：MediaPipe Hands（手势识别）+ Three.js（3D 背景动画）+ Tailwind CSS（UI 样式）+ FontAwesome（图标）
- 以纯前端方式运行，无需后端服务

功能概览：
- 屏幕切换：仪表盘（Dashboard）、地图（Map）、音乐（Music）三大界面
- 手势交互：
  - 挥手切换界面：检测手腕 X 轴的快速移动，左右切换屏幕
  - 捏合调节：拇指与食指间距映射为 0~1，用于音乐界面的音量和地图界面的缩放
- 手势可视化：屏幕上的手势光标，捏合时光标变小并高亮
- 3D 背景：赛博风格无限隧道（网格地面 + 星点粒子），根据模拟车速动态变化
- 状态栏与小组件：速度表、电量、续航、导航、音乐播放器、全屏切换按钮

快速开始：
1) 直接打开：双击 `index.html`（推荐使用 Chrome/Edge 最新版本）
2) 点击“启动引擎（开启摄像头）”按钮
3) 浏览器弹出权限提示时选择允许摄像头
4) 使用手势：
   - 左右挥手：切换界面
   - 捏合手势：在音乐界面调节音量，在地图界面缩放地图
5) 需要网络以加载 CDN 资源；如需离线使用，请参考“依赖与版本”将资源本地化

运行环境建议：
- 操作系统：Windows/macOS/Linux 任意
- 浏览器：Chrome/Edge 最新版，需支持摄像头访问（HTTPS 或本地文件）
- 硬件：可用的摄像头，且不被其他应用占用
- 网络：外网可用，用于加载 CDN 资源

依赖与版本（通过 CDN 加载）：
- Tailwind CSS：`https://cdn.tailwindcss.com`
- Three.js：`https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js`（r128）
- MediaPipe：
  - `@mediapipe/camera_utils`：`https://cdn.jsdelivr.net/npm/@mediapipe/camera_utils/camera_utils.js`
  - `@mediapipe/control_utils`：`https://cdn.jsdelivr.net/npm/@mediapipe/control_utils/control_utils.js`
  - `@mediapipe/hands`：`https://cdn.jsdelivr.net/npm/@mediapipe/hands/hands.js`
- FontAwesome 图标：`https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css`（6.4.0）

手势细节（与实现对应）：
- 挥手切换：当手腕 X 轴位移的绝对值 > 0.08（归一化坐标）时触发；向左为下一屏，向右为上一屏，设有 1 秒冷却
- 捏合判定：拇指尖与食指尖距离 < 0.05 时显示捏合光标效果
- 捏合映射：将距离在约 0.02~0.25 的范围线性映射为 0~1，用于音量和地图缩放

界面说明：
- 仪表盘：速度表（动态数字）、电量、续航、档位；右侧导航与音乐组件
- 地图：网格背景、路线 SVG、车辆位置、缩放指示
- 音乐：唱片视觉、播放控制、音量条（捏合调整）

常见问题：
- 摄像头被占用（NotReadableError/Device in use）：关闭其他占用摄像头的软件或浏览器标签页后重试
- 权限拒绝（NotAllowedError/PermissionDeniedError）：在浏览器设置中允许摄像头访问并刷新页面
- 无网络：无法加载 CDN 资源，建议改为本地化依赖或使用本地服务器

目录结构：
- `index.html`：主页面与脚本、样式（通过 CDN 引入）

本地化与离线建议（可选）：
- 将上述 CDN 文件下载至本地并使用相对路径引用，固定版本号
- 使用本地静态服务器（如 `http-server` 或 `live-server`）提高兼容性与权限管理