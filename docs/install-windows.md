# BidPilot 安装指南 · Windows

> ✅ **Sprint I-A B7 正式版（覆盖 B0 占位 · 2026-04-25）**

**适用版本**：v0.1.0-alpha.1
**面向**：alpha 测试开发版 · 受邀测试用户

---

## 适用范围

- **操作系统**：Windows 10（1507+ / Build 10240+）/ Windows 11 · 64 位
- **依赖软件**：WPS Office 2019+（专业版 / 校园版 / 个人免费版均可）
- **网络**：下载、登录、AI 调用等功能需要联网；本地服务首次启动会加载本地模型，可能需要 30-60 秒
- **磁盘空间**：建议预留 2 GB
- **当前版本性质**：**alpha 测试开发版** · 仅用于端到端流程验证 · 暂未做代码签名 · 受邀测试用户使用

---

## 下载

有两种方式：

### 方式一：从官网"我的账户"下载（如果该入口已上线）

1. 登录 [intelgenai.com](https://intelgenai.com/login)
2. 进入"我的账户"页面
3. 点击「下载插件开始使用」 → 「下载 Windows 安装包」

### 方式二：从 GitHub Releases 下载（备用入口）

直接访问：

```
https://github.com/709411fan/bidpilot-releases/releases/latest
```

下载最新的 `BidPilotSetup-v0.1.0-alpha.1.exe`（约 200-300 MB · 含 AI 模型）。

**校验文件完整性**（可选）：

同时下载 `SHA256SUMS.txt` · 用 PowerShell 校验：

```powershell
Get-FileHash BidPilotSetup-v0.1.0-alpha.1.exe -Algorithm SHA256
```

输出的 hash 应与 `SHA256SUMS.txt` 内的 hash 一致。

---

## 安装步骤

### 1. 关闭 WPS Office

> ⚠️ 安装时如果 WPS 正在运行 · installer 会弹窗提示关闭。建议预先保存所有 WPS 文档并关闭。

### 2. 双击 `BidPilotSetup-v0.1.0-alpha.1.exe`

如出现 SmartScreen 警告 → 见下方 [SmartScreen 处理](#smartscreen-处理) 段。
如出现杀毒软件提示 → 见下方 [杀毒误报处理](#杀毒误报处理) 段。

### 3. 按向导完成安装

- 默认安装目录：`%LOCALAPPDATA%\BidPilot\`（用户级安装 · 无需管理员）
- WPS 插件自动注册到：`%APPDATA%\kingsoft\wps\jsaddons\biaoshentong_3.0.0\`
- 桌面会创建快捷方式「启动标审通本地服务」

### 4. 启动本地服务

双击桌面快捷方式 **「启动标审通本地服务」**。

> ⚠️ **首次启动需要 30-60 秒**（加载本地 AI 模型）· 请耐心等待。

可通过以下方式验证服务已启动 → 见下方 [本地服务验证](#本地服务验证) 段。

### 5. 重新打开 WPS Office

> ⚠️ 必须先**完全关闭** WPS（含 wps.exe / wpp.exe / et.exe 所有进程）· 再重新打开。WPS 启动时才会加载新注册的插件。

### 6. 找到「标审通」选项卡

打开 WPS Writer 任意文档 · 在顶部菜单栏找到 **「标审通」选项卡** → 点击任意按钮 → 右侧弹出 TaskPane 插件面板。

✅ 看到面板 = 安装成功。

---

## SmartScreen 处理

双击 installer 时如出现：

> Windows 已保护你的电脑
> Microsoft Defender SmartScreen 已阻止启动一个无法识别的应用。
> 发布者：未知发布者

这是因为当前 alpha 测试版**未做代码签名证书**（正式版会做）。

**如果你信任本次测试来源**（例如从官方邮件 / 官方测试邀请获得安装包），可以：

1. 点击窗口中的 **「更多信息」**
2. 出现 **「仍要运行」** 按钮 → 点击继续

> ⚠️ **不建议**从非官方链接、非官方测试邀请、第三方下载站下载或运行此安装包。如果你不确定来源，请联系反馈邮箱确认。

---

## 杀毒误报处理

部分杀毒软件（360 / 火绒 / Windows Defender 等）可能误报 installer 或 `bidpilot_core.exe` 为可疑文件。原因：

- installer 未做代码签名（alpha 阶段）
- `bidpilot_core.exe` 是 PyInstaller 打包的本地服务 · 启动时会监听本地端口 :3891 · 部分杀毒会误识别为后台进程

**如果你信任本次测试来源**，可以：

1. 在杀毒软件中将 `%LOCALAPPDATA%\BidPilot\bin\` 整目录加入白名单
2. 或对单个文件 `bidpilot_core.exe` 加白名单

> ⚠️ **不建议**为运行测试软件而临时关闭整个杀毒软件 · 也不建议从非官方链接下载安装包。

---

## 本地服务验证

启动「标审通本地服务」后 · 可通过以下任一方式验证服务已运行：

### 方式一：浏览器（推荐普通用户使用）

打开浏览器 · 访问：

```
http://127.0.0.1:3891/
```

返回 HTML 页面（标审通前端界面）= 服务已就绪。

### 方式二：任务管理器

按 `Ctrl + Shift + Esc` 打开任务管理器 · 在「进程」标签页找到：

- `bidpilot_core.exe`（主进程）

存在 = 服务已运行。

### 方式三：命令行（可选 · 高级用户）

```cmd
curl http://127.0.0.1:3891/
```

返回 HTML 内容 = 服务已就绪。

> ⚠️ 首次启动需 30-60 秒加载 AI 模型 · 等服务完全就绪后再打开 WPS。

---

## 常见问题

### Q1：WPS 中看不到「标审通」选项卡？

逐项检查：

1. **WPS 已完全关闭并重新打开**（含 wps.exe / wpp.exe / et.exe 所有进程 · 必要时重启电脑）
2. **本地服务已启动**（双击桌面"启动标审通本地服务"快捷方式 · 等 30-60 秒）
3. **WPS 版本符合要求**（2019+）
4. 检查 `%APPDATA%\kingsoft\wps\jsaddons\biaoshentong_3.0.0\` 目录是否存在

如全部正确仍看不到 · 联系反馈邮箱。

### Q2：点击「标审通」选项卡按钮后 TaskPane 没反应？

通常是本地服务未启动或未就绪：

- 检查任务管理器有无 `bidpilot_core.exe` 进程
- 浏览器访问 `http://127.0.0.1:3891/` 看是否返回页面
- 首次启动等够 30-60 秒（AI 模型加载）

### Q3：下载链接打开 404？

可能是 release 还未发布。请：

- 访问 [bidpilot-releases](https://github.com/709411fan/bidpilot-releases/releases) 确认是否有 latest release
- 联系反馈邮箱确认当前 alpha 版本号

### Q4：Windows 提示「未知发布者」？

是 SmartScreen 对未签名 installer 的正常提示 · 见 [SmartScreen 处理](#smartscreen-处理) 段。

### Q5：杀毒软件拦截 installer 或 bidpilot_core.exe？

是杀毒软件对未签名本地服务的常见误报 · 见 [杀毒误报处理](#杀毒误报处理) 段。

### Q6：怎么卸载？

见下方 [卸载](#卸载) 段。

---

## 卸载

### 卸载步骤

1. **Windows 设置**：开始菜单 → 设置 → 应用 → 已安装应用 → 找到「标审通」→ 卸载
2. **或控制面板**：控制面板 → 程序 → 程序和功能 → 找到「标审通」→ 卸载
3. **或开始菜单快捷方式**：开始菜单 → 标审通 → 卸载标审通

### 卸载时的用户数据询问

卸载向导会弹出对话框：

> 是否同时删除本地用户数据？
> 路径：%APPDATA%\BidPilot\user_data
> 包含：本地 SQLite 数据库 / 知识库索引 / 上传文件 / 生成历史 / 日志
> 建议保留以便重装后继续使用。
> 点「是」清除数据。
> 点「否」保留所有数据。

**默认建议保留**（点「否」）· 重新安装后可以继续使用历史数据。

### 彻底清理（如需）

如果卸载时选了「否」保留 · 但后续想彻底清理 · 可手工删除：

```
%APPDATA%\BidPilot\user_data\
```

> ⚠️ **不要**手工删除 `%APPDATA%\kingsoft\wps\jsaddons\biaoshentong_3.0.0\`（卸载向导会自动处理）· 也**不要**手工编辑 `%APPDATA%\kingsoft\wps\jsaddons\publish.xml`（除非你知道在做什么）。

---

## 反馈渠道

- **测试反馈邮箱**：15232252222@163.com（过渡邮箱 · 后续启用 sales@intelgenai.com）
- **问题报告**：邮件附上：
  - Windows 版本（Win + R 输入 `winver`）
  - WPS Office 版本（WPS 顶部 → 关于）
  - 出错截图或错误描述
  - 安装日志（如有 · 一般在 `%LOCALAPPDATA%\BidPilot\bin\` 下）

---

🟢 **本指南 · alpha 测试开发版 v0.1.0-alpha.1 · Sprint I-A B7 (2026-04-25)**
