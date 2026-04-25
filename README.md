# BidPilot Releases

**BidPilot 标审通 · 分发版 · 测试开发期**

本仓库**只承载** BidPilot 标审通的 Windows 安装包发布 · **不包含源代码**。

---

## 下载

前往 [Releases](https://github.com/709411fan/bidpilot-releases/releases) 页面下载最新版 installer。

每个 release 包含：

- `BidPilotSetup-vX.Y.Z-alpha.N.exe` · Windows 安装包
- `SHA256SUMS.txt` · 校验文件（SHA256）
- release notes · 版本说明

最新版直链（release 发布后生效）：
`https://github.com/709411fan/bidpilot-releases/releases/latest/download/BidPilotSetup-vX.Y.Z-alpha.N.exe`

---

## 📖 安装指南

→ **[Windows 安装指南](docs/install-windows.md)**（适用于 alpha 测试开发版 · 受邀测试用户）

包含：系统要求 / 下载入口 / 安装步骤 / SmartScreen 处理 / 杀毒误报 / 本地服务验证 / 常见问题 / 卸载。

---

## 仓库内容边界（硬纪律）

本仓库**仅允许**存放：

- ✅ installer `.exe` 产物
- ✅ `SHA256SUMS.txt` 校验文件
- ✅ `docs/install-windows.md` 安装指南
- ✅ release notes

本仓库**严禁**存放：

- 🚫 源码
- 🚫 `.env` 任何配置文件
- 🚫 私钥 · 证书
- 🚫 内部 spec · 架构文档
- 🚫 开发脚本 · CI 配置
- 🚫 测试代码

每次 push 前应检查 `git diff --name-only origin/main` 不包含上述禁止项。

---

## 主仓库

BidPilot 主仓库（源码 + 开发）为内部访问 · 本仓库不提供源码下载。

---

## 当前状态

⚠️ **测试开发期** · 首个 installer release（`v0.1.0-alpha.1`）尚未发布 · 本仓库目前仅含 installer 占位（**安装指南 docs/install-windows.md 已就绪 · Sprint I-A B7 中等版**）。

---

## 反馈

产品问题或安装问题：15232252222@163.com

---

**版权所有 © 上海智源工坊信息科技有限公司**
