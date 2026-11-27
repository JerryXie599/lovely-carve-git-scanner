# LovelyCarve Git 仓库扫描与取证分析插件

插件 ID：`org.forensicflow.collector`（LPP v2，`v0.3.0`）

> 本仓库仅提供面向 **LovelyCarve** 的 Release `.lcpkg` 二进制插件包发布与使用说明，不包含源码。

## 下载与安装

请前往本仓库 **[Releases](../../releases)** 页面下载最新版本的 `org.forensicflow.collector-0.3.0-windows-x64.lcpkg`。

### 安装方式

- **图形界面**：打开 LovelyCarve → **「设置 → 插件 → 安装 .lcpkg」**，选择下载的 `.lcpkg` 文件。
- **命令行**：
  ```bash
  lovelycarve-cli plugin install org.forensicflow.collector-0.3.0-windows-x64.lcpkg
  ```

## 核心能力

### 1. 全盘 Git / GitHub 仓库递归扫描（`git_forensics`）
自动递归扫描整份检材中的 `**/.git/HEAD`、`config`、`logs/HEAD`、`packed-refs`、`index`（也支持通过 `repo_path` 指定单个仓库路径），并在左侧 **「工具 → Git 仓库」** 注册快捷入口，支持按需勾选分析子项：
- **仓库概览与 GitHub 远程凭据（`.git/config`）**：提取仓库路径、Remote URL、分支配置与嵌入凭据/Token 线索；
- **提交历史（Commit History — Loose & Pack）**：直接解析松散对象与 Packfile 提交记录；
- **回滚、重置与分支变更操作（`.git/logs` Reflog）**：还原 `reset`、`checkout`、`rebase`、`commit --amend` 等操作轨迹；
- **回滚残留对象与敏感数据恢复（Dangling & Secrets）**：扫描孤立/悬空对象并提取潜在敏感凭据；
- **暂存区工作树文件清单（`.git/index`）**：解析 Git 索引文件记录与时间戳。

### 2. 单仓库文件级解析（`git_forensics_files`）
在文件列表中右键选中 `.git/config`、`HEAD`、`index` 等文件时，按需触发单个仓库的取证解析。

### 3. 自定义文件清单收集（`collect`）
按用户可编辑的 JSON 规则把散落在检材各处的文件聚合成清单记录（每行支持源文件定位与跳转预览）：
- Windows 默认配置路径：`%APPDATA%\app.lovelycarve\collector\collectors.json`（首次运行自动生成模板，可用 `LC_COLLECTOR_CONFIG` 环境变量覆盖）。
