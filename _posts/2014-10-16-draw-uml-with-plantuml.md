---
layout: post
title: "PlantUML绘制UML"
description: "使用PlantUML绘制UML"
category: "杂项"
tags: [plantuml, uml]
excerpt: "PlantUML是一个开源项目，它能够方便的绘制各种UML图形，并支持多种图形导出格式。
PlantUML定义了一个简单直观的语言，非常容易学习。
PlantUML是一个命令行工具，能够十分容易的和其他工具结合使用。"
---
{% include JB/setup %}

[PlantUML](http://plantuml.sourceforge.net/) 是一个开源项目，能够方便的绘制各种UML图形：
- 时序图
- 用例图
- 类图
- 活动图
- 组件图
- 状态图
- 对象图

PlantUML 使用一个非常简单直观的语言来定义图形， 每个定义均包含在 `@startuml` 和 `@enduml`。

## 时序图
时序图使用 `->` 绘制`参与者`之间的消息。例如：
{% highlight text %}
@startuml
A -> B: 请求 1
B -> C: 请求 1
C -> B: 应答 1
B -> A: 应答 1
@enduml
{% endhighlight %}

PlantUML 绘制的结果如图：

<div class="img-center" markdown="1">
![时序图]({{ site.url }}/assets/imgs/seq1.png)
</div>
