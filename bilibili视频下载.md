作者：见长
链接：https://www.zhihu.com/question/41367609/answer/625032725
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。



## ***You-get\***

![img](https://pic3.zhimg.com/v2-e4ce366d74730d7e3b56b492e68c001e_b.jpg)![img](https://pic3.zhimg.com/80/v2-e4ce366d74730d7e3b56b492e68c001e_720w.jpg)

You-get是GitHub上的一个项目，也可以说是一个命令行程序，帮助大家下载大多主流网站上的视频、图片及音频。

支持的网站非常多，我们可以先来看一部分。

国外网站：

![img](https://pic4.zhimg.com/v2-ccb853bd91f5bc1da6f5a432235b470f_b.jpg)![img](https://pic4.zhimg.com/80/v2-ccb853bd91f5bc1da6f5a432235b470f_720w.jpg)

国内网站：

![img](https://pic4.zhimg.com/v2-e99e4467cb09e5aed2127a373484010b_b.jpg)![img](https://pic4.zhimg.com/80/v2-e99e4467cb09e5aed2127a373484010b_720w.jpg)

还有很多很多...

下面我们就一步步来演示如何使用。



第一步：下载安装python3.7（最新）

第二步：按住键盘上的“win+R”键，在打开的运行窗口中输入“cmd”，点击确定。

![img](https://pic4.zhimg.com/v2-9d4785c71522257846ffde94eb9671a7_b.jpg)![img](https://pic4.zhimg.com/80/v2-9d4785c71522257846ffde94eb9671a7_720w.jpg)

![img](https://pic1.zhimg.com/v2-ddf3833235db17db41e3bfb6c807d248_b.jpg)![img](https://pic1.zhimg.com/80/v2-ddf3833235db17db41e3bfb6c807d248_720w.jpg)

第三步：

在箭头所指处输入下方内容，点击enter键，安装you-get工具。

pip3 install you-get

![img](https://pic4.zhimg.com/v2-3bc69db3e89d96f35fa708fbee514d27_b.jpg)![img](https://pic4.zhimg.com/80/v2-3bc69db3e89d96f35fa708fbee514d27_720w.jpg)

接着输入下方内容，点击enter键，升级you-get工具。

pip3 install --upgrade you-get

然后会有提示让你输入下方内容。

python -m pip install --upgrade pip

![img](https://pic4.zhimg.com/v2-34e367c7b636898bc6f32204b56f9f23_b.jpg)![img](https://pic4.zhimg.com/80/v2-34e367c7b636898bc6f32204b56f9f23_720w.jpg)



第四步：其实到这里，基本就完成操作了...没错就是这么简单。

那么，如何下载呢？就是复制视频链接（或音乐、图片链接）再粘贴就好了...没错就是这么简单...

具体方式是：

打开想要下载的视频，复制链接。

比如复制一个B站视频的链接：

[https://www.bilibili.com/video/av44291718](https://link.zhihu.com/?target=https%3A//www.bilibili.com/video/av44291718)

在命令行工具中输入“you-get 视频链接”点击“enter”键就可以下载了。

![img](https://pic2.zhimg.com/v2-076eb4b21b7d2dd1bea3a600a7f6e165_b.jpg)![img](https://pic2.zhimg.com/80/v2-076eb4b21b7d2dd1bea3a600a7f6e165_720w.jpg)

速度为9MB/s，上一次体验到这么高的速度还是...好吧没有上一次。

再来一个优酷视频链接：

首先我们输入 you-get -i 视频链接

![img](https://pic2.zhimg.com/v2-8d2b4f6cc95778cb8494bd2bd0ee00f1_b.jpg)![img](https://pic2.zhimg.com/80/v2-8d2b4f6cc95778cb8494bd2bd0ee00f1_720w.jpg)

注意这里多了一个“-i”，加了它就可以先预览下载的画质选择，可以看到有超清、高清、标清和渣清。

比如我们要下载高清的，可以看到它最后有个内容是：

you-get --format=mp4hd URL

我们把URL替换成视频链接，输入，enter，就可以下载高清画质的了。

![img](https://pic1.zhimg.com/v2-fdef22836d73227b888945f1fd2fc700_b.jpg)![img](https://pic1.zhimg.com/80/v2-fdef22836d73227b888945f1fd2fc700_720w.jpg)

这次的速度达到了11MB/s，没想到记录这么快就被打破了。

下载的文件在左侧的文件目录里，箭头所指处。

![img](https://pic1.zhimg.com/v2-ecc3d58f10bcfcc3e6813600b41d0710_b.jpg)![img](https://pic1.zhimg.com/80/v2-ecc3d58f10bcfcc3e6813600b41d0710_720w.jpg)