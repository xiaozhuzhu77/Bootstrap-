## HTML `<meta>` 标签 ##
###定义和用法###
1.<meta> 元素可提供有关页面的元信息（meta-information），比如针对搜索引擎和更新频度的描述和关键词。
2.<meta> 标签位于文档的头部，不包含任何内容。<meta> 标签的属性定义了与文档相关联的名称/值对。

*注释：*元数据总是以名称/值的形式被成对传递的。
### 必须的属性###

属性| 值 | 描述
-----------|-----------------------|-------------------
content|	some_text	|定义与 http-equiv 或 name 属性相关的元信息

###可选的属性###
属性	|值|	描述
-----------|-----------------------|-------------------
http-equiv	|content-type expires refresh set-cookie|把 content 属性关联到 HTTP 头部。
name	| author description keywords generator revised others|把 content 属性关联到一个名称。
scheme|	some_text|定义用于翻译 content 属性值的格式。

###< meta http-equiv = "X-UA-Compatible" content = "IE=edge,chrome=1" />###
这是个是IE8的专用标记,用来指定IE8浏览器去模拟某个特定版本的IE浏览器的渲染方式（比如人见人烦的IE6），以此来解决部分兼容问题，例如模拟IE7的具体方式如下：
< meta http-equiv = "X-UA-Compatible" content = "IE=EmulateIE7" />
但令我好奇的是，此处这个标记后面竟然出现了chrome这样的值，难道IE也可以模拟chrome了？
迅速搜索了一下，才明白原来不是微软增强了IE，而是谷歌做了个外挂：Google Chrome Frame（谷歌内嵌浏览器框架GCF）。这个插件可以让用户的IE浏览器外不变，但用户在浏览网页时，实际上使用的是Google Chrome浏览器内核，而且支持IE6、7、8等多个版本的IE浏览器，谷歌这个墙角挖的真给力！
而上文提到的那个meta标记，则是在是安装了GCF后，用来指定页面使用chrome内核来渲染。

GCF下载地址: http://code.google.com/intl/zh-CN/chrome/chromeframe/
安装完成后,如果你想对某个页面使用GCF进行渲染，只需要在该页面的地址前加上 gcf： 即可，例如： gcf:http://cooleep.com
但是如果想要在开发时指定页面默认首先使用GCF进行渲染，如果未安装GCF再使用IE内核进行渲染，该如何进行呢？
就是使用这个标记。

标记用法：

1.最基本的用法：在页面的头部加入
``
**`< meta http-equiv = "X-UA-Compatible" content = "chrome=1" >`**
```

用以声明当前页面用chrome内核来渲染。
复杂一些的就是本文一开始看到的那中用法：
```
`< meta http-equiv = "X-UA-Compatible" content = "IE=edge,chrome=1" />`
```

这样写可以达到的效果是如果安装了GCF，则使用GCF来渲染页面，如果为安装GCF，则使用最高版本的IE内核进行渲染。
2.通过修改HTTP头文件的方法来实现让指定的页面使用GCF内核进行渲染：
在HTTP的头文件中加入以下信息：X-UA-Compatible: chrome=1
在Apache服务器中，确保 mod_headers 和 mod_setenvif文件可用，然后在httpd.conf中加入以下配置信息：
```
1. < IfModule mod_setenvif.c>
2. < IfModule mod_headers.c>
3. BrowserMatch chromeframe gcf
4. 4Header append X-UA-Compatible "chrome=1" env=gcf
5. </ IfModule >
6. </ IfModule >
```
在IIS7或者更高版本的服务器中，只需要修改web.config文件,添加如下信息即可即可:
```
1. < configuration >
2. < system.webServer >
3. < httpProtocol >
4. < customHeaders >
5. < add name = "X-UA-Compatible" value = "chrome=1" />
6. </ customHeaders >
7. </ httpProtocol >
8. </ system.webServer >
9. </ configuration >
```
```
Http-equiv 参考链接：http://kinglyhum.iteye.com/blog/827807
```


***IE8需要配合 Response.js 来实现响应式（即实现对媒体查询的支持）***

