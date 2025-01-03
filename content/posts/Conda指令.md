---
title: "Conda指令"
date: 2025-01-03T09:36:50+08:00
draft: false
author: "Yuze Gao"
authorlink: "https://yuzegao.com"
tags: ["Conda"]
categories: ["工具"]
---

## 安装指南

从清华镜像站下载安装anaconda，地址为：https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/

将安装源换为清华源，将~/.condarc内容替换，参考：https://mirrors.tuna.tsinghua.edu.cn/help/anaconda/ 

## conda指令

conda管理， 主要包括信息查看，版本管理

```bash
# 查看版本 测试是否安装成功
conda --version
# 查看更多信息
conda info

# 更新conda至最新版本
conda update conda
# 更新conda后可以更新所有包
conda update -all

# 
conda clean -i
```

conda环境管理，主要包括环境的创建，查看，切换等操作

```bash
# 创建环境，环境在conda目录中env/下, 可指定python版本
conda create -n envname
conda create -n envname python=3.9
# 查看已创建环境
conda info -e

# 切换环境
conda activate envname
# 返回上一个环境
conda deactivate

# 给虚拟环境安装包，也可以在conda activate env后直接 conda install scipy
conda install -n envname scipy

# 克隆环境，新环境：clone_env
conda create --name clone_env --clone envname
# 删除环境
conda remove -n envname --all
```

conda包管理，主要包括包的安装，删除，更新等。

```bash
# 当前环境安装包
conda install numpy
# 安装包
conda install -n envname numpy

# 更新包，也可以在conda activate env后直接conda update numpy
conda update -n envname numpy

# 删除包，也可以在conda activate env后直接conda remove numpy
conda remove -n envname numpy

# 查看包
conda list -n envname
```

分享环境：通过env.yml文件分享

```bash
#创建.yml文件
conda env export > environment.yml
#通过.yml文件还原环境
conda env create -f environment.yml
```

## 参考

1. https://zhuanlan.zhihu.com/p/87123943
2. https://zhuanlan.zhihu.com/p/57287956
