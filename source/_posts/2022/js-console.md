---
title: console 输出
author: Yu
toc: true
date: 2022-03-14 13:13:49
cover: https://cdn.jsdelivr.net/gh/yvywang/figure-bed@main/img/202203141322495.png
tags: [JavaScript]
categories: [JavaScript, console]
---

## 概述

在查看日志，输出调试，常用到 `console` ，这里深入介绍一下它的用法。

<!-- more -->

## 占位符

| key         | Description               |
| ----------- | ------------------------- |
| `%s`        | 字符串                    |
| `%d` / `%i` | 整数                      |
| `%f`        | 浮点数                    |
| `%o`        | 可展开DOM                 |
| `%O`        | 列出DOM的属性             |
| `%c`        | css样式格式化输出的字符串 |

**示例**

```JavaScript
console.info("%d年%d月%d日",2022,03,14);
console.log('%c Hello World', 'color: pink; background: blue;')
```

## 常见

常见的控制台方法：

```JavaScript
console.log() // - 打印内容的通用方法。
console.info() // - 打印资讯类说明信息
console.debug() // - 控制台打印 'debug'级别的信息。
console.warn() // - 打印一个警告信息。
console.error() // - 打印一个错误信息。并显示其堆栈
```

## 进阶

这一块的方法相对少用，科普一下，起码不能不知道 😄

**Console 对象方法**

<table>
    <tr>
        <th>Method</th>
        <th>Description</th>
        <th>Demo</th>
    </tr>
    <tr>
        <td>assert</td>
        <td>该方法接受两个参数 ( 表达式, 字符串 ) 只有当表达式不成立，才会输出打印字符串</td>
        <td>
            ```JavaScript
                console.assert( 1 === 2, "不相等")
                // error - Assertion failed: 不相等
            ```
        </td>
    </tr>
    <tr>
        <td>clear</td>
        <td>清除当前控制台的所有输出，将光标回置到第一行</td>
        <td>
            ```JavaScript
                console.clear()
            ```
        </td>
    </tr>
    <tr>
        <td>group</td>
        <td>将打印的信息进行分组，可以折叠和展开查看</td>
        <td>
            ```JavaScript
                console.group('ul')
                    console.warn('warn')
                    console.error('error')
                console.groupEnd()
            ```
        </td>
    </tr>
    <tr>
        <td>groupCollapsed</td>
        <td>和 group 方法类似，唯一区别就是初始状态是折叠的</td>
        <td>
            ```JavaScript
                console.groupCollapsed('ul');
                    console.warn('warn')
                    console.error('error')
                console.groupEnd();
            ```
        </td>
    </tr>
    <tr>
        <td>table</td>
        <td>将复合类型的数据转为表格显示</td>
        <td>
            ```JavaScript
                const obj = {
                    a:{ num: "1"},
                    b:{ num: "2"},
                    c:{ num: "3" }
                }
                console.table(obj)
            ```
        </td>
    </tr>
    <tr>
        <td>time</td>
        <td>通常用来计时，和 timeEnd 搭配使用</td>
        <td>
            ```JavaScript
                console.time('timer')
                // code...
                console.timeEnd('timer')
            ```
        </td>
    </tr>
    <tr>
        <td>trace</td>
        <td>追踪函数的调用过程</td>
        <td>
            ```JavaScript
                const fun = () => console.trace()
                const a = () => fun()
                const res = a()
            ```
        </td>
    </tr>
    <tr>
        <td>count</td>
        <td>用于计数，每执行一次 count 所标记的 字符串 都会打印当前执行的次数</td>
        <td>
            ```JavaScript
                let count = 10
                while(count--){
                    console.count('test')
                }
                // log - test: 1
                // log - test: 2
                // ······
                // log - test: 10
            ```
        </td>
    </tr>
</table>
