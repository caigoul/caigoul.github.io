---
layout: post
title: "Nodejs模块: http"
excerpt: nodejs笔记（2）
head-img: /img/head/nodejs1.jpeg
categories:
  - nodejs
tags:
  - nodejs
---

> [参见官方文档（http://nodejs.cn/api/http.html）](http://nodejs.cn/api/http.html)

# 创建服务器

```javascript
const http = require("http");

const server = http.createServer((req, res) => {
  res.writeHead(200, {
    "content-type": "text/plain"
  });
  res.end("So simple server");
});

server.listen(3000, () => console.log("listening port 3000"));
```

`http.createServer`返回一个 **基于事件的 http** 服务器，`http.request`可以用来向 http 服务器发送请求。

上面的`res`和`req`分别是`http.IncomingMessage`和`http.ServerResponse`实例。

## `http.Server`的事件

- [`request`](http://nodejs.cn/api/http.html#http_event_request)

  最常用的事件，当客户端请求到来时触发该事件，提供`res`和`req`两个参数，代表请求和相应信息。

- [`connect`](http://nodejs.cn/api/http.html#http_event_connect_1)

  建立 TCP 连接时触发该事件，提供一个`socket`参数，是`net.Socket`类的一个实例。

- `close`

  服务器关闭时触发。

`http.createServer()`方法就是添加了一个`request`事件监听：

```javascript
const http = require("http");
const server = new http.Server();

server.on("request", (req, res) => {
  res.writeHead(200, {
    "content-type": "text/plain"
  });
  res.end("So simple server");
});

server.listen(3000, () => console.log("listening port 3000"));
```

## `http.IncomingMessage`的事件

`http.IncomingMessage` 对象由 `http.Server` 或 `http.ClientRequest` 创建，用于访问响应状态、消息头、以及数据。

- `date` 当请求数据到来时触发，提供一个`chunk`参数，表示接受到的数据。

- `end` 请求数据传输完毕时触发。

- `close`

用户请求结束时，触发该事件。

## `http.IncomingMessage`的主要属性

- `method` HTTP 请求的方法，如`GET`。

- `headers` HTTP 请求头。

- `url` 请求 URL。

- `httpVersion` HTTP 协议的版本。

修改服务器的代码:

```javascript
const http = require("http");
const server = new http.Server();

server.on("request", (req, res) => {
  let data = "";
  res.writeHead(200, {
    "content-type": "text/html"
  });

  req.on("data", chunk => (data += chunk));
  req.on("end", () => {
    let method = req.method;
    let url = req.url;
    let headers = JSON.stringify(req.headers);
    let httpVersion = req.httpVersion;
    res.end(`
    <h1>Data</h1> <p>${data}<p>
    <h1>Method</h1> <p>${method}<p> 
    <h1>url</h1> <p>${url}</p>
    <h1>headers</h1> <p>${headers}</p>
    <h1>httpVersion</h1> <p>${httpVersion}</p>
    `);
  });
});

server.listen(3000, () => console.log("listening port 3000"));
```

打开浏览器查看网页:

![http=server](/img/2019-06-16-http-server.png)

## `http.ServerResponse`

`http.ServerResponse`是服返回给客户端的信息，常用方法：

- `res.writeHead(statusCode, [headers])`

  向请求的客户端发送响应头。

- `res.write(data, [encoding])`

  向请求的客户端发送内容。

- `res.end([data], [encoding])`

  结束请求。

# 向服务器发送请求

`http`模块向服务器发送 HTTP 请求的方法：

> [http.request(option, [callback])](http://nodejs.cn/api/http.html#http_http_request_options_callback)

`option`参数为一个对象。主要字段有：

- `host`
- `port`（默认为 80）
- `method`（默认为`get`）
- `path`（相对路径，默认为 “`\`”）
- `headers`等。

返回一个`httpClientRequest`实例。

> [http.get(option[, callback)]](http://nodejs.cn/api/http.html#http_http_get_options_callback)

get 请求的简便方法。

```javascript
const http = require("http");

let reqData = "";
var req = http.request(
  {
    host: "127.0.0.1",
    port: "3000",
    method: "get"
  },
  res => {
    res.on("data", chunk => (reqData += chunk));
    res.on("end", () => console.log(reqData));
  }
);

req.on("error", e => console.error("ERRO =>", e));
req.end();
```

使用`http.get()`方法:

```javascript
const http = require("http");

let reqData = "";
var req = http.get(
  {
    host: "127.0.0.1",
    port: "3000"
  },
  res => {
    res.on("data", chunk => (reqData += chunk));
    res.on("end", () => console.log(reqData));
  }
);

req.on("error", e => console.error("ERRO =>", e));
req.end();
```

# `http.ClientRequest`对象

`http.request()`和`http.get()`方法返回一个`http.ClientRequest`对象，其主要对象和方法有：

- [`response` 事件](http://nodejs.cn/api/http.html#http_event_response)

  接收到响应时触发。

- [`request.write[, encoding][, chunk]`](http://nodejs.cn/api/http.html#http_request_write_chunk_encoding_callback)

  发送请求数据。

- [`res.end([data][, encoding][, callback])`](http://nodejs.cn/api/http.html#http_request_end_data_encoding_callback)

  <strong style="color:#de3f3f; font-size: 20px">[重要]必须记得调用</strong>, 用于结束请求。

```javascript
const http = require("http");

let option = {
  host: "127.0.0.1",
  port: "3000"
};
let reqData = "";

var req = http.request(option);

req.on("request", res => {
  res.on("data", chunk => (reqData += chunk));
  res.on("end", () => console.log(reqData));
});
req.on("error", e => console.error("ERRO =>", e));
req.end();
```
