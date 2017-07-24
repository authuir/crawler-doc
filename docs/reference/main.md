# Crawler参数手册

如果你想修改一些默认值，可以在构造 `Crawler()` 的时候配置相关的参数，此时的参数将在全局范围内生效。如果你只想对单个请求配置独立的参数，你可以在调用 `queue()` 函数时覆盖参数。

`Crawler` 使用了 `request` 库，所以 `Crawler` 可供配置的参数列表是 `request` 库的[参数列表](https://github.com/request/request#requestoptions-callback)的超集，即 `request` 库中所有的配置在 `Crawler` 中均适用。

以下为所有参数：

## 基本请求参数

 * `uri`: [String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#String_type) 想要爬取的站点的URL
 * `timeout` : [Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Number_type) 超时时间（单位：毫秒，默认值15000）
 * [All mikeal's requests options are accepted](https://github.com/mikeal/request#requestoptions-callback)

## 回调函数

 * `callback(error, res, done)`: 请求完成后将被调用的回调函数
     * `error`: [Error](https://nodejs.org/api/errors.html) 错误信息
     * `res`: [http.IncomingMessage](https://nodejs.org/api/http.html#http_class_http_incomingmessage) 服务器响应的数据资源合集
         * `res.statusCode`: [Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Number_type) HTTP状态码，正常返回 `200`
         * `res.body`: [Buffer](https://nodejs.org/api/buffer.html) | [String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#String_type) HTTP响应实体部分
         * `res.headers`: [Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) HTTP响应头部
         * `res.request`: [Request](https://github.com/request/request)  An instance of Mikeal's `Request` instead of [http.ClientRequest](https://nodejs.org/api/http.html#http_class_http_clientrequest)
             * `res.request.uri`: [urlObject](https://nodejs.org/api/url.html#url_url_strings_and_url_objects) 处理后的URL的HTTP请求实体
             * `res.request.method`: [String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#String_type) HTTP 请求方法,例如 `GET`,`POST`
             * `res.request.headers`: [Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) HTTP 请求头部
         * `res.options`: [Options](#options-reference) 此次请求的参数
         * `$`: [jQuery Selector](https://api.jquery.com/category/selectors/) HTML或XML文档的jQuery选择器
     * `done`: [Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function) 在处理结束之后必须调用此函数

## 调度参数

 * `maxConnections`: [Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Number_type) 工作线程池的大小 (默认为 10).
 * `rateLimit`: [Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Number_type) 两次请求之间的默认间隔时间 (默认为 0).
 * `priorityRange`: [Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Number_type) 有效的优先值范围，从0开始 (默认为 10).
 * `priority`: [Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Number_type) 请求的默认优先值 (默认为 5). 此值越低优先度越高。

## 重试参数

 * `retries`: [Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Number_type) 请求失败后的重试次数 (默认为 3),
 * `retryTimeout`: [Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Number_type) 重试的默认等待时间，单位为毫秒 (默认为 10000).

## DOM选项

 * `jQuery`: [Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)|[String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#String_type)|[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) 设置为true或者"cheerio"时，将使用 `cheerio` 作为解析器，并使用默认配置. 使用自定义配置的 `cheerio` 或使用符合 [Parser options](https://github.com/fb55/htmlparser2/wiki/Parser-options)的对象时. Disable injecting jQuery selector if false. If you have memory leak issue in your project, use "whacko", an alternative parser,to avoid that. (Default true)

## 编码设置

 * `forceUTF8`: [Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type) If true crawler will get charset from HTTP headers or meta tag in html and convert it to UTF8 if necessary. Never worry about encoding anymore! (Default true),
 * `incomingEncoding`: [String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#String_type) With forceUTF8: true to set encoding manually (Default null) so that crawler will not have to detect charset by itself. For example, `incomingEncoding : 'windows-1255'`. See [all supported encodings](https://github.com/ashtuchkin/iconv-lite/wiki/Supported-Encodings)

## 缓存设置

 * `skipDuplicates`: [Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type) If true skips URIs that were already crawled, without even calling callback() (Default false). __This is not recommended__, it's better to handle outside `Crawler` use [seenreq](https://github.com/mike442144/seenreq)

## 其他

 * `rotateUA`: [Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type) 此值为 `true` 时, `userAgent` should be an array and rotate it (Default false) 
 * `userAgent`: [String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#String_type)|[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array), If `rotateUA` is false, but `userAgent` is an array, crawler will use the first one.
 * `referer`: [String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#String_type) If truthy sets the HTTP referer header