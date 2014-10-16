---
layout: post
title: "Jekyll-Bootstrap和Github搭建个人博客"
description: "使用Jekyll-Bootstrap和Github搭建个人博客"
category: "杂项"
tags: [jekyll, jekyll bootstrap, github]
excerpt: 利用 Jekyll 和 Jekyll-Bootstrap 可以非常方便的生成一个静态站点, 利用Github 的 Pages功能可以方便的将站点内容发布到网络上。结合Jekyll和Github便可非常方便的搭建一个个人博客。
---
{% include JB/setup %}

利用 [Jekyll](http://jekyllrb.com) 和 [Jekyll-Bootstrap](http://jekyllbootstrap.com) 可以非常方便的生成一个静态站点, 利用 [Github](https://github.com) 的 [Pages](https:/pages.github.com) 功能可以方便的
将站点内容发布到网络上。结合Jekyll和Github便可非常方便的搭建一个个人博客。下面详细的介绍这样一个博客的搭建过程。

**注意** 以下介绍均以 `Fedora 20` 系统为准。

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

![创建项目仓库]({{ site.url }}/assets/imgs/create-repository.png)

**注意** 不要勾选 `Initialize this repository with a README`, 否则会导致后面的git push失败。

## 安装Jekyll-Bootstrap
在终端输入以下命令，安装Jekyll-Bootstrap:

{% highlight sh %}
~ $ git clone https://github.com/plusjade/jekyll-bootstrap.git USERNAME.github.io
~ $ cd USERNAME.github.io
~ $ git remote set-url origin git@github.com:USERNAME/USERNAME.github.io.git
~ $ git push origin master
{% endhighlight %}

命令完成之后，便完成了安装。

## 配置
Jekyll的配置均在根目录下的 `_config.yml` 文件中。默认的配置是一些测试内容，需要进行修改。如下是本博客的配置：

{% capture text %}permalink: /:year/:month/:day/:title 

exclude: [".rvmrc", ".rbenv-version", "README.md", "Rakefile", "changelog.md"]
highlighter: pygments

title : MacKong
tagline: Site Tagline
author :
  name : MacKong
  email : mackonghp@gmail.com
  github : mackong

production_url : http://mackong.github.io

JB :
  version : 0.3.0

  BASE_PATH : false

  ASSET_PATH : false

  archive_path: /archive.html
  categories_path : /categories.html
  tags_path : /tags.html
  atom_path : /atom.xml
  rss_path : /rss.xml

  comments :
    provider : disqus
    disqus :
      short_name : mackong
   
  analytics :
    provider : google 
    google : 
        tracking_id : 'UA-123-12'
    getclicky :
      site_id : 
    mixpanel :
        token : '_MIXPANEL_TOKEN_'
    piwik :
        baseURL : 'myserver.tld/piwik' # Piwik installation address (without protocol)
        idsite : '1'                   # the id of the site on Piwik

  sharing :
    provider : false
{% endcapture %}
{% include JB/liquid_raw %}

其中每个字段的含义，可参看注释。 为了减少篇幅， 此处删除了所有的行注释。

## 访问
此时，通过浏览器输入 `http://USERNAME.github.io` 便可访问你的个人博客了。由于Github生成站点需要一些时间，如果无法访问，可能需要等一段时间。如果一段时间之后，任然无法访问，需要确定上述步骤是否出现错误。

## 发表文章
上述步骤完成之后，通过

{% highlight sh %}
~ $ rake post title="HELLO WORLD"
{% endhighlight %}

命令，便可在 `_post` 目录下生成一个文章模板文件。修改该文件，便可以开始撰写博客的实际内容了。

## 其它

### 中文菜单
观察生成的页面，会发现页面顶部的菜单等内容均是英文。如果想修改成中文，需要修改相应的文件。例如要将 `Tag` 修改成 `标签`，则需要修改根目录下的 `tags.html`, 将其中的
{% capture text %} title: Tag
{% endcapture %}
{% include JB/liquid_raw %}

修改成

{% capture text %} title: 标签
{%endcapture %}
{% include JB/liquid_raw %}

即可。对于 `Archive`， `Category` 等进行相同的修改即可。

### 中文分类
默认配置下，如果文章的 `Category` 是中文， 则在生成的时候会报错。 解决这个问题，只需要修改 `permalink` 配置项即可，参看上面 `配置` 中 `permalink` 的修改。

### 主题
Jekyll-Bootstrap自带的主题有 `bootstrap-3` 和 `twitter` 两种。如果需要其它的主题，可以去 [此处](http://themes.jekyllbootstrap.com/) 选择。
找到满意的主题之后，点击左下角的 `Install Theme` 按钮， 会弹出如下图的界面：

![安装主题]({{ site.url }}/assets/imgs/install-theme-1.png)

拷贝其中的命令， 如下图：

![安装主题]({{ site.url }}/assets/imgs/install-theme-2.png)

在终端下，切换到博客根目录，执行上面拷贝的命令，便完成了相应主题的安装。

之后，可以通过以下命令：

{% highlight sh %}
~ $ rake theme:switch name="THEME-NAME"
{% endhighlight %}

进行切换。其中 `THEME-NAME` 是你想要切换的主题的名称， 如 `the-program`。

### 代码高亮
Jekyll进行代码高亮有多种方法。本博客使用 [Pygments](http://pygments.org)。

**1.**
首先通过以下命令生成一个 `syntax.css` 文件：

{% highlight sh %}
~ $ pygmentize -S manni -f html > syntax.css
{% endhighlight %}

其中 `manni` 是本博客使用的样式，你可以通过

{% highlight sh %}
~ $ pygmentize -L
{% endhighlight %}

查看pygments支持的样式。

**2.**
将生成的 `syntax.css` 文件拷贝到你选择的Jekyll主题的css文件夹下。例如本博客使用的主题是 `bootstrap-3`, 对应的css文件夹路径为
 `assets/themes/bootstrap-3/css`。

**3.**
修改 `_includes\themes\bootstrap-3\` 目录下的 `default.html`。 此处 `bootstrap-3` 应该换成你所使用的主题名称。
在 `default.html` 文件的第 `22` 后面添加一条代码。如下所示：

{% highlight html %}
<!-- Custom styles -->
<link href="{% raw %}{{ ASSET_PATH }}{% endraw %}/css/style.css?body=1" rel="stylesheet" type="text/css" media="all">

<link href="{% raw %}{{ ASSET_PATH }}{% endraw %}/css/syntax.css" rel="stylesheet" type="text/css" media="all">

<!-- HTML5 Shim and Respond.js IE8 support of HTML5 elements and media queries -->
{% endhighlight %}

**4.**
通过以上步骤，在文章中通过以下代码：
{% highlight text %}
{% raw %}{% highlight c %}{% endraw %}
void hello(void)
{
    printf("hello\n");
}
{% raw %}{% endhighlight %}{% endraw %}
{% endhighlight %}

便可产生代码高亮的效果了。

{% highlight c %}
void hello(void)
{
    printf("hello\n");
}
{% endhighlight %}
