## HTML `<meta>` 标签 ##
###定义和用法###
1.<meta> 元素可提供有关页面的元信息（meta-information），比如针对搜索引擎和更新频度的描述和关键词。
2.<meta> 标签位于文档的头部，不包含任何内容。<meta> 标签的属性定义了与文档相关联的名称/值对。

*注释：*元数据总是以名称/值的形式被成对传递的。
### 必须的属性###
```
属性	|  值  | 	描述
-----------|-----------------------|-------------------
content|	some_text	|定义与 http-equiv 或 name 属性相关的元信息
```
###可选的属性###
属性	|值|	描述
http-equiv	|content-type
expires
refresh
set-cookie
|把 content 属性关联到 HTTP 头部。
name	|
author
description
keywords
generator
revised
others
|把 content 属性关联到一个名称。
scheme|	some_text|	定义用于翻译 content 属性值的格式。

