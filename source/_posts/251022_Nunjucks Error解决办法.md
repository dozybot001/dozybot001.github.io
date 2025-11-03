---
title: Nunjucks Error 解决办法
categories:
  - Software
tags:
  - Hexo
---

写博客时遇见如下错误：

![](https://cdn.jsdelivr.net/gh/dozybot001/blogimage/202510221832878.png)

Nunjucks Error 是一个常见错误。
- 原因：Hexo 调用 Nunjucks 渲染文章，而文章中的`{ something }`会被 Nunjucks 识别为某种指令而报错
- 解决办法：把被报错的内容用：

```bash
{% raw %}

{something}

{% endraw %}
```
包起来。
- 注意：被包住的内容中，Markdown 标识符无法识别，例如标识无序编号的`-`会直接显示出来，并不产生小圆点，图片格式也会失效，如：

![](https://cdn.jsdelivr.net/gh/dozybot001/blogimage/202510221841385.png)

所以只要包住造成报错的公式内容即可：

![](https://cdn.jsdelivr.net/gh/dozybot001/blogimage/202510221842491.png)

同时这个方法还可以解决矩阵或多行公式渲染后挤成一行的问题，例如：

![](https://cdn.jsdelivr.net/gh/dozybot001/blogimage/202510222209499.png)

把矩阵包起来：

![](https://cdn.jsdelivr.net/gh/dozybot001/blogimage/202510222210612.png)

原因是换行符没有被正确识别，当然也可以用转义字符达成一样的效果。

所以，为了彻底杜绝这类渲染错误以及排版错误，建议再每次输入公式时都在前后分别加上 
```bash
{%raw%}
```
和 
```bash
{%endraw%}
```