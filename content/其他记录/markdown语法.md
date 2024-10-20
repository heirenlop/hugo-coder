---
title: "markdwon语法示例"
date: 2024-10-20
draft: false
---

# 1. 插入
## (1). 插入图片

你可以使用 Markdown 语法插入图片。假设图片存储在 `static/images` 目录下：

![没图？](/images/ceshi.png)

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