---
title: Markdown 扩展语法
date: 2022-03-03 14:33:29
author: Yu
toc: true
cover: https://cdn.jsdelivr.net/gh/yvywang/figure-bed@main/img/202203091534863.png
tags: [Markdown]
categories: [Markdown, advanced]
---

## 概述

基本语法主要是为了应付大多数情况下的日常所需元素，但对于个别人群来说还不够，这就是扩展语法的用武之地，本文将介绍它的使用。

<!-- more -->

## 表格

要添加表请使用三个或以上连字符 `---` 创建每列的标题，并使用管道 `｜` 分隔每列。您可以选择在表的任一端添加管道。

```Markdown
| Syntax    | Description |
| --------- | ----------- |
| Header    | Title       |
| Paragraph | Text        |
```

输出如下：

| Syntax    | Description |
| --------- | ----------- |
| Header    | Title       |
| Paragraph | Text        |

### 对齐

标题行的连字符 左侧，右侧，两侧 中添加冒号 `:` ，将列中的文本对齐到 左侧， 右侧， 或居中。

```Markdown
| Syntax    | Description |   Test Text |
| :-------- | :---------: | ----------: |
| Header    |    Title    | Here's this |
| Paragraph |    Text     |    And more |
```

 输出如下：
 
 | Syntax    | Description |   Test Text |
 | :-------- | :---------: | ----------: |
 | Header    |    Title    | Here's this |
 | Paragraph |    Text     |    And more |


**Tip:** 使用连字符和管道创建表可能很麻烦，为了高效可以尝试使用 [Markdown Tables Generator]([http://127](https://www.tablesgenerator.com/markdown_tables))。
使用图形界面构建表，填充内容后生成 Markdown 格式的文本复制到文件中。


## 围栏代码块

Markdown基本语法允许您使用一个制表符来创建代码块。如果发现不方便，请尝试使用受保护的代码块。根据 Markdown处理器或编辑器的不同，您将在代码块之前和之后的行上使用三个反引号 `` ``` `` 或三个波浪号 `~~~` 。

````Markdown
```
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```
````

输出如下:

```
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```

**Tip:** 要在代码块展示特殊符号，请参阅了解如何转义它们。

### 语法高亮

许多Markdown处理器都支持受围栏代码块的语法突出显示。使用此功能，您可以为编写代码的任何语言添加颜色突出显示。要添加语法突出显示，请在受防护的代码块之前的反引号旁边指定一种语言。

````Markdown
```json
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```
````

输出如下:

```json
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```

## 脚注

脚注可以让你添加注释和参考，而不会使文档正文混乱。当您创建脚注时，带有脚注的上标数字会出现在您添加脚注参考的位置。读者可以单击链接以跳至脚注内容区域。

要创建脚注参考，请在语句中插入 `[^1]` 标识符。这里的 `1` 就是标识符，标识符可以是数字或单词。脚注按顺序编号。

使用冒号和文本 `[^1]: my text` 来添加你脚注参考的内容。 不必在文档末尾添加脚注，可以将它们放在除了列表，块引号，表之类的其他元素之外的任何位置。

```Markdown
Here's a simple footnote,[^1] and here's a longer one.[^bignote]

[^1]: This is the first footnote.
[^bignote]: Here's one with multiple paragraphs and code.

    Indent paragraphs to include them in the footnote.

    `{ my code }`

    Add as many paragraphs as you like.

```
## 标题编号

有时候我们想要点击一个关键词，跳到对应的内容区域查看，定义标题编号后使用 Markdown的链接语法可以实现这个需求。

```Markdown
## My Great Heading {#custom-id}
[Heading](#custom-id)
```

## 定义列表

一些Markdown处理器允许您创建术语及其对应定义的定义列表。要创建定义列表，请在第一行上键入术语。在下一行，键入一个冒号，后跟一个空格和定义。

```Markdown
First Term
: This is the definition of the first term.

Second Term
: This is one definition of the second term.
: This is another definition of the second term.
```

HTML 看起来像这样

```Html
<dl>
  <dt>First Term</dt>
  <dd>This is the definition of the first term.</dd>
  <dt>Second Term</dt>
  <dd>This is one definition of the second term. </dd>
  <dd>This is another definition of the second term.</dd>
</dl>
```

输出如下：

First Term
: This is the definition of the first term.

Second Term
: This is one definition of the second term.
: This is another definition of the second term.

## 删除线

在单词前后使用两个波浪号

```Markdown
~~Hello World~~
```
输出如下：
~~Hello World~~

## 任务列表语法

要创建带复选框的项目列表，需要在列表项前添加破折号 `-` 和 方括号 `[ ]` ，选中复选框状态请在方括号添加 `x`, 如 `[x]`。

```Markdown
- [x] Write the press release
- [ ] Update the website
- [ ] Contact the media

```

 输出如下：

- [x] Write the press release
- [ ] Update the website
- [ ] Contact the media

## Emoji 表情

有两种方法可以将表情符号添加到Markdown文件中：将表情符号复制并粘贴到Markdown格式的文本中，或者键入emoji shortcodes。

在大多数情况下，可以简单地从 [Emojipedia](https://emojipedia.org/) 等来源复制表情粘贴到文档中。

### 使用表情符号简码

一些 Markdown 应用程序允许你通过键入表情符号短代码来插入表情。
```Markdown
you're so funny :joy:
```
输出如下：

you're so funny :joy:;

**Tip:** 你可以使用此[表情符号简码](https://gist.github.com/rxaviers/7360908), 但需要注意的是，简码解析因程序而异。

## 自动网址链接

许多Markdown处理器会自动将URL转换为链接。这意味着如果您输入http://www.example.com，即使您未使用方括号，您的Markdown处理器也会自动将其转换为链接。

`http://www.example.com`

输出如下：
http://www.example.com

### 禁用自动URL链接

如果您比希望自动链接URL，则可以通过反引号代码来显示链接。

```Markdown
`http://www.example.com`
```

输出如下：
`http://www.example.com`

## 参考
* [Markdown 扩展语法](https://markdown.com.cn/extended-syntax/)