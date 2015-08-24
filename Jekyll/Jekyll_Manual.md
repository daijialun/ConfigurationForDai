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

## Problem Solution
1. 使用Jekyll Serve的时候，显示Could not find a JavaScript runtime.(ExecJS::RuntimeUnavailable)

                >  sudo apt-get install nodejs
		
2.  
    
## Tips

1. 代码高亮，可使用Pygments或者Rouge

2. 通过输入`jekyll serve`，用built-in development serve在本地浏览器预览生成的网页[http://localhost:4000/](http://localhost:4000/)。

3. 网站配置主要存储在`_config.yml`中
