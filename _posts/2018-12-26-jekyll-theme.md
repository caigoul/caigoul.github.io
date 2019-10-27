---
layout: post
title: "本地化Jekyll themes网站来为自己的GitPage博客挑选主题"
excerpt: 解决国内jekyllthemes.org访问过慢的情况。
categories:
  - jekyll theme
tags:
  - jekyll theme
  - 日常
  - linux
---

> 我想在 github 搭建静态博客的小伙伴会对这篇文章感兴趣 (= =)

# http://jekyllthemes.org/

[Jekyll Themes](http://jekyllthemes.org/)，一个收集了很多**Jekyll 主题**的网站。在这里可以收集到很多的 Jekyll 主题。_(我自己 Bolg 上的主题就是从这里找的)_

![1](/img/2018-12-26-1.png)

![0](/img/2018-12-26-0.png)

但是在国内的访问速度却十分缓慢*（可能服务器在国外吧……）*，有时还会出现访问不上的情况。

![2](/img/2018-12-26-2.png)

# 其实是 github 上的一个 Jekyll 项目

是的，其实 [*Jekyll Themes(*http://jekyllthemes.org/)\*](http://jekyllthemes.org/) 是 github 上的一个开源项目，而且是用 jekyll 写的。项目地址是[https://github.com/mattvh/jekyllthemes/](https://github.com/mattvh/jekyllthemes/)。

那么，我们完全可以把整个项目`git clone`到本地上，然后用`jekyll s`来本地运行（经常在本地调试自己的 jekyll 静态博客的同学应该发现这种方法特别亲切……qwq）。

# 那么，git clone it and ENJOY

这里不会提及关于 ruby、jekyll 和 git 等等等等的安装方法。（能点进来的小伙伴其实应该熟悉这些东西……）

- 把项目 git clone 到本地。

  ```shell
  % git clone https://github.com/mattvh/jekyllthemes/
  正克隆到 'jekyllthemes'...
  remote: Enumerating objects: 4674, done.
  remote: Total 4674 (delta 0), reused 0 (delta 0), pack-reused 4674
  接收对象中: 100% (4674/4674), 16.25 MiB | 1.16 MiB/s, 完成.
  处理 delta 中: 100% (2681/2681), 完成.
  ```

- 进入项目目录，运行项目。

  ```
  % cd jekyllthemes
  % jekyll s
  		------一堆输出信息---------
      Server address: http://127.0.0.1:4000
    Server running... press ctrl-c to stop.
  ```

- 打开浏览器访问`127.0.0.1:4000`, 为自己的 jekyll blog 挑选好看打主题吧。enjoy it :)

![3](/img/2018-12-26-3.png)

> ps:
>
> 可以在项目目录那里运行 git pull 来同步网站（= =）
