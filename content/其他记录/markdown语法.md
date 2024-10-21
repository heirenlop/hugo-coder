---
title: "markdwon语法示例"
date: 2024-10-20
draft: false
---

# 1. 插入

## (1). 插入图片

Markdown 的完整图片语法是 ![没图？](/images/ceshi.png "hugo为了测试")

没图？ 用于源码模式和图片未成功加载提示图片用途
/images/ceshi.png 是图片地址，可以是本地的也可以是网络图床
hugo 是图片标题，默认是鼠标悬浮显示

### 图片说明

这是示例图片的说明文字。

## (2). 插入视频

### 使用 HTML 插入视频

你可以使用 HTML 语法插入视频。假设视频存储在 `static/videos` 目录下：

<video controls>
  <source src="/videos/example-video.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

### 视频说明

这是示例视频的说明文字。

## (3). 插入代码块

### Python 代码块

```python
def hello_world():
    print("Hello, world!")
