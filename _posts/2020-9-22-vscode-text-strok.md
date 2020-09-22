---
layout: post
title: vscode 字体描边
excerpt: vscode 在 linux 下的中文显示其实并不算很好，字号稍微小一点就会发虚。这里讨论如何使用 css3 中的 text-stroke 属性来改善 vscode 的使用体验。
categories:
  - 日常
tags:
  - vscode
---

这里还是先上一张前后的效果图，原理是给 vscode 嵌入自定义的 css 代码：

![preview](/img/2020-09-22-preview.png)

## 安装拓展

为 vscode 字体描边使用的插件是 [Custom CSS and JS Loader](https://marketplace.visualstudio.com/items?itemName=be5invis.vscode-custom-css)，因为需要在 vscode 中引入自定义的 css 文件，因此需要以 **root 权限** 打开 vscode（在终端中使用`sudo code`启动 vscode）。

在安装完 Custom CSS and JS Loader 这个插件后，需要使用 `Ctrl + Shift + P` 打开命令面板，输入 settings json，来打开 vscode 配置文件 `settings.json`，在末尾添加

```json
"vscode_custom_css.imports": [
	"file:///path/to/your/css/file"
],
"vscode_custom_css.policy": true,
```

`vscode_custom_css.imports` 里指定要嵌入的 css 文件的位置。

## 创建 css 文件并完善 vscode 设置

之后就是创建一个 css 文件，里面只有三行代码：

```css
* {
  -webkit-text-stroke-width: 0.5px !important;
}
```

代码很简单，只是用了 css3 里的 text-stroke 属性，来指定文本描边的像素值。

最后在 settings.json 里将 css 文件的路径填入 `vscode_custom_css.imports` 就行。注意文件路径要以`file://` 开头，后面才是文件的绝对路径。之后使用快捷键 `Ctrl + Shift + P` 打开命令面板，输入 reload，来重启 vscode，会发现之前的 css 文件已经生效了。
