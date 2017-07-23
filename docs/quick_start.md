# 快速上手

## 安装

    shell> npm install crawler

## 最简单的使用实例

    var Crawler = require("crawler");

    var c = new Crawler({
        // 在每个请求处理完毕后将调用此回调函数
        callback : function (error, res, done) {
            if(error){
                console.log(error);
            }else{
                var $ = res.$;
                // $ 默认为 Cheerio 解析器
                // 它是核心jQuery的精简实现，可以按照jQuery选择器语法快速提取DOM元素
                console.log($("title").text());
            }
            done();
        }
    });

    // 将一个URL加入请求队列，并使用默认回调函数
    c.queue('http://www.amazon.com');

    // 将多个URL加入请求队列
    c.queue(['http://www.google.com/','http://www.yahoo.com']);

    // 对单个URL使用特定的处理参数并指定单独的回调函数
    c.queue([{
        uri: 'http://parishackers.org/',
        jQuery: false,

        // The global callback won't be called
        callback: function (error, res, done) {
            if(error){
                console.log(error);
            }else{
                console.log('Grabbed', res.body.length, 'bytes');
            }
            done();
        }
    }]);

    // 将一段HTML代码加入请求队列，即不通过抓取，直接交由回调函数处理（可用于单元测试）
    c.queue([{
        html: '<p>This is a <strong>test</strong></p>'
    }]);

## 并发控制及慢速模式

使用 `maxConnections` 参数可控制最大并发数。

    var Crawler = require("crawler");

    var c = new Crawler({
        // 最大并发数默认为10
        maxConnections : 1,
        
        callback : function (error, res, done) {
            if(error){
                console.log(error);
            }else{
                var $ = res.$;
                console.log($("title").text());
            }
            done();
        }
    });

    c.queue('http://www.amazon.com');

使用 `maxConnections` 参数可控制最大并发数。

    var Crawler = require("crawler");

    var c = new Crawler({
        maxConnections : 1,

        // 最大并发数默认为10
        rateLimit: 1000, // `maxConnections` 将被强制修改为 1
        
        callback : function (error, res, done) {
            if(error){
                console.log(error);
            }else{
                var $ = res.$;
                console.log($("title").text());
            }
            done();
        }
    });

    c.queue('http://www.amazon.com');


