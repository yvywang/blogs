---
title: Markdown 基本语法
author: yvy
date: 2022-02-28 14:16:58
tags: [Markdown]
---

## 概述

本文将介绍 Markdown 基本使用语法。

<!--more-->

### 标题语法

创建标题时，在单词或短语前添加 `#` 号， `#` 号的数量代表了当前标题的级别，例如, `###` 即表示创建一个三级标题 `<h3 />`

| Markdown                | Html                       | preview                  |
| ----------------------- | -------------------------- | ------------------------ |
| `# Heading level 1`     | `<h1>Heading level 1</h1>` | <h1>Heading level 1</h1> |
| `## Heading level 2`    | `<h2>Heading level 2</h2>` | <h2>Heading level 2</h2> |
| `### Heading level 3`   | `<h3>Heading level 3</h3>` | <h3>Heading level 3</h3> |
| `#### Heading level 4`  | `<h4>Heading level 4</h4>` | <h4>Heading level 4</h4> |
| `##### Heading level 5` | `<h5>Heading level 5</h5>` | <h5>Heading level 5</h5> |

### 强调语法

通过更改文本字体样式来凸显其重点。

#### 粗体 (Bold)

加粗文本有两种方式，在单词或短语的前后各添加两个 `*` 或 `_` 。需要注意的是，`Markdown` 在如何处理单词或短语中间的下划线并不一致，考虑其兼容性，在单词或短语中间部分加粗的话，请使用 `*`。

| Markdown                    | Html                                     | preview                                |
| --------------------------- | ---------------------------------------- | -------------------------------------- |
| `I just test **bold text**` | `I just test <strong>bold text</strong>` | I just test <strong>bold text</strong> |
| `I just test __bold text__` | `I just test <strong>bold text</strong>` | I just test <strong>bold text</strong> |
| `test **bold** text`        | `test <strong>bold</strong> text`        | test <strong>bold</strong> text        |

#### 斜体 (Ltalic)

同上粗体一样写法，区别在于前后只需要一个 `*` 或 `_` 裹住，同建议使用 `*`

### 引用语法

创建块引用，在段落前添加一个 `>` 符号。

```markdown
 > Dorothy followed her through many of the beautiful rooms in her castle.
```
效果如下：
> Dorothy followed her through many of the beautiful rooms in her castle.

#### 多个段落的块引用

块引用可以包含多个段落。 为段落之间的空白行添加 `>` 符号隔开。

```markdown
> Dorothy followed her through many of the beautiful rooms in her castle.
>
> Dorothy followed her through many of the beautiful rooms in her castle.
```
效果如下：
> Dorothy followed her through many of the beautiful rooms in her castle.
>
> Dorothy followed her through many of the beautiful rooms in her castle.

#### 嵌套块引用

块引用可以嵌套。在需要嵌套的段落基于自身的的 `>` 前多加一个 `>`。

```markdown
> Dorothy followed her through many of the beautiful rooms in her castle.
>
>> Dorothy followed her through many of the beautiful rooms in her castle.
```
效果如下：
> Dorothy followed her through many of the beautiful rooms in her castle.
>
>> Dorothy followed her through many of the beautiful rooms in her castle.

### 列表语法

可以将多个条目组织成有序或无序列表。

#### 有序列表

创建有序列表，请在每个列表项前添加数字并紧跟一个英文句点。

#### 无序列表

创建无序列表，在每个列表项前添加 `-`、`*`、`+` 三选一。 缩进一个或多个列表可嵌套列表。

#### 最佳实践

在列表中嵌套其他元素

```markdown
*   This is the first list item.
*   Here's the second list item.

    > A blockquote would look great below the second list item.

*   And here's the third list item.
```
效果如下：
*   This is the first list item.
*   Here's the second list item.

    > A blockquote would look great below the second list item.

*   And here's the third list item.

### 代码预览语法

要将语句以代码风格展示，需要将其包裹 `` ` ``。

例如：
````
```Javascript
const log = 'Hello World'
```
````
效果如下：
```Javascript
const log = 'Hello World'
```

### 分割线

创建分割线，有三种写法，在单独一行上使用多个 `***` 、 `---`、 `___` 三选一，并且分割线当前行不能包含其他内容。
```markdown
***

_______

-------------
```
效果如下：

****

______

-----------

### 链接语法

链接显示的文案放在中括号内，地址放在括号中，title可选。
语法代码：`[文案](地址 "可选title")`
对应HTML代码：`<a href="地址" title="可选title">文案</a>`
```markdown
链接： [blogs](https://yvywang.github.io/blogs/ "hover me")
```

效果如下
链接： [blogs](https://yvywang.github.io/blogs/ "hover me")

#### 网址和Email地址

使用尖括号可以很方便地把URL或者email地址变为可点击的链接。

```
<https://yvywang.github.io/blogs/>
<fake@example.com>
```
效果如下：
<https://yvywang.github.io/blogs/>
<fake@example.com>

#### 带格式化的链接
[强调]() 链接， 在链接语法前后加上 `*`。要将链接表示为代码，在方括号添加 `` ` ``
```markdown
I love supporting the **[EFF](https://eff.org)**.
This is the *[blogs](https://yvywang.github.io/blogs/)*.
See the section on [`code`](#code).
```
I love supporting the **[EFF](https://eff.org)**.
This is the *[blogs](https://yvywang.github.io/blogs/)*.
See the section on [`code`](#code).

### 图片语法

要添加图片的展示，需要使用 `!` , 然后在中括号添加替代文案，图片地址放在圆括号，其后面有可选的title图片标题文案
插入图片的 Markdown 语法：`![图片alt](图片链接 "图片title")`。
对应的 HTML：`<img src="图片链接" alt="图片alt" title="图片title">`

#### 带超链接的图片

给图片增加链接，拥有跳转的特性，在语法外多加一层中括号，最后面多加一个括号填写超链接地址
`[![图片alt](图片链接 "图片title")](https://yvywang.github.io/blogs/)`
