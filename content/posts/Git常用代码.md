---
title: "Git常用代码"
date: 2025-04-27T16:22:15+08:00
draft: false
author: "Yuze Gao"
authorlink: "https://yuzegao.com"
tags: ["Git"]
categories: ["工具"]
---

Git 是一个分布式版本控制系统，用于跟踪文件的变化，特别是在开发过程中对源代码的管理。

## 1.配置用户名和邮箱

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

#查看配置
git config --list
```

## 2.配置ssh

生成SSH密钥，SSH公钥在 `~/.ssh` 目录下，生成密钥后，将`~/.ssh/id_rsa.pub`添加到远程GitHub中SSH Keys中。

```bash
# 生成SSH密钥对
# -t rsa: 使用 RSA 算法。
# -b 4096: 设置密钥长度为 4096 位（更强的加密）。
# -C "your_email@example.com": 设置密钥的注释，通常使用你的邮箱。
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

# 3.仓库与文件操作

```bash
# 初始化仓库
git init
# 克隆仓库
git clone <repository_url>

# 添加文件
git add <file_name>      # 添加单个文件
git add .                # 添加当前目录下所有文件
# 删除文件
git rm <file_name>

#提交文件到本地仓库
git commit -m "Your commit message"

# 从远程仓库拉取代码
git pull origin <branch_name>
# 推送代码到远程仓库
git push origin <branch_name>
```

# 4.分支操作

```bash
# 创建新分支
git branch <branch_name>
# 切换到另一个分支
git checkout <branch_name>
# 创建并切换到新分支
git checkout -b <branch_name>
# 查看分支
git branch

# 删除分支 
git branch -d <branch_name>  # 删除本地分支
git push origin --delete <branch_name>  # 删除远程分支

# 合并
git merge <branch_name>
```

