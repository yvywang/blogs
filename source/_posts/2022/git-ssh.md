---
title: ssh 配置
author: Yu
toc: true
date: 2022-03-11 14:46:25
cover: https://cdn.jsdelivr.net/gh/yvywang/figure-bed@main/img/202203111447234.png
tags: [ssh]
categories: [git, ssh]
---

## 概述

这里记录一下在 mac 配置 ssh key 。
开发过程中，向 `github` 的项目提交代码时， `github` 需要知道你当前设备上有没有 `Deploy keys` 中某个 `public key` 配对的 `private key`。

<!-- more -->
## ssh-keygen

 ssh-keygen 是一个认证密钥的生成、管理和转换的工具。采用密钥对的形式，生成一个私钥和一个公钥。
可以用来做用于远程服务器的链接、Github 的 SSH 链接等。

```Shell
 ##使用 -t 参数创建一个指定密钥的类型并添加注释：
 $ ssh-keygen -t rsa -C 'testEmail@xxx.com'
```

| 参数 | 描述                     |
| ---- | ------------------------ |
| -b   | 指定密钥长度             |
| -e   | 读取openssh 的私钥或公钥 |
| -f   | 指定用来保存密钥的文件名 |
| -t   | 指定要创建的密钥类型     |
| -C   | 添加注释                 |

生成输出内容：
```Shell
# 提示键入保存密钥的位置，默认是保存在用户目录下的 ".ssh" 文件夹下。
> Enter file in which to save the key (/Users/你的用户名/.ssh/id_ed25519):

# 提示键入该密钥对的秘密，如果不想每次使用时输入密码，可以直接回车（默认密码为空）
> Enter passphrase (empty for no passphrase):
# 二次确认，同上一步输入
> Enter same passphrase again:

> Your identification has been saved in /Users/evan/.ssh/id_ed25519/github.  #私钥的存放位置
> Your public key has been saved in /Users/evan/.ssh/id_ed25519/github.pub.	 #公钥的存放位置

# 该密钥的指纹，请勿泄漏
> The key fingerprint is:
> SHA256:ffhbuKjfuHbi2nBjcubnkeHjb5LjbusdeusAjbucu8oo comment  #在第一步填写的 描述 会展示在这里，和公钥的末尾

# 该密钥的随机图像，请勿泄漏
> The key's randomart image is:
> +--[ED25519 256]--+
> |  ..**=+BO*      |
> |*Bo+o=E .        |
> |B..o*O.+o. o     |
> |o@+.* o          |
> |    o .o. S      |
> |   .+. o=.       |
> |    .            |
> |                 |
> |                 |
> +----[SHA256]-----+

# END
```

## 配置 Deploy keys

将生成的 `.pub` 后缀文件也就是公钥，添加到 `github` 或其他 `代码托管平台` 对应项目的 Deploy keys 中。\

![Deploy keys](https://cdn.jsdelivr.net/gh/yvywang/figure-bed@main/img/202203111519747.png)

`ssh ` 服务器默认是去 `ssh` 找 `id_rsa`, 现在需要吧我们生成的 `key` 添加到 `ssh-agent` 中，这样 `ssh` 服务器才能匹配找到生成的 `key`

```Shell
# 将 SSH 私钥添加到 ssh-agent，-K 参数指将密码存储在密钥链中
$ ssh-add -K ~/.ssh/id_rsa
```

查看添加结果:
```Shell
$ ssh-add -l
```

## 调试

创建配置文件 `~/.ssh/config` 内容如下：

```Shell
Host TestSSH.github.com
	HostName github.com 
	User git
	PreferredAuthentications publickey
	IdentityFile ~/.ssh/id_rsa_TestSSH_github
Host YourProjectName.gitlab.com
	HostName gitlab.com
	User git
	PreferredAuthentications publickey
	IdentityFile ~/.ssh/id_rsa_YourProjectName_gitlab
```

### 测试

```Shell
$ ssh -T git@TestSSH.github.com

# 预期如下：
> Hi MrSeaWave/TestSSH! You've successfully authenticated, but GitHub does not provide shell access.
```

### 问题

在一次重启电脑后，发现拉项目居然拉不下来，一看 `ssh-agent` 配置的私钥居然没了，后来才发现，每次重启都需要 `ssh-add` 执行一次，这种解决方式让人泪目，一定有一劳永逸的解决方式 ！

#### 发现

在 `linux` 手册可以了解到 `ssh-add` 是把密钥添加到 `ssh-agent` 的高速缓存中。
![linux 手册](https://cdn.jsdelivr.net/gh/yvywang/figure-bed@main/img/202203112057980.png)

那么每次 `ssh` 鉴权的时候，只要指定了密钥就可以快速验证，既然重启后就没了，那么就可以确定这个高速缓存存储是在内存里的。

一劳永逸的思路有两个

1. 能不能每次打开一个终端时，都跑一次 `ssh-add` 多次执行会进行覆盖操作，看起来只有性能上有所顾虑
2. 既然每次重启才被清空，那么可不可以每次开机时跑一次 `ssh-add` 添加一次？

很明显，第二个方案更符合直觉，简单说一下`方案一`的操作。
每次开一个终端 `zsh` 都会去加载并且执行 `startup` 文件，那么我们只需要在这个文件中加入 `ssh-add -K xx` 即可。


下面讲讲`方案二`。
1. 在 `mac` 中有一个 `GUI` 软件可以设置一些脚本， 它就是 `自动操作`
![聚焦搜索]](https://cdn.jsdelivr.net/gh/yvywang/figure-bed@main/img/202203121812254.png)

2. 打开应用后，在弹出来的窗口中点击`新建文稿`
![](https://cdn.jsdelivr.net/gh/yvywang/figure-bed@main/img/202203121813412.png)

3. 在又弹出来的窗口选择`应用程序`
![](https://cdn.jsdelivr.net/gh/yvywang/figure-bed@main/img/202203121811438.png)

1. 搜索 `shell` 后，将 `运行Shell脚本` 拖到右侧 `输入` 区域。
![](https://cdn.jsdelivr.net/gh/yvywang/figure-bed@main/img/202203122216765.png)

1. 在脚本里面输入要执行的语句 `ssh-add -K ~/.ssh/xxx`，然后点击右上角的运行看是否能通过。

2.  `command + s` 保存到你想要放置的地方。
3. 在 `系统偏好设置 - 用户与群组 - 登陆项` 点击下面的 `+` 号，将刚刚添加的脚本添加到这个列表，这里相当于钩子，每次开机都会执行一次这里的列表任务。
![](https://cdn.jsdelivr.net/gh/yvywang/figure-bed@main/img/202203122224130.png)

## 参考

* [Git - 关于SSH](https://docs.github.com/cn/authentication/connecting-to-github-with-ssh/about-ssh)