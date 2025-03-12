---
title: "Huggingface"
date: 2025-03-12T09:35:33+08:00
draft: false
author: "Yuze Gao"
authorlink: "https://yuzegao.com"
tags: ["HuggingFace"]
categories: ["工具"]
---

Hugging Face 是一个旨在推动自然语言处理（NLP）技术和工具发展的开源社区和公司，提供了一系列优秀的预训练NLP模型，本文介绍如何从Hugging Face的镜像网站下载模型。

## 1.安装

安装必要的包

```shell
pip install transformers
pip install -U huggingface_hub
# 高速下载工具 hf-transfer
pip install -U hf-transfer
```

设置镜像站点`hf-mirror`

```shell
# linux
export HF_ENDPOINT='https://hf-mirror.com'
# windows
$env:HF_ENDPOINT = "https://hf-mirror.com"
```

是否启用`hf-transfer`，可选

```shell
% 启用
export HF_HUB_ENABLE_HF_TRANSFER=1
% 关闭
export HF_HUB_ENABLE_HF_TRANSFER=0
```

## 2.下载

下载模型，`--resume-download`表示在之前基础上下载，后是具体模型，`--local-dir`后是本地目录

```shell
huggingface-cli download --resume-download deepseek-ai/DeepSeek-R1-Distill-Qwen-32B --local-dir deepseek-ai/DeepSeek-R1-Distill-Qwen-32B
```

下载数据，`--resume-download`表示在之前基础上下载，后是数据集，`--local-dir`后边是的是本地目录

```shell
huggingface-cli download --repo-type dataset --resume-download wikitext --local-dir wikitext
```

## 3.参考

1. https://zhuanlan.zhihu.com/p/475260268
2. https://hf-mirror.com/
