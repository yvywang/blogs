---
title: Visual Studio Code 常用快捷键
author: Yu
toc: true
date: 2022-03-08 12:57:08
cover: https://cdn.jsdelivr.net/gh/yvywang/figure-bed@main/img/202203091529241.png
tags: [vscode]
categories: [vscode, shortcut]
---

## 概述

在日常开发中，熟练使用快捷键可以提高开发的效率及体验，本文记录在 Mac 使用编辑器 vscode 中常用的快捷键。

<!-- more -->

## 光标移动

| Description                        | Shortcut                    |
| ---------------------------------- | --------------------------- |
| 单词为单位移动到其 ( 前面 / 后面 ) | `option[⌥] + （ ← / → ）`   |
| 当前行（ 向上 / 向下）移动一行     | `option[⌥] + （ ↑ / ↓ ）`   |
| 移动到当前行最 （ 前面 / 后面 ）   | `command[⌘] + （ ← / → ）`  |
| 花括号之间跳转                     | `command[⌘] + shift[⇧] + \` |
| 移动到文档 （ 第一行 / 最后一行 ） | `command[⌘] + ( ↑ / ↓ )`    |

## 文本操作

| Description                                | Shortcut                              |
| ------------------------------------------ | ------------------------------------- |
| 以字符为单位选择文本                       | `shift[⇧] + （ ← / → ）`              |
| 以单词为单位选择文本                       | `shift[⇧] + option[⌥] + （ ← / → ）`  |
| 以光标的位置为起点到当前行（ 最前 / 最后） | `shift[⇧] + command[⌘] + （ ← / → ）` |
| 折叠当前文本块                             | `command[⌘] + option[⌥] + ( [ / ] )`  |


## 文件、符号、代码之间的快速跳转

| Description                                      | Shortcut                           |
| ------------------------------------------------ | ---------------------------------- |
| 查看已打开文件列表                               | `control[⌃]`                       |
| 搜索当前打开目录的文件,可选指定行聚焦光标        | `command[⌘] + P (?:number`         |
| 跳转到指定行                                     | `control[⌃] + G`                   |
| 查看文件的符号（ 函数名... ），可选 `:` 进行分类 | `command[⌘] + shift[⇧] + o (?:`    |
| 查看函数定义位置仅适用于纯 ( TS \| JS )          | `fn + F12 / command[⌘] + fn + F12` |

**Tips:**
`command[⌘] + shift[⇧] + P` 打开 Vscode 可配置列表
`code .` 使用 Vsocde 打开当前终端所在的目录
