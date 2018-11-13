# Git
> 将已有的项目提交到Github
``` bash
1/$ git init   #在当前项目目录中生成本地git管理,并建立一个隐藏.git目录
2/$ git add .  #添加当前目录中的所有文件到索引
3/$ git commit -m "commit notes"  #提交到本地源码库，并附加提交注释
4/$ git remote add origin git@github.com:hcly3015/**.git  #提交远程github(**.git对应新建Github项目的Repository)
5/$ git push -u origin master  #把本地源码库push到github 别名为origin的远程项目中，确认提交
```

> 从GitHub克隆到本地
``` bash
$ git clone git@github.com:hcly3015/**.git
```

> 本地文件修改后提交命令
``` bash
1/$ git commit -a -m 'commit remark'  #提交到本地源码库，并附加提交注释
2/$ git push origin master            #把本地源码库push到github别名为origin的master分支远程项目中
```

> 删除命令
``` bash
$ git remote rm origin
```

> 合并分支
``` bash
假如我们现在在dev分支上，刚开发完项目，执行了下列命令
git add .
git commit -m 'devModify'
git push -u origin dev
然后我们要把dev分支的代码合并到master分支上 该如何？ 
首先切换到master分支上
git checkout master
如果是多人开发的话 需要把远程master上的代码pull下来
git pull origin master
如果是自己一个开发就没有必要了，为了保险期间还是pull
然后我们把dev分支的代码合并到master上
git merge dev
然后查看状态
git status
将合并的本地master分支推送到远程master
git push origin master
```

## 开发Vue项目
> 脚手架构建

安装node.js

安装cnpm(淘宝镜像：$ npm install -g cnpm --registry=https://registry.npm.taobao.org)

vue安装($ cnpm install vue)

1/安装vue-cli脚手架构建工具($ cnpm install -g vue-cli)

2/创建一个基于webpack模板的新项目(指定目录 $ vue init webpack my-project)


## vscode开发vue相关配置
> vscode配置建议
``` bash
{
	"files.autoSave": "afterDelay",
	"editor.tabSize": 2,
	"editor.detectIndentation": false,
	"prettier.singleQuote": true,
	"prettier.semi": false,
	"vetur.format.defaultFormatter.html": "js-beautify-html",
	"vetur.format.defaultFormatter.js": "vscode-typescript",
	"javascript.format.insertSpaceBeforeFunctionParenthesis": true,

  "editor.fontSize": 15,
  "editor.lineHeight": 24,
  "editor.fontLigatures": true,
}
插件
Chinese (Simplified) Language Pack for Visual Studio Code
Material Theme
Prettier - Code formatter
Prettier-Standard - JavaScript formatter
```

## PM2
> PM2相关命令
``` bash
全局安装 pm2 
$ npm install pm2 -g

更新
$ pm2 update

在项目中package.json中增加了一条 "pm2": "pm2 start processes.json"
在启动就直接输入如下命令
$ npm run pm2

$ pm2 stop [app-name|id]    #停止某一个进程，可以使用app-name或者id
$ pm2 stop all              #停止所有进程
$ pm2 restart all           #重启所有的进程
$ pm2 delete [app-name|id]  #删除并停止进程
$ pm2 delete all            #删除并停止所有进程
```

## phpStudy:一键安装nginx环境(下载phpStudy安装配置即可)
> nginx特点

1/基本Http服务，可以作为Http代理服务器和反向代理服务器，支持通过缓存加速访问，可以完成简单的负载均衡和容错，支持包过滤功能，支持SSL

2/高级Http服务，可以进行自定义配置，支持虚拟主机，支持URL重定向，支持网络监控，支持流媒体传输等

3/邮件代理服务器，支持IMAP/POP3代理服务功能，支持内部SMTP代理服务功能


## Xshell(下载安装Xshell)
> 利用Xshell连接云服务器地址发布项目
``` bash
1/$ yum install lrzsz  #(通过Xshell上传文件可以下载安装rz。在Xshell中运行此命令)
2/$ cd **              #目录(利用cd命令定位到需要的目录下)
3/$ rm -rf *           #(清空当前文件夹下所有的文件，注意当前文件夹目录，勿删错)
4/$ rz                 #(利用rz命令上传压缩包文件，或者执行拖动文件)
5/$ unzip backend20180505.zip  #(解压上传的压缩包)
6/$ rm -f backend20180505.zip  #(删除压缩包文件)
7/$ mv backend20180505/* ./    #(移出文件)
8/$ rm -rf backend20180505     #(删除目录backend20180505下的所有文件、子目录下的所有文件和目录、删除文件夹本身)
9/$ ll  #(显示信息)

$ vim /文件名   #编辑文件
$ Esc          #退出编辑状态
$ :wq          #保存并退出
$ Shift + zz   #保存并退出
```

## Nginx
> nginx部署vue打包项目
``` bash
1/找到nginx安装的目录，启动nginx.exe #(或者启动命令 $ cd E:\nginx-1.15.3\nginx-1.15.3。 $ start nginx)
2/$ tasklist /fi "imagename eq nginx.exe"  #查看nginx任务进程(ps:需要在安装的根路径下执行)
3/修改nginx配置文件，配置文件为conf下的nginx.conf,修改nginx.conf中的server配置片段，如下：
4/$ nginx -s reload  #(完成nginx配置后重新加载配置文件)
5/部署成功，浏览器地址：127.0.0.1:8190
```
``` bash
server {
  listen       8190;
  server_name  127.0.0.1;
  #charset koi8-r;
  #access_log  logs/host.access.log  main;
  root    "E:/hxx/github/vue2-admin/dist"; #vue项目的打包后的dist
  location / {
    try_files $uri $uri/ @router; #需要指向下面的@router否则会出现vue的路由在nginx中刷新出现404
    index  index.html index.htm;
  }
  #对应上面的@router，主要原因是路由的路径资源并不是一个真实的路径，所以无法找到具体的文件
  #因此需要rewrite到index.html中，然后交给路由在处理请求资源
  location @router {
    rewrite ^.*$ /index.html last;
  }
  location /api/ {
    proxy_pass http://127.0.0.1:8091; #对应api地址
    proxy_redirect     off;
    proxy_set_header   Host             $host;
    proxy_set_header   X-Real-IP        $remote_addr;
    proxy_set_header   X-Forwarded-For  $proxy_add_x_forwarded_for;
    proxy_next_upstream error timeout invalid_header http_500 http_502 http_503 http_504;
    proxy_max_temp_file_size   0;
    proxy_connect_timeout      90;
    proxy_send_timeout         90;
    proxy_read_timeout         90;
    proxy_buffer_size          64k;
    proxy_buffers              4 32k;
    proxy_busy_buffers_size    64k;
    proxy_temp_file_write_size 64k;
  }
}
```

## 其它相关地址

掘金
https://juejin.im/timeline

前端资料 
https://yuchengkai.cn/docs/zh/frontend/

Git教程
https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000

图标库
http://www.iconfont.cn

字体库
http://fontawesome.dashgame.com/
