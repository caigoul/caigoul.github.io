---
layout: post
title: "Nodejs的控制台：console"
excerpt: nodejs笔记（0）
cover: /img/head/nodejs0.jpg
categories:
  - nodejs
tags:
  - nodejs
---

> [Node.js官方文档 (http://nodejs.cn/api/console.html)](http://nodejs.cn/api/console.html)

在Node.js中，`console`代表控制台，可以通过console的各种方法对控制台进行输出。

# console.log()

`console.log`用来向控制台输出一行信息。向控制台输出`F*ck the rubbish Node.js!`：

```javascript
console.log('F*ck the rubbish Node.js!');
```

或者传入多个参数，控制台时以*空格*分隔这些参数。

```javascript
console.log('F*ck', 'the', 'rubbish', 'Node.js!');
```

`console.log`可以使用**占位符**来定义输出的格式，如`%d`代表数字，`%s`代表字符串。

```javascript
console.log('Total num = %d', 0);
```



# console.dir()

将一个对象的信息输出到控制台。

```javascript
const obj = {
	name: 'a simple demo',
	set: function(name) {
		this.name = name;
		console.log('Set the name: %s -> %s', this.name, name);
	},
	get: function() {
		console.log(this.name)
	}
}

console.dir('obj')
```

运行结果如下:

```javascript
{ name: 'a simple demo',
  set: [Function: set],
  get: [Function: get] }
```



# console.time() console.timeEnd()

用于统计一段代码运行的时间，`console.time()`置于代码起始处，`console.tineEnd()`置于代码结尾处。统计时间以毫秒为单位。

函数接受一个字符串，作为计时的 label。

```javascript
console.time('total time');

console.time('time1');
for(let i = 0; i < 10000; i++) {}
console.timeEnd('time1');

console.time('time2');
for(let i - 0; i < 100000; i++) {}
console.timeEnd('time2');

console.timeEnd('totle time')
```

```javascript
time1: 0.336ms
time2: 2.251ms
total time: 19.153ms
```



# console.trace()

输出当前位置的堆栈信息，同样接受一个字符串作为label。

```javascript
console.trance('Trace');
```

```javascript
> console.trace('Trace')
Trace: Trace
    at Console.trace (internal/console/constructor.js:336:11)
    at repl:1:9
    at Script.runInThisContext (vm.js:124:20)
    at REPLServer.defaultEval (repl.js:325:29)
    at bound (domain.js:425:14)
    at REPLServer.runBound [as eval] (domain.js:438:12)
    at REPLServer.onLine (repl.js:650:10)
    at REPLServer.emit (events.js:198:15)
    at REPLServer.EventEmitter.emit (domain.js:481:20)
    at REPLServer.Interface._onLine (readline.js:307:10)
```

