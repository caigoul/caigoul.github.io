---
layout: post
title: "Nodejs包管理器:npm"
excerpt: nodejs笔记（1）
cover: /img/head/nodejs1.jpeg
categories:
  - nodejs
tags:
  - nodejs
---

`npm`是`Node.js`的包管理器工具，默认与`Node.js`一起安装。通过 npm 可以很方便吧地下载和使用第三方模块，简化开发工作。

# npm init

通过`npm init`将生成一个`package.json`文件，这个文件是整个项目的描述文件。这个文件可以清楚地知道项目的依赖关系、版本、作者等信息。

使用`npm init`时，需要填写项目名、版本号、作者等信息，填写完毕之后，将会在使用这个命令的文件夹下产生一个`package.json`文件。

新建名字为 test 的项目：

```
mkdir test && cd test
npm init
# 填写项目信息，填写完毕之后，test文件夹下将会生成 package.json文件
```

![npm init](/img/2019-06-16-npm-init.png)

可以使用`-y`或者`--yes`参数来跳过填写内容。

```
npm init -y
# 或者 npm init --yes
```

# npm install

`npm install`用来安装 node.js 模块。如安装`underscore`模块:

```
npm install underscore
```

安装完毕之后，运行命令的文件夹将会多出一个`node_modules`文件夹，在这个文件夹下就可以找到`underscores`这个文件夹。

![npm install](/img/2019-06-16-npm-install.png)

如果模块只是在开发、调试时使用到（如 vue-cli, babel-loader），使用`--save-dev`参数，这时`package.json`文件的`devDependencies`字段将会记录安装的模块信息。

```
npm install --save-dev underscore
```

![npm install --save-dev](/img/2019-06-16-npm-install-save-dev.png)

如果是项目在运行、发布到生产环境时依赖的模块（如 antd , element,react）,使用`--save`参数，这时`package.json`文件的`dependencies`字段将会记录安装的模块信息。

```
npm install --save underscore
```

![npm install --save underscore](/img/2019-06-16-npm-install-save.png)

使用`npm install`命令，npm 会自动下载`package.json`文件里`dependencies`和`devDependencies`字段下的依赖模块。

使用`npm uninstall`来卸载模块。

# 导入模块

对于 Node.js 原生模块和 npm 下载的模块，使用`require()`并赋值给一个变量，就可以使用该模块的属性和功能。

```javascript
var http = require("http");
```

如果要导入一个文件模块，使用**相对路径**来加载模块，可以省略 js 后缀名。

```javascript
var myRubbishModule = require("./mymodule/ARubbishModule");
```

# 导出模块

一个模块的变量和方法只能作用于模块自己，如果要与其他模块共享一些方法或属性，可以使用`exports`导出一个对象。

假设下面的模块名为`exports.js`，使用`exports`导出两个方法，一个用于计算数组之和，一个用于数组去重：

```javascript
function noRepeat(arr) {
  return arr.filter(function(ele, index) {
    return arr.indexOf(ele) == index;
  });
}

function add(arr) {
  return arr.reduce(function(ele1, ele2) {
    return ele1 + ele2;
  });
}

module.exports = {
  noRepeat: noRepeat,
  add: add
};
```

在另一个文件里引入`exports`模块：

```javascript
var mymodule = require("./exports");
const arr = [1, 2, 2, 3];
console.log("数组和   =>" + mymodule.add(arr));
console.log("数组去重 =>" + mymodule.noRepeat(arr));
```

```
数组和   =>8
数组去重 =>1,2,3
```
