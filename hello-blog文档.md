# 1、搭建前准备

··

后端管理：https://github.com/byteblogs168/hello-blog-admin

前端主题：https://github.com/byteblogs168/theme-default

# 2、下载后端代码到本地，打开application.yml，修改数据库信息

后端项目自带SQL脚本
datasource:
  name: helloblog
  url: jdbc:mysql://***.***.***.***:3306/helloblog?useSSL=false&characterEncoding=utf8
  username: root
  password: ***

# 3、运行后端代码，默认运行在8086端口

# 4、打开后端管理系统

npm install --registry=https://registry.npm.taobao.org

# 5、打开项目根目录中的vue.config，修改代理设置

proxy: {
[process.env.VUE_APP_BASE_API]: {
    target: `http://127.0.0.1:8086/api/hello-blog-service`,
    changeOrigin: true,
    pathRewrite: { '^/api/blog': '/' }
  }
}

# 6.、启动后端管理系统

vue-cli-service serve

# 7、进入到页面，鼠标单击，使用GitHub登录，第一次登录则默认为管理员

# 8、设置七牛云SDK账号密码，图片等信息默认使用七牛云，后期会加入阿里云，没有七牛云的用户，可暂时跳过，需要时再进行设置

新建公有空间，私有空间不方便后期使用


填写七牛云空间信息



# 9、前端配置

打开下载好的前端项目进行编译


npm install --registry=https://registry.npm.taobao.org
打开根目录中的vue.config修改项目api访问地址
proxy: {
  // 配置多个代理(配置一个 proxy: 'http://localhost:4000' )
[process.env.VUE_APP_BASE_API]: {
    target: `http://127.0.0.1:8086/api/hello-blog-service`,
    changeOrigin: true,
    pathRewrite: { "^/api/blog": "/" }
  }
}

# 10、运行前端项目

vue-cli-service serve

# 11、访问博客http://localhost:8002

 



 

# 12、目前博客还是空的，可以在后端进行文章的添加

 



# 13、发布博文，随后到前端进行查看

 



# 14、到这里，博文搭建成功，但还只是本地的测试，还需要发布到云服务器之上

# 15、部署后端到服务器

配置Maven打包命令
clean package -Dmaven.test.skip=true




运行Maven编译之后，找到项目存放目录，进入到target
将helloblog-v1.0.1-Alpha.jar上传到服务器之中
使用如下命令运行后端项目
nohup  java -jar helloblog-v1.0.1-Alpha.jar >catalina.out 2>&1 &16
15、部署管理系统与前端页面到到服务器

打开管理系统项目，输入如下命令
编译完成后，会在项目根目录中生成一个dist目录
vue-cli-service build
打开前端项目，输入如下命令
vue-cli-service build
新建文件夹用于保存页面
#将管理系统编译后的dist文件夹中的内容上传到此文件夹
mkdir -p /usr/lcoal/helloblog/admin
#将前端编译后的dist文件夹中的内容上传到此文件夹
mkdir -p /usr/lcoal/helloblog/front
使用Nginx进行反向代理(CnetOS7安装Nginx)
当前nginx安装在/usr/local/nginx中
vim /usr/local/nginx/conf/nginx.conf
server {
   listen       80;
   location /admin {
       root    /usr/local/hellobolg;
        index  index.html index.htm;
     } # 配置后端访问地址

     location / {
        root  /usr/local/hellobolg/front;
        index index.html index.htm;
     } # 配置前端访问地址
     
     location ^~ /api/blog {
        index  index.html index.htm index.php;
        index  proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        index  proxy_set_header Host $host;
        index  proxy_set_header X-Real-IP $remote_addr;
        proxy_pass http://localhost:8086/api/hello-blog-service; #后端服务器，配置upstream即可  
      }
  }
配置完成后，访问服务器查看是否配置成功







————————————————
版权声明：本文为CSDN博主「青涩知夏」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_41098163/article/details/102876093