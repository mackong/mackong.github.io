---
layout: post
title: "SVN批量添加和删除"
description: "SVN批量添加和删除"
category: "杂项"
tags: [svn]
excerpt: "SVN默认不能很好的支持批量添加和删除， 通过简单的脚本可以使SVN方便的支持批量操作。"
---
{% include JB/setup %}

SVN默认不能很好的支持批量添加和删除， 通过简单的脚本可以使SVN方便的支持批量操作。参考 [这里](http://www.base-10.net/blog/2009/12/11/subversion-bulk-add-or-remove/)。

## 添加
{% highlight sh %}
~ $ svn st | grep ^? | sed 's/?[ ]*//' | xargs svn add
{% endhighlight %}

## 删除
{% highlight sh %}
~ $ svn st | grep ^! | sed 's/![ ]*//' | xargs svn rm
{% endhighlight %}

**注意** 上述命令中的sed部分的方括号中均有一个空格。
