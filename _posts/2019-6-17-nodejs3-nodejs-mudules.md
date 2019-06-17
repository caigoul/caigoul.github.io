---
layout: post
title: "Nodejs常用模块"
excerpt: nodejs笔记（3）—— url、querystring、util、path和dns模块。
head-img: /img/head/nodejs3.jpeg
categories:
  - nodejs
tags:
  - nodejs
---

# url 模块 —— url 地址处理

[`url`](http://nodejs.cn/api/url.html)模块是一个分析、解析 url 的模块。

- [`url.parse(urlString[, parseQueryString[, slashesDenoteHost]])`](http://nodejs.cn/api/url.html#url_url_parse_urlstring_parsequerystring_slashesdenotehost)

  解析 url 字符串并返回一个 url 对象。

- [`url.format(urlObject)`](http://nodejs.cn/api/url.html#url_url_format_urlobject)

  接受一个`url对象`，返回完整的 url 网址。

- [`url.resolve(from, to)`](http://nodejs.cn/api/url.html#url_url_resolve_from_to)

  接受两个网址字符串，并将其拼接起来。

```javascript
var url = require("url");
let parseUrl = "https://www.google.com/?q=node.js";
let urlObj = url.parse(parseUrl);
console.dir(urlObj);
console.log(url.format(urlObj));

/**运行结果
Url {
  protocol: 'https:',
  slashes: true,
  auth: null,
  host: 'www.google.com',
  port: null,
  hostname: 'www.google.com',
  hash: null,
  search: '?q=node.js',
  query: 'q=node.js',
  pathname: '/',
  path: '/?q=node.js',
  href: 'https://www.google.com/?q=node.js' }
https://www.google.com/?q=node.js
**/
```

```javascript
const url = require("url");
console.log(url.resolve("/one/two/three", "four"));
console.log(url.resolve("http://example.com/", "/one"));
console.log(url.resolve("http://example.com/one", "/two"));

/**运行结果
/one/two/four
http://example.com/one
http://example.com/two
**/
```

# querystring —— 查询 URL 字符串处理

[`querystring`](http://nodejs.cn/api/querystring.html)是一个用于解析和格式化 URL 字符串的模块，主要方法：

- [`querystring.parse()`](http://nodejs.cn/api/querystring.html#querystring_querystring_parse_str_sep_eq_options) 将一个 URL 查询字符串解析成一个对象。

- [`querystring.stringify()`](http://nodejs.cn/api/querystring.html#querystring_querystring_stringify_obj_sep_eq_options) 将一个对象序列化为 URL 查询字符串。

```javascript
const querystring = require("querystring");
let str = "keyWord=node.js&name=rubbish";
let obj = querystring.parse(str);
console.log(obj);
// { keyWord: 'node.js', name: 'rubbish' }
```

```javascript
const querystring = require("querystring");
const obj = {
  name: "rubbish",
  keyWord: "Node.js"
};
console.log(querystring.stringify(obj));
// const querystring = require("querystring");
```

# util 模块 —— 实用工具

[`util`](http://nodejs.cn/api/util.html)模块的常用方法：

- [`util.inspect()`](http://nodejs.cn/api/util.html#util_util_inspect_object_options) 返回一个`对象`反序列化形成的字符串。

- [`util.format()`](http://nodejs.cn/api/util.html#util_util_format_format_args)

  返回一个使用占位符格式化的字符串，类似 C 语言的`printf()`，可用的占位符有`%s`、`%d`、`%j`(JSON 对象)。

```javascript
const util = require("util");
var obj = {
  Nodejs: "Rubbish",
  C: "powerful"
};
console.log(util.inspect(obj));
// { Nodejs: 'Rubbish', C: 'powerful' }
```

还可以添加`colors: true`选项，让输出带有颜色。

```javascript
const util = require("util");
var obj = {
  Nodejs: "Rubbish",
  C: "powerful"
};
console.log(
  util.inspect(obj, {
    colors: true
  })
);
```

`util.format()`的参数个数少于占位符，多余的占位符不会被替换。

```javascript
util.format('%s:%s', 'foo'); 
// foo:%s
```

如果参数多余占位符，剩余的参数将会被强制转换成字符串，然后拼接到返回的字符串，参数之间用空格分隔。

```javascript
util.format('%s:%s', 'foo', 'bar', 'baz');
// 'foo:bar baz'
```

如果没有占位符，将用空格分隔参数，并返回拼接后的字符串。

```javascript
util.format('Language', 'C', 'is', 'No.', 1, 'program', 'language' )
// Language C is No. 1 program language
```

# path模块 —— 路径处理

`path`模块用于处理文件路径和目录路径。可用`const path = require('path');`引入。

- [`path.join()`](http://nodejs.cn/api/path.html#path_path_join_paths) 将所有参数连接起来，然后生成符合使用平台的路径。

- [`path.extname()`](http://nodejs.cn/api/path.html#path_path_extname_path) 返回路径参数的拓展名，无拓展名返回空字符窜。

- [`path.parse()`](http://nodejs.cn/api/path.html#path_path_parse_path) 将路径字符串转换成一个对象。

- [`path.format()`](http://nodejs.cn/api/path.html#path_path_format_pathobject) 将一个路径对象转换成一个完整的路径字符串。

```javascript
path.join('dir', 'file')
// 'dir/file'

path.join()
// '.'，表示当前目录

path.join('/foo', 'bar', 'baz/asdf', 'quux', '..');
// '/foo/bar/baz/asdf'

path.extname('index.html');
// '.html'
```

`path.format()`方法返回一个路径对象，

具有`root`、`dir`、`base`、`ext`、`name`字段。

在`Linux`或`Mac OS`上:

```javascript
path.parse('/home/user/dir/file.txt');
// 返回:
// { root: '/',
//   dir: '/home/user/dir',
//   base: 'file.txt',
//   ext: '.txt',
//   name: 'file' }
```

在`Windows`上:

```javascript
path.parse('C:\\path\\dir\\file.txt');
// 返回:
// { root: 'C:\\',
//   dir: 'C:\\path\\dir',
//   base: 'file.txt',
//   ext: '.txt',
//   name: 'file' }
```

# dns模块

[`dns`](http://nodejs.cn/api/dns.html)用于域名处理和域名解析。

- [`dns.resolve()`](http://nodejs.cn/api/dns.html#dns_dns_resolve_hostname_rrtype_callback) 域名解析一个域名，获得资源记录的数组。

- [`dns.lookup()`](http://nodejs.cn/api/dns.html#dns_dns_lookup_hostname_options_callback) 解析域名，获得第一个找到的A（IPV4）或AAAA（IPV6）记录。

- [`dns.reverse()`](http://nodejs.cn/api/dns.html#dns_dns_reverse_ip_callback) 通过IP解析域名。

```javascript
const dns = require('dns')
dns.resolve('baidu.com', (err, address) => {
  if (err) {
    console.error(err);
    return;
  }
  console.log(address);
})
// [ '123.125.114.144', '220.181.38.148' ]
```

```javascript
dns.lookup('baidu.com', (err, address) => {
  if (err) {
    console.error(err);
    return;
  }
  console.log(address);
})
// 220.181.38.148
```

```javascript
dns.reverse('114.114.114.114', (err, ip) => {
  if (err) {
    console.error(err);
    return;
  }
  console.log(ip);
})
// [ 'public1.114dns.com' ]
```