---
title: vscode的插件Todo-Tree
date: 2020-04-07 14:05:15
tags: 记录
categories: 工具
---

发现一个很好用的vscode插件记录一下。
[Todo-Tree](https://marketplace.visualstudio.com/items?itemName=Gruntfuggly.todo-tree)可以很方便得找到标记的位置（通过侧边栏的树形图标显示文件列表），高亮标记位置（可以配置不同的tags名称，并自定义颜色）。

这是我的配置：

```json
   // settings.json
    "todo-tree.general.tags": ["TODO:", "FIXME:", "BUG:"],
    "todo-tree.highlights.defaultHighlight": {
        "type": "text-and-comment",
        "gutterIcon": true,
    },
    "todo-tree.highlights.customHighlight": {
        "TODO:": {
            "foreground": "#FFFFFF",
            "background": "#FFBD2A",
            "iconColour": "#FFBD2A"
        },
        "FIXME:": {
            "foreground": "#fff",
            "background": "#f06292",
            "icon": "flame",
            "iconColour": "#f06292"
        },
        "BUG:": {
            "foreground": "#fff",
            "background": "#be0707",
            "icon": "bug",
            "iconColour": "#be0707"
        }
    },
```

效果：

![](/images/result.png)

