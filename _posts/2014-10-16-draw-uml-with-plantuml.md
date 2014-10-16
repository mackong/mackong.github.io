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
时序图中，使用 `->` 绘制`参与者`之间的消息。例如：
{% highlight text %}
@startuml
Alice -> Proxy: SIP MESSAGE 1
Proxy --> Bob: SIP MESSAGE 2
Proxy <- Bob: 200 OK 1
Alice <-- Proxy: 200 OK 2
@enduml
{% endhighlight %}

PlantUML 绘制的结果如图：

<div class="img-center" markdown="1">
![时序图]({{ site.url }}/assets/imgs/seq1.png)
</div>

为了可读性更好，PlantUML支持 `<-`。 对于 `-->` / `<--`， PlantUML会生成点线。

## 用例图
用例图中，使用 `()` 定义 `用例`， `::` 定义 `主角`。例如：
{% highlight text %}
@startuml
:用户: -> (查询)
:用户: -> (缴费)
:用户: -> (取款)
:用户: -> (转账)
@enduml
{% endhighlight %}

PlantUML 绘制的结果如图：

<div class="img-center" markdown="1">
![用例图]({{ site.url }}/assets/imgs/usecase1.png)
</div>

## 类图
类图中，使用 `<|--` 定义 `继承`， `*--` 定义 `组合`， `o--` 定义 `聚合`。例如：
{% highlight text %}
@startuml
Class01 <|-- Class02
Class03 *-- Class04
Class05 o-- Class06
@enduml
{% endhighlight %}

PlantUML 绘制的结果如图：

<div class="img-center" markdown="1">
![类图]({{ site.url }}/assets/imgs/class1.png)
</div>

## 活动图
活动图中， 使用 `""` 定义 `活动`， `(*)` 定义 `起点` 和 `终点`， `-->` 定义 `箭头`。例如：
{% highlight text %}
@startuml
(*) --> "First Activity"
--> "Second Activity"
--> (*)
@enduml
{% endhighlight %}

PlantUML 绘制的结果如图：

<div class="img-center" markdown="1">
![活动图]({{ site.url }}/assets/imgs/activity1.png)
</div>

## 组件图
组件图中，使用 `[]` 定义 `组件`， `()` 定义 `接口`， 可以组合使用 `..`, `--`, `-->`。例如：
{% highlight text %}
@startuml
() DataAccess - [First Component]
[First Component] --> HTTP
@enduml
{% endhighlight %}

PlantUML 绘制的结果如图：

<div class="img-center" markdown="1">
![组件图]({{ site.url }}/assets/imgs/component1.png)
</div>

## 状态图
状态图中，直接使用 `名称` 定义 `状态`， `[*]` 定义 `起点` 和 `终点`， `-->` 定义 `箭头`。 例如
{% highlight text %}
@startuml
[*] --> State1
State1 --> [*]
State1 -> State2
State2 --> [*]
@enduml
{% endhighlight %}

PlantUML 绘制的结果如图：

<div class="img-center" markdown="1">
![状态图]({{ site.url }}/assets/imgs/state1.png)
</div>

## 对象图
对象图中，使用 `object` 关键字定义 `对象`，`<|--` 定义 `继承`， `*--` 定义 `组合`， `o--` 定义 `聚合`。例如：
{% highlight text %}
@startuml
object Object01
object Object02
object Object03
object Object04
object Object05
object Object06

Object01 <|-- Object02
Object03 *-- Object04
Object05 o-- Object06
@enduml
{% endhighlight %}

PlantUML 绘制的结果如图：

<div class="img-center" markdown="1">
![对象图]({{ site.url }}/assets/imgs/object1.png)
</div>

## 在Jekyll中使用PlantUML
[Jekyll](http://jekyllrb.com) 提供插件支持，可以通过插件的方式在Jekyll中使用PlantUML。具体方法参看 [这里](https://github.com/mackong/jekyll-liquid-plantuml-plugin)。

**注意**， 这种方式只能在本地使用，无法在Github上使用。

## 在org-mode中使用PlantUML
Emacs的org-mode提供对PlantUML的支持。 配置如下：
{% highlight cl %}
(org-babel-do-load-languages
 'org-babel-load-languages
 '((plantuml . t)
   ))
(setq org-confirm-babel-evaluate nil)
(setq org-plantuml-jar-path (expand-file-name "/path/to/plantuml.jar"))
{% endhighlight %}

通过上述配置，在 `.org` 文件中，输入：

{% highlight text %}
#+BEGIN_SRC plantuml :file /path/to/result.png :cmdline -charset UTF-8
Alice -> Proxy: SIP MESSAGE 1
Proxy --> Bob: SIP MESSAGE 2
Proxy <- Bob: 200 OK 1
Alice <-- Proxy: 200 OK 2
#+END_SRC
{% endhighlight %}

按下 `C-c C-c` 便可生成UML图形。

## 注意
PlantUML的功能远不止上述介绍的这些，这里抛砖引玉，更多更详细的介绍参看 [这里](http://plantuml.sourceforge.net/PlantUML_Language_Reference_Guide.pdf)。
