<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset=".github/logo-dark.png">
  <img alt="zerolink" src=".github/logo-light.png" width="440">
</picture>

### P2P + 中转 VPN · 跨地域联机 · 规则分流 · L2/L3 虚拟局域网

[![version](https://img.shields.io/badge/version-0.9.125-2563eb?style=flat-square)](https://github.com/Rulinye/zerolink-release/releases/latest)
[![platform](https://img.shields.io/badge/platform-Windows%20%7C%20macOS-64748b?style=flat-square)](#-下载)
[![downloads](https://img.shields.io/github/downloads/Rulinye/zerolink-release/total?style=flat-square&color=16a34a&label=downloads)](https://github.com/Rulinye/zerolink-release/releases/latest)

**[⬇ 下载 Windows](https://github.com/Rulinye/zerolink-release/releases/download/v0.9.125/zerolink-installer_0.9.125_x64.exe)** &nbsp;·&nbsp; **[⬇ 下载 macOS](https://github.com/Rulinye/zerolink-release/releases/download/v0.9.125/zerolink.app.tar.gz)** &nbsp;·&nbsp; [国内镜像 ↓](#-下载)

</div>

---

> [!NOTE]
> **链路命名 = “入口-出口”**，如 `gz-cc` 即入口在 gz、出口在 cc。除非用 `direct` 后缀的链路（直连优化专线，无视地理）。**大陆用户选大陆入口，海外用户选海外入口。**
>
> `gz`广州 · `cc`韩国春川 · `hk`香港 · `seoul`首尔 · `jp`日本 · `sg`新加坡 · `usa`美西 · **`-direct`后缀 = 直连，任意地区可选**
>
> ⚠️ **严禁无端跨地域选择链路，检测封号将不提醒。**

## 目录

- [📥 下载](#-下载)
- [🪟 Windows 安装 / 卸载](#-windows-安装--卸载)
- [🍎 macOS 安装 / 卸载](#-macos-安装--卸载)
- [🧭 规则分流](#-规则分流)
- [🎮 联机房间](#-联机房间)
- [💬 反馈](#-反馈)
- [🗺️ 未来计划](#-未来计划)

---

## 📥 下载

**最新版本 `0.9.125`**，按系统下载一个文件即可：

| 系统 | 直接下载 | 国内镜像（GitHub 慢时用） |
|---|---|---|
| 🪟 **Windows 10 / 11 (64-bit)** | [**zerolink-installer_0.9.125_x64.exe**](https://github.com/Rulinye/zerolink-release/releases/download/v0.9.125/zerolink-installer_0.9.125_x64.exe) | [镜像下载](https://ghfast.top/https://github.com/Rulinye/zerolink-release/releases/download/v0.9.125/zerolink-installer_0.9.125_x64.exe) |
| 🍎 **macOS（Apple Silicon / M 芯片）** | [**zerolink.app.tar.gz**](https://github.com/Rulinye/zerolink-release/releases/download/v0.9.125/zerolink.app.tar.gz) | [镜像下载](https://ghfast.top/https://github.com/Rulinye/zerolink-release/releases/download/v0.9.125/zerolink.app.tar.gz) |

> 💡 装好后客户端会**自动检查更新**，以后有新版应用内一键升级，不用再回来手动下载。
> `.sig` / `latest-*.json` 是自动更新机制用的辅助文件，普通用户忽略。

---

## 🪟 Windows 安装 / 卸载

### 安装

双击下载的 `zerolink-installer_0.9.125_x64.exe` → UAC 弹出点“是” → 安装完成。系统服务在安装时自动注册，无需额外操作。

> - **SmartScreen 提示“未知发布者”**：点“更多信息” → “仍要运行”。我们暂未购买 EV 签名证书。
> - 安装时可能有一两个黑色 cmd 窗口一闪而过，是 Windows 调用命令行工具的标准行为，不影响功能。
> - 如果启动后主页提示“系统组件未安装”（自动注册被杀软拦截等罕见情况），点界面里的“立即安装”按钮 → UAC 确认即可。

### 卸载

- **方式 1**：在安装目录直接运行 `uninstall.exe`（可能出现黑框，耐心等待）。
- **方式 2**：Settings → 应用 → **zerolink** → 卸载（或控制面板“程序和功能”）。

卸载会自动：停止删除 Helper 服务 · 卸载我们装的 TAP-Windows 网卡驱动（不动其他 VPN 的）· 删入站防火墙规则 · 清理安装目录 + 用户数据。

---

## 🍎 macOS 安装 / 卸载

### 安装

1. 下载 `zerolink.app.tar.gz`，在访达里双击解压得到 `zerolink.app`，拖到“应用程序”。
2. 首次启动会弹 macOS 授权框要 sudo 密码，输入即可。系统组件装到 `/Library/PrivilegedHelperTools/` + `/Library/LaunchDaemons/`。

> - **Gatekeeper 提示“无法验证开发者”**：系统设置 → 隐私与安全性 → 找到 zerolink 条目 → “仍要打开”。我们暂未做 Apple notarize。
> - 目前仅支持 **Apple Silicon（M 系列芯片）**。

### 卸载

应用内：**设置 → 完全卸载系统组件**（红色按钮），输入 sudo 密码，然后把 `应用程序/zerolink.app` 拖到废纸篓。

---

## 🧭 规则分流

主页“规则”标签页管理分流配置。每个**配置文件**包含一组规则，可随时切换激活的配置文件。

**默认配置**：内置 `GeoIP-CN` + `GeoSite-CN` —— **中国大陆 IP / 网站直连，境外走代理**。首次启动后无需调整即可用。

| 模式 | 含义 | 适用 |
|---|---|---|
| **规则 (黑名单)** | 默认走代理，命中规则的走直连 | 全局代理，但少数应用要直连（银行、本地服务） |
| **规则 (白名单)** | 默认直连，命中规则的走代理 | 大部分直连，只为特定网站 / 应用走代理 |
| **全局** | 所有流量走代理，忽略规则 | 临时全代理 |

**自定义规则**三字段：**类型**（域名 / 域名后缀 / 关键词 / IP / IP 段）· **值**（如 `example.com`、`192.168.1.0/24`）· **动作**（代理 / 直连 / 阻断）。
例：让 `*.github.com` 走代理 → 加 “域名后缀 = `github.com` → 代理”。

---

## 🎮 联机房间

基于服务器中转的虚拟局域网，房友之间像在同一台路由器下互相访问。用途：LAN 联机游戏、文件共享、内网穿透、远程桌面发现。

| 房间类型 | 说明 | 平台 |
|---|---|---|
| **L3 (默认)** | 三层路由，IP 转发，广播 / 多播由服务器转发 | Windows + macOS |
| **L2** | 真二层桥接，以太网帧 / ARP / 原生广播，支持游戏 LAN 自动发现、Wake-on-LAN | **仅 Windows** |

> 绝大多数场景 L3 够用；只有需要原生广播的局域网游戏才要 L2。

| 联机模式 | 说明 | 适用 |
|---|---|---|
| **中转 (默认)** | 数据走联机节点中继，抗 NAT / DPI，稳定 | 大多数情况 |
| **直连** | 尝试 P2P 直连，延迟更低 | 双方 NAT 友好，追求最低延迟 |

**Broker 路径**（控制信道，只影响你自己）：**直连 broker（默认）** 延迟最低 · **中转 broker** 绕一跳，适合直连受阻的网络。

---

## 💬 反馈

应用内：**设置 → 反馈** 写问题或建议，提交后管理员后台收到。建议附：系统版本（Win 10/11、macOS 14.x）· 客户端版本（主页底部）· 复现步骤 / 错误截图。

也可来 [Issues](https://github.com/Rulinye/zerolink-release/issues) 提交。

---

## 🗺️ 未来计划

- **iOS 端**：暂无计划。
- **Android 端**：暂无计划。

<div align="center"><sub>∞ zerolink</sub></div>
