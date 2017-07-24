# 高级功能

## 自定义参数

在很多时候，一次爬取过程会由几次网页抓取组成。例如，抓取某新闻站点所有新闻，需要先爬取列表页获得新闻ID，再根据ID构造新闻详细页的URL进行抓取，并最后将新闻以`ID-新闻内容`的`key-value`形式存储。为了应对这种情况，`Node-Crawler` 允许自定义参数，所有参数均存储在`res.options`，并可在callback函数中获得。

    var Crawler = require("crawler");

    var c = new Crawler({
        callback : function (error, res, done) {
            if(error){
                console.log(error);
            }else{
                var $ = res.$;
                console.log($("title").text());
                // 获取输入的自定义参数并打印。
                console.log(res.options.parameter1);
            }
            done();
        }
    });

    c.queue({
        uri:"http://www.baidu.com",
        parameter1:"value1",
        parameter2:"value2",
        parameter3:"value3"
    });

## 使用http代理

`Node-Crawler` 支持http代理，以应对在极端情况下，爬虫运行的节点IP可能无法访问服务器的情况。代理服务器输入格式需要符合 `RFC1738` 规范，即 `scheme://user:pass@host:port` 的形式。

    var Crawler = require("crawler");

    var c = new Crawler({
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

    c.queue({
        uri:"http://www.baidu.com",
        proxy:"http://user:pass@host:port"
    });

## 处理原始返回数据

在爬取图片、PDF文档等二进制文件时，需要对服务器返回的原始数据进行处理，此时需通过指定 `encoding` 参数为 `null` 来禁止 `Node-Crawler` 将其转换为字节流，同时也需要将 `jQuery` 参数指定为 `false` 来禁止 `DOM` 元素提取。
下面是一个抓取图片并保存为本地图片的例子。

    var Crawler = require("crawler");
    var fs      = require("fs");

    var c = new Crawler({
        encoding:null,
        jQuery:false,// set false to suppress warning message.
        callback:function(err, res, done){
            if(err){
                console.error(err.stack);
            }else{
                fs.createWriteStream(res.options.filename).write(res.body);
            }
            
            done();
        }
    });

    c.queue({
        uri:"https://nodejs.org/static/images/logos/nodejs-1920x1200.png",
        filename:"nodejs-1920x1200.png"
    });

