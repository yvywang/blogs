---
title: package 文档
author: Yu
toc: true
date: 2022-03-15 15:13:31
cover: https://cdn.jsdelivr.net/gh/yvywang/figure-bed@main/img/202203151530867.png
tags: [package]
categories: [node, package]
---

## 概述

本文简单说一些 `package.json` 使用的点。

<!-- more -->

## Scripts 脚本

| Script                    | Description                                                                 |
| ------------------------- | --------------------------------------------------------------------------- |
| `prepublish`              | `publish` or `npm install（ 不带参数 ）` 前执行                             |
| `prepare`                 | `prepublish`后， `prepublishOnly` 前 or `npm install（ 不带参数 ）` 前 执行 |
| `prepublishOnly`          | `publish` 前执行                                                            |
| `publish, postpublish`    | `publish` 后执行                                                            |
| `preinstall `             | `install` 前执行                                                            |
| `install, postinstall`    | `npm install` 后执行                                                        |
| `preuninstall, uninstall` | `npm uninstall` 前执行                                                      |
| `postuninstall`           | `npm uninstall` 后执行                                                      |
| `preversion`              | 改变 `version` 前执行                                                       |