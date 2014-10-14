---
layout: post
title: "Jekyll-Bootstrap和Github搭建个人博客"
description: "使用Jekyll-Bootstrap和Github搭建个人博客"
category: "杂项"
tags: [jekyll, jekyll bootstrap, github]
---
{% include JB/setup %}

利用 [Jekyll](http://jekyllrb.com) 和 [Jekyll-Bootstrap](http://jekyllbootstrap.com) 可以非常方便的生成一个静态站点, 利用 [Github](https://github.com) 的 [Pages](https:/pages.github.com) 功能可以方便的
将站点内容发布到网络上。结合Jekyll和Github便可非常方便的搭建一个个人博客。下面详细的介绍这样一个博客的搭建过程。

**注意** 以下介绍均以`Fedora 20`系统为准。

## 安装Jekyll
Jekyll基于Ruby语言编写，在终端输入以下命令进行安装：
{% highlight sh %}
~ $ gem install jekyll
{% endhighlight %}

可以通过
{% highlight sh %}
~ $ jekyll -v
{% endhighlight %}
来确定是否安装成功。

## 创建项目仓库
登录 [Github](https://github.com/login) 创建一个新的项目仓库，仓库名称叫做 `USERNAME.github.io`, 其中USERNAME是你自己的github名称。如图

![创建项目仓库]({{ site.url }}/assets/imgs/create-repository.png ) 

**注意** 不要勾选`Initialize this repository with a README`, 否则会导致后面的git push失败。

## 安装Jekyll-Bootstrap
在终端输入以下命令，安装Jekyll-Bootstrap:
{% highlight sh %}
~ $ git clone https://github.com/plusjade/jekyll-bootstrap.git USERNAME.github.io
~ $ cd USERNAME.github.io
~ $ git remote set-url origin git@github.com:USERNAME/USERNAME.github.io.git
~ $ git push origin master
{% endhighlight %}

命令完成之后，便完成了安装。

## 访问
此时，通过浏览器输入 `http://USERNAME.github.io` 便可访问你的个人博客了。由于Github生成站点需要一些时间，如果无法访问，可能需要等一段时间。如果一段时间之后，然后无法访问，需要确定上述步骤是否出现错误。

## 发表文章
上述步骤完成之后，通过
{% highlight sh %}
~ $ rake post title="HELLO WORLD"
{% endhighlight %}
命令，便可在`_post`目录下生成一个文章模板文件。修改该文件，便可以开始撰写博客的实际内容了。

## 其它
### 中文
观察生成的页面，会发现页面顶部的菜单等内容均是英文。如果需要修改成中文，需要修改相应的文件。例如要将`Tag`修改成`标签`，则需要修改根目录下的`tags.html`, 将其中的
{% capture text %} title: Tag
{% endcapture %}
{% include JB/liquid_raw %}
修改成
{% capture text %} title: 标签
{%endcapture %}
{% include JB/liquid_raw %}
即可。
