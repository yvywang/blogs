---
title: husky 使用总结
date: 2022-03-02 20:14:35
tags: [husky]
---

## 概述

在规范一个项目中，一般都需要操作 git hooks 来达到一些需求， 如规范日志，或检查代码格式 ，本文将介绍使用 husky来实现这一需求。

<!-- more -->

### 介绍

它在过去的 <font face="微软雅黑" color="#f14668">husky</font> 配置 <font face="微软雅黑" color="#f14668">git hooks</font> 是在我们项目 <font face="微软雅黑" color="#f14668">package.json</font> 中配置。

如下：
```Json
{
  "husky": {
    "hooks": {
      "pre-commit": "npm run test", 
      "commit-msg": "commitlint -e $HUSKY_GIT_PARAMS"
    }
  }
}
```
为什么它会是过去，  husky 为什么放弃这种配置方式，原因如下 ⬇️

husky 为了能够让用户设置任何类型的 git hooks 能正常工作，它就必须要创建所有类型的 git hooks ，这样就能在 git 工作的每个阶段中调用  husky 所设置的脚本， 这个脚本会检查用户是否配置了该 hook ,如果有就会执行用户配置的命令，没有就继续往下执行。

这么做的好处就是任何类型的 hook  都能符合预期的运行，但是缺点也是非常明显，即使用户没有设置任何  hook ,  husky 也向 git 添加了所有类型的 git hooks。

作者认为这个问题是由于 husky 工作模型的自身缺陷导致的, 要解决只能采用新的工作模型。

新版的 husky 工作原理
husky 使用了 git 2.9 开始引入的其中一个新功能core.hooksPath. 它可以指定 git hooks 所在的目录而不是使用默认的 .git/hooks/。 这样的话 husky 就可以将目录部署到自己的 .husky/ 然后使用 `husky add` 在 .husky/ 目录添加 hook。通过这种方式我们就可以只添加需要的, 并且所有脚本都保存在同一个地方，也就不存在同步文件的问题。

### 实践

1. 安装 husky 
```shell
npm install -D husky
```

2. package.json 添加 prepare 脚本；
```Json
{
  "scripts": {
    "prepare": "husky install"
  }
}
```
prepare 会在 `npm install` （不带参数） 之后执行。 `husky install`  会将.husky/目录指定该目录为 git hooks 所在的目录。

3. 执行下面命令创建 pre-commit git hooks
```Json
npx husky add .husky/pre-commit "npm run test"
```
执行完会发现 .husky/pre-commit 多了这个shell 脚本，那么现在执行 git commit 命令前会先执行 pre-commit 这个脚本。

### 举例
 在项目中我们会使用  <font face="微软雅黑" color="#f14668">commit-msg</font> 这个git hook 来检查提交的备注信息是否符合规范。

 执行如下命令创建 commit-msg hook 使用 commitlint 检查
 ```Shell
 npm install -g @commitlint/cli @commitlint/config-conventional

 echo "module.exports = {extends: ['@commitlint/config-conventional']}" > commitlint.config.js
 
 npx husky add .husky/commit-msg 'npx --no-install commitlint --edit "$1"'
 ```

 
 
 