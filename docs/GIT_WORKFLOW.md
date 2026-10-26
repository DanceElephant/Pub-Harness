# Git 使用说明

## 已配置的连接

- GitHub 账户：`DanceElephant`
- 远端仓库：`DanceElephant/Pub-Harness`
- 连接方式：HTTPS，由官方 GitHub CLI 提供凭据
- 主分支：`main`
- 本仓库的提交邮箱：GitHub 提供的 noreply 邮箱

仓库目前公开。选择上传文件时，请检查其中的个人资料。

## 常用命令

在项目目录的终端执行：

```sh
# 查看改动
git st
git diff

# 只暂存选定文件，然后检查本次提交内容
git add -- README.md docs/GIT_WORKFLOW.md
git diff --cached
git commit -m "说明本次完成的工作"

# 上传当前分支；第一次推送会自动建立跟踪关系
git push

# 获取远端更新；发生分叉时停下，先决定如何处理
git pull --ff-only

# 查看最近的提交
git lg
git last

# 创建工作分支
git switch -c codex/my-change

# 将文件从暂存区移出，保留文件内容
git unstage -- README.md

# 查看 GitHub 登录状态与仓库信息
gh auth status
gh repo view
```

也可以直接用中文描述要保存哪些文件，让 Codex 完成检查、提交和推送。

## 本机工具与配置

配置日期：2026-10-26。

- Git 2.56.0：使用官方源码与公布的 SHA-256 校验值，在本机编译安装到 `~/.local/share/git/2.56.0/`。
- GitHub CLI 2.103.2：使用官方 macOS ARM64 发布包并核验 SHA-256，安装到 `~/.local/share/github-cli/`。
- 两个工具的入口位于 `~/.local/bin/`，已在 Zsh 配置中优先使用。已有终端窗口可重新打开以加载新配置。
- `/opt/homebrew/bin/` 中也已创建指向上述工具的链接，让当前运行中的桌面环境立即使用新版。
- GitHub 登录凭据保存在 macOS 钥匙串中。
- 全局默认值：新仓库使用 `main`；拉取仅允许快进；获取时清理已删除的远端分支引用；普通推送采用 `simple` 并自动建立上游；中文文件名正常显示。
- 快捷命令：`git st`、`git lg`、`git last`、`git unstage`。
- 配置备份位于 `~/.config/codex-git/backups/`。
- 本机现有个人文件的排除规则位于 `.git/info/exclude`，该文件不会上传。

## 将来使用其他仓库

```sh
gh repo clone OWNER/REPOSITORY
cd REPOSITORY
git st
```

在 Codex 中打开对应的本地目录后，可继续用同样的中文请求操作 Git。

## 重新连接

```sh
gh auth status
# 仅在登录失效时执行，并在浏览器核对授权账户
gh auth login --hostname github.com --git-protocol https --web
gh auth setup-git --hostname github.com
```

若要解除这台机器的命令行登录，可运行 `gh auth logout --hostname github.com`；也可以在 GitHub 的应用授权设置中撤销 GitHub CLI 授权。
