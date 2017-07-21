# node-crawler：一个轻量级爬虫工具

[Git](https://github.com/bda-research/node-crawler) | [Official Website](http://nodecrawler.org/)

[![npm package](https://nodei.co/npm/crawler.png?downloads=true&downloadRank=true&stars=true)](https://nodei.co/npm/crawler/)

[![build status](https://secure.travis-ci.org/bda-research/node-crawler.png)](https://travis-ci.org/bda-research/node-crawler)
[![Dependency Status](https://david-dm.org/bda-research/node-crawler/status.svg)](https://david-dm.org/bda-research/node-crawler)
[![Gitter](https://img.shields.io/badge/gitter-join_chat-blue.svg?style=flat-square)](https://gitter.im/node-crawler/discuss?utm_source=badge)

## 这就是node-crawler

`node-crawler`是一个轻量级的node.js爬虫工具，兼顾了高效与便利性，支持分布式爬虫系统，支持硬编码，支持http前级代理。

`node-crawler`完全由nodejs写成，天生支持非阻塞异步IO，为爬虫的流水线作业机制提供了极大便利。同时支持对`DOM`的快速选择，对于抓取网页的特定部分的任务可以说是杀手级功能，无需再手写正则表达式，提高爬虫开发效率。

## 特点

* DOM 元素快速解析 & 符合jQuery语法的选择器功能(默认使用Cheerio，支持更换为`JSDOM`等其它DOM解析器)
* 支持连接池模式，并发数和重连数均可配置
* 支持请求队列的优先权（即不同URL的请求能有不同的优先级）
* 支持延时功能（某些服务器对每分钟内连接数有限制）
* 支持`forceUTF8`模式以应对复杂的编码问题，当然你也可以自己为不同的连接设置编码
* 支持4.x及更高版本的Nodejs

## 快速上手

* [安装](https://github.com/bda-research/node-crawler)
* [最简单的使用实例](https://github.com/bda-research/node-crawler)
* [回调处理](https://github.com/bda-research/node-crawler)
* [慢速模式及并发控制](https://github.com/bda-research/node-crawler)

## 高级功能

* [链式模型](https://github.com/bda-research/node-crawler)
* [自定义参数](https://github.com/bda-research/node-crawler)
* [使用http代理](https://github.com/bda-research/node-crawler)
* [处理原始返回数据](https://github.com/bda-research/node-crawler)
* [分布式爬虫](https://github.com/bda-research/node-crawler)

## 参数详细介绍

* 回调设置
* 调度参数
* 重试控制
* DOM选项
* 编码设置
* 缓存设置
* 其它

## Crawler类捕获事件

* Event: 'schedule'
* Event: 'limiterChange'
* Event: 'request'
* Event: 'drain'