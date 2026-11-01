# 学习日志 03：打通 AI 生成 -> GitHub 仓库 -> 服务器部署全链路

**时间**：2026-10-19——11-01

**任务目标**：使用 AI（Codex/GPT）生成网页代码，并通过 GitHub 仓库和 Git 命令，将网页部署到自己的 Ubuntu 服务器上。

## 💬 我是怎么和 AI 对话的（Prompt）
> “帮我写一个个人主页的 `index.html`，要求蓝粉配色，复古华丽，正中间写‘ Panxi Wang’


## 🛠️ 我的硬核操作过程（Git 联动）
1. **存入仓库**：将 AI 生成的代码在 GitHub 网页端新建为 `index.html` 并提交（Commit）。
2. **解决权限坑**：最初 GitHub 仓库是私有的（Private），服务器无法拉取。我将仓库改为公开（Public）。
3. **服务器拉取**：在服务器终端（OrcaTerm）进入 `/var/www` 目录，删除旧的默认网页文件，使用 `git clone` 命令将 GitHub 仓库完整克隆到服务器。
4. **权限设置**：使用 `chown -R www-data:www-data /var/www/html` 赋予 Nginx 读取网页的权限。

## 💡 我的发现与踩坑
- **踩坑**：一开始在 Windows 本地终端敲了 Linux 命令；后来因为一次性复制了多行命令，导致终端把 `chown` 当成了 GitHub 的用户名报错（SIGINT）。这让我深刻理解了终端必须“一行一行、严格按语法”执行。
- **发现**：原来真正的开发不是把代码复制粘贴进服务器，而是把 GitHub 当作中枢。AI 写代码 -> 推送到 GitHub -> 服务器拉取。以后只要改了 GitHub，在服务器跑一下 `git pull`，网页就自动更新了！这就是自动化的魅力！

## 🖼️ 成果展示
<img width="1802" height="1104" alt="image" src="https://github.com/user-attachments/assets/09aa4589-92d5-4c8c-8ecd-80204915cca7" />


