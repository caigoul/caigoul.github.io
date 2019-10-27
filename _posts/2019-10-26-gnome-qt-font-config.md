---
layout: post
title: 如何在gnome上使用比Regular粗一点的微软雅黑字体
excerpt: 系统是Arch，桌面环境是gnome。<br/>Linux上的字体显示对于我这个<del>老年</del>人来说貌似太细了一点（而且发虚），如果不花点力气是很难看清楚的。这里讲述如何通过<code>fontconfig</code>的<b>粗体合成</b>功能，来使用稍微比Regular粗一点的字体。
categories:
  - 日常
tags:
  - 日常
  - linux
  - 字体配置
---

# Gnome上GTK+字体的配置

gnome在Regular粗细的字体显示得并不是特别清楚。

在gnome上虽然有`gnome-tweak`来配置字体，但是无法使用字体特定的样式，比如说将字体设置成 微软雅黑 Bold 之后，GTK界面的字体并没有被加粗。原因是gtk主题的css文件也对GTK程序的界面产生了影响。

现在想到的加粗GTK界面的字体方法是，在fontconfig文件里，为light字体开启粗体合成，然后编辑gtk设置的css文件，强制将所有界面的字体换成light字体。

首先编辑字体配置文件`~/.config/fontconfig/fonts.conf`，加入以下配置，为light字体开启粗体合成。

```
<match target="font">
   <test name="weight" compare="less"><int>80</int></test>
   <edit name="embolden"><bool>true</bool></edit>
</match>
```

之后编辑`~/.config/gtk-3.0/gtk.css`文件，强制为所有元素指定字体，使用被加粗之后的light字体。

```css
* {
	font-family: '微软雅黑 Light'
}
```

这是加粗以前和加粗以后的gtk程序截图。

![img0](/img/2019-10-27-gtk-regular.png)
![img1](/img/2019-10-27-gtk-bolden.png)

这样子的话，gnome-tweak上的字体配置将会无效，但至少gtk程序的字体看起来更加舒服了一点。

## QT程序的字体配置

现在QT程序有两个问题，一个是fontconfig上的合成加粗无法使用，另一个是，界面的主题和GTK主题不一致。这是QBittorrent的一个截图：

![img2](/img/2019-10-27-qt-before.png)

解决办法是，安装`qt5ct`和`qt5-styleplugins`来为qt使用GTK主题，同时配置字体。

```
sudo pacman -S qt5ct qt5-styleplugins
```

然后编辑`~/.profile`文件，添加一个环境变量：

```
export QT_QPA_PLATFORMTHEME="qt5ct"
```

重启系统之后，就可以使用qt5ct来配置QT程序的主题和字体了，主题选择gtk2，字体使用了 思源黑体 Normal。

![img3](/img/2019-10-27-qt5ct-theme-config.png)

这样子QT程序的样式就和GTK统一起来了，并且字体也配置完毕。这是之后QBittorrent的截图：

![img4](/img/2019-10-27-after.png)