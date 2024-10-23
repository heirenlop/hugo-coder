---
title: "html和css语法"
date: 2024-10-22
draft: false
public: true
categories: ["html","css"]
tags: ["语法"]
---

# 1. css

## 1.1 注释

```css
/* xxxx */
```

## 1.2 新建类选择器

(1) 如新建类选择器.third-class，可以在标签内选择class="third-class"

```css
.third-class {
  }
```
(2) 定义标签hr，定义页面内所有带有hr标签的内容
*tips:定义标签时，无"."*
```css
hr{
}
```

## 1.3 设置类选择器

(1) 以写过的类选择器为例

```css
.third-class {
    /* 设置字体大小 */
    font-size: 18px;
    /* 设置字体颜色 */
    color: darkblue;
    /* 设置字体斜体 */
    font-style: italic;
    /* 设置行缩进 */
    margin-left: 50px;
    /* 字体设置下划线 */
    text-decoration: underline;
    /* 设置字体格式 */
    font-family: '宋体', 'Microsoft YaHei',sans-serif;
}
```
```css
.summary icon {
  /* 调整图标与文本之间的间距 */
  margin-right: 8px; 
  /* 设置图标的颜色 */
  color: #ffdd00; 
}
```
```css
.underline {
    text-decoration: underline;
}

```
(2) 以写过的为例
```css
hr {
    border: none;
    /* 分割线粗细 */
    height: 1px;
    /* 分割线颜色 */
    background-color: #ccc;
    /* 分割线上下边距为20px */
    margin: 20px 0; 
  }
```
## 1.4 css样式配置

新增styles.css文件，路径一般为static/assets/css/路径下，可通过：
```html
<head>
    <link rel="stylesheet" href="/assets/css/styles.css">
</head>
```
引入后，在html中即可使用。

## 1.5 css示例

可参考styles.css文件：[完整示例](../../static/assets/css/styles.css)

# 2. html

## 2.1 注释

```html
<!-- xxx -->
```

## 2.2 标签
```html
(1) 基本结构标签
<!DOCTYPE html>：声明文档类型，告诉浏览器这是一个HTML5文档。
<html>：根元素，包含整个HTML文档的内容。
<head>：包含文档的元数据，如标题、字符集、链接到外部资源等。
<title>：定义文档的标题，显示在浏览器的标签页上。
<body>：包含文档的所有可见内容。
(2) 文本内容标签
<h1> 到 <h6>：标题标签，从最重要的 <h1> 到最不重要的 <h6>。
<p>：段落标签。
<br>：换行标签，不需闭合。
<strong>：加粗文本。
<em>：斜体文本，表示强调。
<span>：用于对文本进行内联样式的容器。
(3) 链接和图像
<a>：超链接标签，用于创建链接。
属性：href（目标URL）、target（目标窗口，如 _blank）。
<img>：图像标签，用于插入图片。
属性：src（图片路径）、alt（替代文本）。
(4) 列表
<ul>：无序列表。
<ol>：有序列表。
<li>：列表项。
(5) 表格
<table>：表格标签。
<tr>：表格行。
<th>：表格头部单元格。
<td>：表格数据单元格。
(6) 表单
<form>：表单标签，用于收集用户输入。
属性：action（提交表单的URL）、method（提交方法，如 get 或 post）。
<input>：输入字段。
类型：text（文本输入）、password（密码输入）、submit（提交按钮）、checkbox（复选框）、radio（单选按钮）等。
<textarea>：多行文本输入。
<label>：标签，用于关联表单控件。
<select>：下拉列表。
<option>：下拉列表中的选项。
(7) 多媒体
<video>：视频标签。
属性：src（视频路径）、controls（显示播放控件）。
<audio>：音频标签。
属性：src（音频路径）、controls（显示播放控件）。
(8) 其他常用标签
<div>：块级容器，用于分组和布局。
<header>：页面或区域的头部。
<footer>：页面或区域的底部。
<nav>：导航链接的集合。
<section>：文档或应用程序中的独立部分。
<article>：独立的内容，如博客文章或新闻。
<aside>：侧栏或辅助内容。
<main>：文档的主要内容。
```

## 2.3 html示例

可参考哈尔滨.md、宁波.md等中html部分：[完整示例](../生活日常/旅行/哈尔滨.md)