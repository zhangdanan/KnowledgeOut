# 1.常规设置

### 缕清思路

网上关于这方面的文章已经挺多的了，但是每次要配置的时候，还是要靠搜索引擎找半天才搞定，索性自己记录一下。之前我遇到了下面几种情况：

- 自己github上项目，即要在自己的Mac上能提交代码，也要在公司的Mac上能提交代码。
- 公司的Mac上，要能往公司自己的git服务器上对应项目提交代码，也要能往自己github上的项目提交代码。
- 别人github上项目，在自己的Mac上能往上面提交代码。



解决上面的各种情况之前，先来说一下SSH Key是咋回事。**公钥认证**，是使用一对加密字符串，一个称为**公钥（public key）**，任何人都可以看到其内容，用于加密；另一个称为**密钥（private key）**，只有拥有者才能看到，用于解密。通过公钥认证可实现SSH免密码登陆，git的SSH方式就是通过公钥进行认证的。

也就是说，我们在自己的电脑上生成一对key，把其中的`public key`配置到git服务器的项目上，`private key`在自己的电脑上配置好，这时就是可以在自己的电脑上往git服务器上的那个项目提交代码了。哪怕你没有一个git帐号，但是能把这个`public key`配置到git服务器的项目上，比如你用两个鸡腿跪求别人把你的`public key`放上去，这时你照样能往上面提交代码。

现在来看一下上面的那几种情况需要怎么配置：

- 需要在自己的Mac上生成一对SSH Key，配置到自己的github项目上，在公司的Mac上也要生成一对SSH Key配置到自己的github项目上。
- 公司的Mac上，生成一对SSH key配置在公司自己的git服务器对应的项目上，再生成一个对SSH key配置在自己的github项目上。
- 在自己的Mac上生成一对SSH Key，配置在对方的github项目上。

### 开始配置

下面都拿github举例子了，毕竟大家都在用😁

#### 在github上的项目配置SSH Key中的`public key`

在github上创建一个`repository`后，在`Settings`中会找到如下项：

[![img](http://shinancao.cn/images/Git-DeployKeys.png)](http://shinancao.cn/images/Git-DeployKeys.png)

这个`Deploy keys`就是配置可以往该项目上提交代码的`public key`，可以添加多个。

对于`public key`的配置就是这么简单，但是要注意，一个`public key`只能给一个`repository`用。

#### 在Windows上配置SSH Key中的`private key`

当往github的项目上提交代码时，github需要知道你电脑上有没有和那些`Deploy keys`中某个`public key`配对的`private key`。接下来就是配置怎样找到这个`private key`。

- 生成1个SSH Key:

```
$ ssh-keygen -t rsa -C "youremail@xxx.com"
```

按回车后：

```
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/Shinancao/.ssh/id_rsa): id_rsa_TestSSH_github(取个名字)
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in 
id_rsa_TestSSH_github.
Your public key has been saved in 
id_rsa_TestSSH_github.pub.
```

最好每次生成时都给SSH Key取个名字，这样后面在管理时自己也一目了然。我这里的格式是`id_rsa_项目名_git提供方`，我生成的所有key都遵循这个规则命名。建议你也有你自己的一种命名方式，并且保持统一。如果不取名字，默认的是`id_rsa`，如果后面生成时不命名，会把这个覆盖掉。密码可以不设置，免得每次提交时还要输入一次，安全性自己衡量吧。第一次生成key时，会在`~`目录下创建一个`.ssh`目录。

```
$ cd ~/.ssh
$ ls
```

- 把`id_rsa_TestSSH_github.pub`添加到github对应的项目的`Deploy keys`中。

[![img](http://shinancao.cn/images/Git-Add-DeployKeys.png)](http://shinancao.cn/images/Git-Add-DeployKeys.png)

- ssh服务器默认是去找`id_rsa`，现在需要把这个key添加到`ssh-agent`中，这样ssh服务器才能认识`id_rsa_TestSSH_github`。

```
$ ssh-add -K ~/.ssh/id_rsa_TestSSH_github
```

这里为什么加上了一个`-K`参数呢？因为在Mac上，当系统重启后会“忘记”这个密钥，所以通过指定`-K`把SSH key导入到密钥链中。

查看添加结果：

```
$ ssh-add -l
```

- 创建本地的配置文件 ~/.ssh/config，编辑如下：

```
Host TestSSH.github.com
	HostName github.com
	User git
	PreferredAuthentications publickey
	IdentityFile ~/.ssh/id_rsa_TestSSH_github
Host YourProjectName.gitlab.com
	HostName gitlab.com
	User git
	PreferredAuthentications publickey
	IdentityFile ~/.ssh/id_rsa_YourProjectName_gitlab
```

Host的名字可以随意取，我这边按照的规则是`项目名.git服务器来源`，接下来会用到这个名字。测试是否配置正确：

```
$ ssh -T git@TestSSH.github.com (就是刚刚你给Host取的名字)
```

敲一下回车，如下出现下面的提示就连接成功了：

```
Hi shinancao/TestSSH! You've successfully authenticated, but GitHub does not provide shell access.
```

一定要注意哦，帐号名称/项目名称，如果这个key没有连接成功，它有可能提示的是别的key的。

- 修改github项目配置，使项目本身能关联到使用的key。

如果你在之前已经把项目clone到本地了，有两种解决方法：

(1) 打开`项目目录/.git/config`，将[remote “origin”]中的url中的`github.com`修改为`TestSSH.github.com`，就是你在第4步中给Host取的那个名字。如下：

```
remote "origin"]
	url = git@TestSSH.github.com:shinancao/TestSSH.git
	fetch = +refs/heads/*:refs/remotes/origin/*
```

(2) 也可以在提交时修改

```
$ git remote rm origin
$ git remote add origin git@TestSSH.github.com:shinancao/TestSSH.git
```

如果还没有clone到本地，则在clone时可以直接将`github.com`改为`TestSSH.github.com`，如下：

```
$ git clone git@TestSSH.github.com:shinancao/TestSSH.git
```

到此，就可以Happy Coding啦😄，可以push一次试试~

### github用户设置中的SSH Key

细心的小伙伴可能已经注意到了，在用户设置中也有一个SSH Keys的配置，这块添加的key是来设置一个电脑上默认使用的key的。每创建一个`repository`都弄一次`Deploy Keys`是挺麻烦的。

[![img](http://shinancao.cn/images/Git-Global-SSH.png)](http://shinancao.cn/images/Git-Global-SSH.png)

github默认找的是`id_rsa`这对密钥，所以此处要添加到github上的就是`id_rsa.pub`的内容。这对密钥一样存在于`~/.ssh`中，而且无需在`config`中设置。

先看一下`id_rsa`是否已经在`ssh-agent`中了：

```
$ ssh-add -l
```

如果不在要添加进去：

```
$ ssh-add -K ~/.ssh/id_rsa
```

测试是否能连接成功：

```
$ ssh -T git@github.com
```

敲一下回车，如果结果如下则成功了：

```
Hi shinancao! You've successfully authenticated, but GitHub does not provide shell access.
```

注意哦，这里只有用户名！没有跟着项目名了~ 配置完成后，就是可以轻松的创建`repository`，然后clone到本地，自由自在的往上面`push`代码啦~

### 配置邮箱和用户名

配置邮箱和用户名是用来干啥的呢？就是记录每一次`commit`的用户和与之关联的邮箱。可以在电脑上配置一个全局的`user.name`和`user.email`，也可以针对不同的`repository`配置不同的`user.name`和`user.email`。

[![img](http://shinancao.cn/images/Git-UserName.png)](http://shinancao.cn/images/Git-UserName.png)

配置全局的`user.name`和`user.email`：

```
$ git config --global user.name "your name"
$ git config --global user.email "your email"
```

查看结果：

```
$ git config --global user.name
$ git config --global user.email
```

位置在`~/.gitconfig`文件中。

在做这块的测试时，我发现了一个很有意思的事情，对于github，即使我随意设置了一个全局的`name`，但最后提交完，显示的还是我github的用户名。当取消了global的设置，只针对某个`repository`设置，则github上可以显示我设置的了。

如果同时设置了全局的，和针对某个`repository`的，则优先使用全局的。那要单独给每个`repository`设置，要先取消全局的设置。

```
$ git config --global --unset user.name
$ git config --global --unset user.email
```

然后进入到项目目录下设置：

```
$ git config user.email "your name"
$ git config user.email "your email"
```

查看结果：

```
$ git config user.name
$ git config user.email
```

位置在`项目目录/.git/config`文件中。

### HTTPS的方式提交代码

通过https的方式clone url，然后再以https的方式提交代码，我觉得就是正常的使用帐号和密码去操作。这种方式需要你知道项目拥有者的帐号和密码，而且在每次`commit`时都要输入用户名和密码。显然不方便啦，尤其是你要参与到别人的项目中去开发，人家总不能把帐号名和密码都给你吧😂。

### 参考链接

- https://nicejade.github.io/2016/01/27/ssh-mac.html
- http://k99k.com/2015/github-multiple-ssh-key/
- https://favoorr.github.io/2015/05/27/git-more-sshkeys-more-host/

> 转载请注明出处：
>
> 作者：意林
>
> 原文链接：http://shinancao.github.io/2016/12/18/Programming-Git-1/

![image-20200404142928914](C:\Users\sloth\AppData\Roaming\Typora\typora-user-images\image-20200404142928914.png)

https://www.cnblogs.com/hugechuanqi/p/10786561.html

http://shinancao.cn/2016/12/18/Programming-Git-1/

http://k99k.com/2015/github-multiple-ssh-key/