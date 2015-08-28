# Manual for Jekyll

## Jekyll是什么

Jekyll是一个简单的博客形态的静态站点生产机器（生成工具）。它有一个模板目录，包含了原始文本格式的文档，通过Markdown（或Textile）以及Liquid转化成一个完整的可发部的静态网站。

## 注意事项

### 安装Jekyll
 
 Jekyll有几个配置要求：
 
1. Ruby
 
    - Ubuntu

                >  sudo apt-get install ruby-full
    
    - Mac OS
    
                > brew install ruby
                
    - Node Js 或其它 JavaScript runtime （CoffeeScript支持）
    
    
2. RubyGem

                > gem install jekyll
                
### 目录结构

- _config.yml 保存配置数据

- _draft 未发布的文章

- _includes 通过调用将其中的内容使用到文章或布局中

- _layouts 文章外的模板。不同文章可根据YAML头信息选择布局

- _posts 存放文章的地方，必须使用`YEAR-MONTH-DAY-title.MARKUP`

- _data 存放格式化的站点数据。自动加载.yml或.yaml

- _site 存放Jekyll转换完所生成的页面，最好将其放入.gitignore中

- _index.html, .html或.md 如果这些文件包含了YAML头文件，Jekyll自动转换。

### 预先定义的全局变量

- layout 指明使用layout文件，不需要拓展名。layout文件存放在_layouts中

- published 设置为false，则不发表该post

- category/categories 不将不同post放置在目录中，指定post属于哪类。一个post多类别，可以通过YAML list或者空格隔开

- tags 与categories相似，一个post可有多个tags，同样可用YAML list和空格

- date 该变量覆盖文件名日期，保证post的正确分类。格式为YYYY-MM-DD HH:MM:SS +/-TTTT

- 如果不常使用变量，则使用默认即可。default可在_config.yml中进行设置

### 发表文章

_posts目录是存放post的地方，文件主要是用Makrdown和HTML所转换的。所有posts都有YAML头信息。

- 在_posts目录下新建文件，文件名要求格式：YEAR-MONTH-DAY-title.MARKUP，例如2011-12-31-new-years-eve-is-awesome.md


## Problem Solution
1. 使用Jekyll Serve的时候，显示Could not find a JavaScript runtime.(ExecJS::RuntimeUnavailable)

                >  sudo apt-get install nodejs
		
2.  
    
## Tips

1. 代码高亮，可使用Pygments或者Rouge

2. 通过输入`jekyll serve`，用built-in development serve在本地浏览器预览生成的网页[http://localhost:4000/](http://localhost:4000/)。

3. 网站配置主要存储在`_config.yml`中

4. 头信息，即YAML。任何包含YAML头信息的文件，在Jekyll中都会被作为特殊文件处理。头信息应该放在最开始位置，而且用以下格式。在这部分里，可以加入很多变量，可应用在文件或者layouts中。

    - - -
    layout: post
    
    title: Blogging
    -- - -
    
5. 如果是UTF-8编码，加入BOM头文件
