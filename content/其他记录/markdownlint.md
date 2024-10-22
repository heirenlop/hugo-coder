---
title: "markdwonlint的json修改"
date: 2024-10-21
draft: false
public: true
categories: ["markdown"]
tags: ["lint"]
---

1. 取消html的标签报警告问题
   在markdownlint:config中设置setting.json的markdownlint.config。
   ```python
    "markdownlint.config": {
        "default": true,
        "MD033": {
          "allowed_elements": [ "font", "li", "table", "tr", "td" ,"ul","strong","summary","details"]
        }
    }
    ```
    需要什么html的标签取消警告，就把标签名放到MDO33中。
