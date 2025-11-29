<p align="center">
  <img src="public/logo.svg" width="100" height="100" alt="Status Monitor Logo">
</p>

<h1 align="center">站点监测</h1>

<p align="center">优雅的站点状态监控面板</p>

<p align="center">
  <img src="https://img.shields.io/badge/Vue.js-3.5-4FC08D?logo=vue.js" alt="Vue">
  <img src="https://img.shields.io/badge/Tailwind_CSS-3.4-38B2AC?logo=tailwind-css" alt="Tailwind">
  <img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License">
</p>

<p align="center">
  <a href="https://vercel.com/new/clone?repository-url=https://github.com/RunWang925/Uptime-Status" title="使用 Vercel 部署">
    <img src="https://vercel.com/button" alt="Deploy with Vercel" />
  </a>
  <a href="https://edgeone.ai/pages/new?repository-url=https%3A%2F%2Fgithub.com%2FRunWang925%2FUptime-Status&output-directory=dist&install-command=npm%20install&build-command=npm%20run%20build" target="_blank" rel="noopener noreferrer">
    <img src="https://cdnstatic.tencentcs.com/edgeone/pages/deploy.svg" alt="Deploy with EdgeOne Pages">
  </a>
  <a href="https://console.cloud.tencent.com/edgeone/pages?action=create" title="使用腾讯云 EdgeOne Pages 部署">
    <img src="https://img.shields.io/badge/-Deploy-00A4FF?style=for-the-badge&labelColor=00A4FF&color=00A4FF&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxMjgiIGhlaWdodD0iMTI4IiB2aWV3Qm94PSIwIDAgMjQgMjQiPjxwYXRoIGZpbGw9IndoaXRlIiBkPSJNNi41IDIwcS0yLjI3NSAwLTMuODg3LTEuNTc1VDEgMTQuNTc1cTAtMS45NSAxLjE3NS0zLjQ3NVQ1LjI1IDkuMTVxLjYyNS0yLjMgMi41LTMuNzI1VDEyIDRxMi45MjUgMCA0Ljk2MyAyLjAzOFQxOSAxMXExLjcyNS4yIDIuODYzIDEuNDg4VDIzIDE1LjVxMCAxLjg3NS0xLjMxMiAzLjE4OFQxOC41IDIweiIvPjwvc3ZnPg==&borderRadius=6" alt="部署到腾讯云 EdgeOne" height="32" />
  </a>
  <a href="https://dash.cloudflare.com/" title="使用 Cloudflare Pages 部署">
    <img src="https://img.shields.io/badge/-Deploy-F38020?style=for-the-badge&labelColor=F38020&color=F38020&logo=cloudflare&logoColor=white&borderRadius=6" alt="部署到 Cloudflare Pages" height="32" />
  </a>
</p>

<p align="center">🎮 在线演示：
  <a href="https://status.bsgun.cn" target="_blank">
    https://status.bsgun.cn
  </a>
</p>

## 📖 简介

最初接触这类工具时，是通过清羽飞扬大佬的推荐了解到 StatusLive 项目（仓库地址：https://github.com/willow-god/StatusLive）

但受限于个人技术水平，在部署该项目时未能成功。直到遇到当前这个站点监测项目，不仅顺利完成部署，其稳定的性能也让我最终选择将它作为日常使用的监控工具。
站点监测是一个基于 UptimeRobot API 开发的站点状态监控面板，支持多站点状态监控、实时通知、故障统计等功能。界面简洁美观，响应式设计，支持亮暗主题切换。
遇到的问题 部署好后 加载需要差不多20秒才能加载处理，最后找到了原因并解决

## 🚩 常见问题解决（新增核心章节）

### 问题1：页面加载极慢（20秒+）
部署这个项目后发现访问需要20秒以上，然后检查发现是由于统计脚本无法访问，直接删除index.html的统计脚本

- 根因：`index.html` 中的统计脚本直接删除
```bash
    <!-- 统计 -->
    <script defer src="https://um.bsgun.cn/tongjifenxi.js" data-website-id="6ed9cbf7-8824-4a8a-80b2-eab7f5dd1e00"></script>
```


## ⚙️ 部署配置

### 环境要求

- Node.js >= 16.16.0

- NPM >= 8.15.0 或 PNPM >= 8.0.0

### 获取 UptimeRobot API Key

1. 注册/登录 [UptimeRobot](https://uptimerobot.com/)

2. 进入 [Integrations & API](https://dashboard.uptimerobot.com/integrations)

3. 下拉到最底部在 Main API keys 部分创建 **Read-Only API Key**

4. 复制生成的 API Key
### API 代理说明
本项目支持以下三种部署方式,均可实现自动处理跨域请求:

1. **腾讯云 EdgeOne Pages**
   - 点击上方蓝色 "Deploy" 按钮
   - 连接到GitHub，选择项目
   - 框架预设选择Vue，点击开始部署
   - 使用默认配置 `VITE_UPTIMEROBOT_API_URL = "/api/status"`
   - 部署前先自行修改`.env`



### 快速开始

1. 克隆项目
```bash
git clone https://github.com/RunWang925/Uptime-Status.git
cd uptime-status
```

2. 安装依赖
```bash
pnpm install
# 或
npm install
```

3. 配置环境变量

在 `.env` 文件中修改以下配置：
```bash
# ========== Uptime-Status 核心配置 ==========
# 【模式1：（作者原有模式）】
# 需同时配置 API Key + 代理地址
# VITE_UPTIMEROBOT_API_KEY = "ur3159051-bfdaacf048a30618ac2e6582"  # 必填（UptimeRobot只读API Key）
# VITE_UPTIMEROBOT_API_URL = "/api/status"                       # 模式1必填：指向自建后端代理（取消注释启用）

# 【模式2：代理模式（我自己乱改的）】
# 无需API Key，仅配置公益代理地址（自动隐藏Key，更安全）
# 公益代理地址生成：https://statuslive-vercel.vercel.app/reejishu 美丽世界提供
VITE_UPTIMEROBOT_API_URL = "https://statuslive.freejishu.com/core/?publickey=e68c941e-1b5f-59c8-68ab-442d2a75b068"  # 代理模式必填

# ========== 通用配置（所有模式均生效） ==========
VITE_APP_TITLE = "野猪佩奇弟弟"                                   # 监控面板站点名称（自定义）
# 监控面板排序方式：可选 friendly_name（按名称）/ create_datetime（按创建时间）
VITE_UPTIMEROBOT_STATUS_SORT = "friendly_name"

# ========== 部署&使用注意事项 ==========
# 1. 模式切换：启用对应模式时，仅保留该模式的配置（注释另一模式）
# 2. 加载慢问题：删除index.html中统计脚本可解决（核心优化点）
# 3. 平台适配：腾讯云EdgeOne我目前部署测试无问题
```
这个代理地址部分主要是参考了[StatusLive 项目](https://github.com/willow-god/StatusLive) 项目的说明
代理模式说明：参考自 StatusLive 项目，主要作用是隐藏 API Key 以提高安全性其他用途我不知道

4. 开发调试
```bash
pnpm dev
# 或
npm run dev

# 开发环境需要将 VITE_UPTIMEROBOT_API_URL 设置为 "https://api.uptimerobot.com/v2/getMonitors"
```

5. 构建部署
```bash
pnpm build
# 或
npm run build
```
构建的文件在 `dist` 目录下，将 `dist` 目录部署到服务器即可。

6. 修改后上传

   查看修改状态（可选，但推荐，确认修改内容）：
   ```
   git status # 会显示哪些文件被修改、新增或删除。
   ```
  
   将修改添加到暂存区：
   ```
   git add .  #添加所有修改（包括新增、修改、删除的文件）：
   ```
   提交暂存区的修改到本地仓库：

   ```
   git commit -m "删除站点统计链接，解决打开网页慢问题" 
   ```
   创建版本标签
   ```
   git tag -a v0.0.1 -m "v1.0.0: 初始化站点监测项目"
   ```
   推送标签到远程仓库
   ```
   git push origin v1.0.0
   ```
   推送到远程仓库：
   ```
   git push origin main # 默认分支是 master（旧版本 GitHub 常用）新版 main
   ```

## CDN赞助

本项目 CDN 加速及安全防护由 Tencent EdgeOne 赞助：EdgeOne 提供长期有效的免费套餐，包含不限量的流量和请求，覆盖中国大陆节点，且无任何超额收费，感兴趣的朋友可以去 EdgeOne 官网获取
<a href="https://edgeone.ai/zh?from=github" target="_blank">
    最佳亚洲 CDN、Edge 和安全解决方案 - 腾讯 EdgeOne
<img src="https://edgeone.ai/media/34fe3a45-492d-4ea4-ae5d-ea1087ca7b4b.png" width="500" height="100">
</a>

## 📝 开源协议

本项目基于 [MIT License](LICENSE) 开源，使用时请遵守开源协议。

## 🙏 致谢

- [UptimeRobot](https://uptimerobot.com/) - 提供监控 API 支持
- [Vue.js](https://vuejs.org/) - 前端框架
- [Tailwind CSS](https://tailwindcss.com/) - CSS 框架
- [Chart.js](https://www.chartjs.org/) - 图表库 
- [freejishu美丽世界](https://www.freejishu.com/)  - 提供公益代理服务



