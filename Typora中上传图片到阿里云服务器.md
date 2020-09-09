## 1.安装

> 还是老规矩，软件下载链接文末自取。

typora升级到最新版本：`version 0.9.86(beta)`

![img](https://pic2.zhimg.com/80/v2-7620718c2c25cd14c83529006d106491_720w.jpg)

picgo也升级到最新版本：`version2.2.2`

![img](https://pic4.zhimg.com/80/v2-dbcf6d6e6cc6845864647f8fd68f852b_720w.jpg)

## 2.配置

打开typora，点开左上角文件，选择**偏好设置**

1. 设置插入图片时为【上传图片】
2. 勾选【对本地位置的图片应用上述规则】
3. 在上传服务中选择“PicGo(app)”
4. 在路径中选择picgo安装目录**PicGo.exe**

![img](https://pic3.zhimg.com/80/v2-876350cd67a3e4ec1b00d3811e560d4a_720w.jpg)

点击下面的验证图片上传选项，上传成功！

上传的方法也很简单，将图片复制进去typora就会自动帮你上传了，你也可以右键点击上传图片。

![img](https://pic2.zhimg.com/v2-9032892f876b84ea4d01249cf41d7591_b.webp)

可以在【格式】->【图像】->【上传所有图片】

![img](https://pic1.zhimg.com/80/v2-2e8de68635d59c0b48beee86ce2974e4_720w.jpg)

### 当然，要是这么简单的话我肯定不会写成博客的，下面就带大家一起排排坑~

## 3.错误排查

### 3.1错误一：Failed to fetch

![img](https://pic4.zhimg.com/80/v2-b77c9f54231067b6f15f96f2352f3d23_720w.png)

这个错误一般是由**端口设置错误**造成的，至于我为什么知道，你看看log文件就懂了。打开picgo的log文件

![img](https://pic2.zhimg.com/80/v2-e48f1817723926a02dd68f50bb52e625_720w.jpg)

错误提示是端口繁忙。

`解决方法`：打开picgo设置，点击设置Server选项，**将端口改为36677端口**，这是picgo推荐的默认端口号，然后保存，成功。

![img](https://pic1.zhimg.com/80/v2-b0811fac0fe9dd226a4bb77ced36a5d0_720w.jpg)



不过有的时候，我们的老朋友Failed to fetch还是如约而至，打开端口设置一看，怎么变成了366771？？？？

问题在于端口冲突，如果你打开了多个picgo程序，就会端口冲突，**picgo自动帮你把36677端口改为366771端口**，导致错误。log文件里也写得很清楚。

![img](https://pic1.zhimg.com/80/v2-a72022194261330d93f1d43cf6166754_720w.jpg)

`解决方法`：**先把picgo中的端口设置改回36677，然后退出所有picgo程序**，再使用typora上传功能（会自动启动picgo程序）

### 3.2错误二：{"success",false}

![img](https://pic3.zhimg.com/80/v2-d189b7f9348acd7d86cf19539e07cb02_720w.png)



这个错误相信也有很多小伙伴遇到了，原因是**文件名冲突**了，如果你上传过一张image1.jpg的图片，再上传名称一样的图片就会失败，康康log文件(感谢日志！)里也写到了。

![img](https://pic3.zhimg.com/80/v2-345dc8f98f84701d937f5afb0caab5c2_720w.jpg)

办法也很简单，打开picgo设置，将【**时间戳重命名】打开**。如图所示：

![img](https://pic3.zhimg.com/80/v2-4ef72b9d2c2f5b0f21e4fa6128cafef2_720w.jpg)

再次上传文件，上传成功~

**授人以鱼不如授人以渔**，上面的三种情况解决方法教给大家了，但是错误总是千奇百怪层出不穷的，如果下次出现上传错误的提示，请大家找到picgo的log文件，自己查看问题的原因嗷

![img](https://pic2.zhimg.com/80/v2-8cd940aca4c0606ce17b4b1d798213d9_720w.jpg)