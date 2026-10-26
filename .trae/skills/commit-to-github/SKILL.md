---
name: commit-to-github
description: 提交并推送当前项目到 GitHub 远程仓库。当用户说"提交到github"、"push到github"、"提交代码到github"时使用此 skill。推送到 Gitee 时不要使用本 skill。
---

# 提交项目到 GitHub

将当前项目通过 git commit 并 push 到 GitHub 远程仓库。

## 远程仓库地址（SSH，已配置公钥）

```
ssh://git@ssh.github.com:443/zhangyuanyuan1205/zhangyuanyuan.git
```

- 使用 GitHub 官方 443 端口 SSH 通道（等效于 `git@github.com:zhangyuanyuan1205/zhangyuanyuan.git`），因为当前环境可能屏蔽 22 端口
- 远程名称使用 `github`（`origin` 已被 Gitee 仓库占用，不要覆盖 `origin`）
- 仓库主页：`https://github.com/zhangyuanyuan1205/zhangyuanyuan`

## 操作步骤

### 1. 检查当前状态

```bash
git status
git diff --staged
git log --oneline -5
```

### 2. 暂存文件

- **仅暂存已修改的文件**，不要使用 `git add .` 或 `git add -A`
- 根据 `git status` 的输出，逐个添加需要提交的文件：
  ```bash
  git add <file1> <file2> ...
  ```
- 不要提交未暂存的文件

### 3. 提交

- 检查最近 5 条 commit 的语言风格：
  ```bash
  git log --oneline -5
  ```
- 如果最近 5 条 commit 使用中文，则使用中文提交信息；否则使用英文
- 提交信息应简洁明了，描述本次变更内容
- **禁止**在提交信息中添加任何 `🤖 Generated with Claude Code` 或 `Co-Authored-By` 相关内容

```bash
git commit -m "提交信息"
```

### 4. 配置远程仓库

先检查是否已存在名为 `github` 的远程：

```bash
git remote -v
```

如果没有，则添加：

```bash
git remote add github ssh://git@ssh.github.com:443/zhangyuanyuan1205/zhangyuanyuan.git
```

如果已存在但地址不是 443 端口通道，则更新：

```bash
git remote set-url github ssh://git@ssh.github.com:443/zhangyuanyuan1205/zhangyuanyuan.git
```

### 5. 推送到 GitHub

```bash
git push github master
```

如果当前分支不是 `master`，则使用实际的分支名。如果推送失败，尝试：

```bash
git push -u github master
```

#### 推送失败排查

- 报 `Connection refused`（22 端口被屏蔽）：确认远程地址使用的是 `ssh://git@ssh.github.com:443/...`
- 报 `Host key verification failed`：先执行一次以下命令接受主机密钥（需能写 `~/.ssh/known_hosts`）：
  ```bash
  ssh -T -o BatchMode=yes -o StrictHostKeyChecking=accept-new -p 443 git@ssh.github.com
  ```
- 认证成功标志是输出 `Hi zhangyuanyuan1205!`

### 6. 确认结果

推送成功后，告知用户提交已完成，并提供 GitHub 仓库链接：

```
https://github.com/zhangyuanyuan1205/zhangyuanyuan
```

## 注意事项

- 如果用户明确要求，才执行提交操作
- 不要提交敏感信息（密码、密钥等）
- 确保 `.gitignore` 已正确配置，避免提交不必要的文件
- 不要修改或删除指向 Gitee 的 `origin` 远程
