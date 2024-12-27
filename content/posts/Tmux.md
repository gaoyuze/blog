---
title: "Tmux"
date: 2024-12-27T10:25:56+08:00
draft: false
author: "Yuze Gao"
authorlink: "https://yuzegao.com"
tags: ["Tmux"]
categories: ["工具"]
---

Tmux是会话与端口解绑工具，可以关闭窗口后不中止会话，继续运行。

## 1.安装

```bash
sudo apt-get install tmux
```

## 2.使用方法

主要包括新建、查看、分离、关闭等常见操作。

```bash
# 启动
tmux
# 退出
exit 或者 Ctrl+d

# 新建会话
tmux new -s <name>
# 查看会话
tmux ls
# 接入会话 
tmux attach -t 0  或者 tmux a -t 0
# 分离会话：退出窗口，会话和进程仍然在执行
tmux detach
# 杀死会话（编号和名称都可以）
tmux kill-session -t 0
# 切换会话
tmux switch -t 0 
# 重命名
tmux rename-session -t 0 <new-name>

# 进入tmux后可以进行分屏
# 上下分屏
tmux split-window
# 左右分屏
tmux split-window -h

# 关闭服务器，杀死所有会话
tmux kill-server

```

## 3.常用快捷键

```bash
Ctrl+b d：分离当前会话（会话任然存在）
Ctrl+b x：关闭当前窗格（关闭会话）
Ctrl+b s：列出所有会话 并进行切换
Ctrl+b %：划分左右两个面板
Ctrl+b "：划分上下两个面板
Ctrl+b z：最大化当前面板
Ctrl+b 方向键：选择面板
```

## 4.参考

1. https://louiszhai.github.io/2017/09/30/tmux/
2. https://www.ruanyifeng.com/blog/2019/10/tmux.html
