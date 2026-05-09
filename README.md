# 0-0link

代理 + 虚拟局域网一体化客户端。本仓库托管编译好的安装包。

## 下载

去 [Releases](https://github.com/Rulinye/0-0_release/releases/latest) 找最新版本。

按系统选一个文件下:

| 系统 | 文件 |
|---|---|
| **Windows 10/11 (64-bit)** | `0-0link_X.Y.Z_x64_zh-CN.msi` |
| **macOS (Intel + Apple Silicon)** | `0-0link_X.Y.Z_universal.dmg` |

其它 `.sig` / `.app.tar.gz` / `latest-*.json` 是给应用内自动更新机制用的,普通用户不用管。

## Windows 安装

**默认路径** (推荐): 双击 `.msi`,跟着提示走,点"是"通过 UAC 提权。装完启动应用即可,系统服务会在安装时一起装好。

**自定义路径**: 管理员 PowerShell 跑:
```powershell
msiexec /i 0-0link_X.Y.Z_x64_zh-CN.msi INSTALLDIR=D:\你的路径
```

> SmartScreen 弹"未知发布者"警告: 我们暂时还没买 EV 签名证书。点"更多信息" → "仍要运行"。
> 
> 安装时会有 1~2 个黑色 cmd 窗口一闪而过,这是 Windows MSI 的限制(install-helper 是命令行程序),不影响功能。

### 自动更新

应用首次启动后会自动检查更新。新版本会从 Releases 拉,弹横幅提示你去 设置 → 检查更新 手动确认安装。

### 万一系统服务没自动装上

启动应用后如果显示"系统组件未安装",点界面里的"立即安装"按钮 → UAC 确认 → 应该就装上了。这是兜底路径。

## Windows 卸载

**Settings → 应用 → 0-0link → 卸载**(或控制面板"程序和功能")。会:
- 停掉助手服务并删除注册
- 卸载 TAP 网卡驱动(我们装的那张,不动你别的 VPN 软件的)
- 删防火墙规则
- 删 `C:\Program Files\0-0link\`(或你自定义路径)
- 删用户 AppData

## macOS 安装

1. 双击 `.dmg`,把 0-0link 拖到"应用程序"。
2. 首次启动时会弹 macOS 授权窗口要 `sudo` 密码,输入后系统组件会装到 `/Library/PrivilegedHelperTools/` 和 `/Library/LaunchDaemons/`。

> Gatekeeper 弹"无法验证开发者": 我们暂时未做 Apple notarize。 系统设置 → 隐私与安全性 → 找到 0-0link → 点"仍要打开"。

## macOS 卸载

应用内: **设置 → 完全卸载系统组件**(红色按钮),输入 sudo 密码,然后把 `应用程序/0-0link.app` 拖到废纸篓即可。

## 常见问题

**Q: 装完启动应用,主页面顶部显示"系统组件未安装"。**

A: 点页面里的"立即安装"按钮,UAC 确认。一般是 .msi 安装时的自动注册被杀软拦了或时机赶不上。

**Q: VPN 连上但访问外网走不通。**

A: 先看主页"实时速度"是否有数据流。如果有但应用打不开网页,可能是 DNS/规则配置问题,去"规则"页检查激活的配置文件。如果完全没数据,看"系统组件"状态。

**Q: 想换安装目录,怎么搞?**

A: Win 用 `msiexec /i ... INSTALLDIR=新路径`(参考上面)。Mac 路径固定 `/Applications/`,移动后重新启动即可。

**Q: 用户名/密码框打不出中文。**

A: 这是有意设计 — 用户名密码限定 ASCII 防止误输入。其它字段(房间名、规则配置名、反馈正文等)中文正常。

## 反馈 / 报 bug

去 [Issues](https://github.com/Rulinye/0-0_release/issues)。粘贴:
- 系统版本(Win 10/11/22H2 之类、mac 14.x 之类)
- 客户端版本(主页底部)
- 复现步骤
- 错误截图或日志

Win 日志位置: `%LOCALAPPDATA%\com.rulinye.zerolink\` 和 `%LOCALAPPDATA%\0-0link\`。
Mac 日志位置: `/var/log/com.rulinye.zerolink.helper.log`(系统组件)。
