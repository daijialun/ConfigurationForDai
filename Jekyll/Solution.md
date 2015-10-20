# Jekyll使用过程的问题解决

- {site.url}变量位于_config.yml中，需要修改为自己的域名，即url: "http://daijialun.github.io"

- jekyll serve模式下，修改_config.yml不会立即生效，需要关闭serve后，重新开启，修改才会生效

- 在blog中添加图片（必须先修改_config.yml中url变量），使用
    
            ![screenshot]({{site.url}}/assets/sreenshot.jpg)
            
- 出现` Error:  Address already in use - bind(2)`的情况

    - 使用`netstat -tanlp | grep '4000'`，检测端口号为4000的端口状态；例如出现0.0.0.0:4000 Listen状态，显示3007/Ruby
    - 再使用`kill **`杀死进程；即 kill -9 3007