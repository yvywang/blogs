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

| Script                          | Description                                                                 |
| ------------------------------- | --------------------------------------------------------------------------- |
| `prepublish`                    | `publish` or `npm install（ 不带参数 ）` 前执行                             |
| `prepare`                       | `prepublish`后， `prepublishOnly` 前 or `npm install（ 不带参数 ）` 前 执行 |
| `prepublishOnly`                | `publish` 前执行                                                            |
| `publish, postpublish`          | `publish` 后执行                                                            |
| `preinstall `                   | `install` 前执行                                                            |
| `install, postinstall`          | `npm install` 后执行                                                        |
| `preuninstall, uninstall`       | `npm uninstall` 前执行                                                      |
| `postuninstall`                 | `npm uninstall` 后执行                                                      |
| `preversion`                    | `npm version xxx` 前执行 (更新版本)                                         |
| `version`                       | 更新版本,提交 `commit` 前执行                                               |
| `postversion`                   | 更新版本，提交 `commit` 后执行                                              |
| `pretest, posttest`             | `npm test` 的勾子                                                           |
| `prestop, poststop`             | `npm stop` 的勾子                                                           |
| `prestart, poststart`           | `npm start` 的勾子                                                          |
| `prerestart, postrestart`       | `npm restart` 的勾子（ 如无配置 `restart`， 则会执行 `start && stop`  ）    |
| `preshrinkwrap, postshrinkwrap` | `npm shrinkwrap` 的勾子（ 用于固定依赖版本 ）                               |

**Tips:**
* 所有的 `script` 都有自己的 `pre, post` 勾子，执行配置的 `scripts` 时，会自动匹配执行对应的勾子；依赖包里面 `package.json` 的 `scripts` 可以用 `npm explore <pkg> -- npm run <script>` 执行

## 参考
* [npm Docs - scripts](https://docs.npmjs.com/cli/v8/using-npm/scripts)