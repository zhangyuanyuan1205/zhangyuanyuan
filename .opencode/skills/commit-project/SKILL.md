---
name: commit-project
description: 提交并推送当前项目到 Gitee 仓库。当用户说"提交项目"、"commit并push"、"推送到gitee"、"提交代码"、"push到远程"时使用此 skill。
---

# 提交项目到 Gitee

将当前项目通过 git commit 并 push 到 Gitee 远程仓库。

## 远程仓库地址

```
https://gitee.com/zyy18698212531/zhangyuanyuan2026
```

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

### 4. 推送到 Gitee

```bash
git push origin main
```

如果远程分支不是 `main`，则使用实际的分支名。如果推送失败，尝试：

```bash
git push -u origin main
```

### 5. 确认结果

推送成功后，告知用户提交已完成，并提供 Gitee 仓库链接：
```
https://gitee.com/zyy18698212531/zhangyuanyuan2026
```

## 注意事项

- 如果用户明确要求，才执行提交操作
- 不要提交敏感信息（密码、密钥等）
- 确保 `.gitignore` 已正确配置，避免提交不必要的文件
