对于经常写文章的人来说，图片上传是个很让人头疼的问题，现在的很多图库都不能使用了，现在用typora自带的图片上传功能来尝试一下

步骤为偏好设置 >> 下载或更新>>打开配置文件 >>验证图片上传

![image-20201021204721559](https://i.loli.net/2020/10/21/AZxoqXRgdDQ5k4I.png)

下载完成后，去smhttps://sm.ms/注册个账号，这是一个云存储服务器，注册送你免费5G的容量，注册完账号后，点击打开配置文件，会蹦出来一个config.json文件，把下面的复制进去，然后改下token，

```
{
  "picBed": {
    "uploader": "smms", // 代表当前的默认上传图床为 SM.MS,
    "smms": {
      "token": "自己生成的token" //一定要换
    }
  },
  "picgoPlugins": {} // 为插件预留
}

```

token是在https://sm.ms/网站里面生成的，点击generate secret token就能生成一个新的token

![image-20201021205605421](https://i.loli.net/2020/10/21/NYXhtZQnE8p9zxM.png)

配置好以后点击验证图片上传选项，显示成功上传图片并获得新的url就是配置成功了

![image-20201021205839673](https://i.loli.net/2020/10/21/JYoLlO9nxpPt7rN.png)