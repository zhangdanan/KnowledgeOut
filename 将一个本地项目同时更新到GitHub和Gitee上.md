## 强制同步

从`Github`上面直接导入的仓库可以使用强制同步

![image-20200909180018978](C:\Users\m1885\Desktop\image-20200909180018978.png)

## 多次推送

1. 使用命令来将本地项目和`Github/Gitee`上面项目进行关联

   ```
   git remote add gitee/github 项目地址
   ```

2. 配置本地项目的`.git`里面的`config`文件，将`Github`和`Gitee`的项目地址分别放入一个`remote`里面，最好将原始的`remote`的名字也改掉，如下。

   ```
   [core]
   	repositoryformatversion = 0
   	filemode = false
   	bare = false
   	logallrefupdates = true
   	symlinks = false
   	ignorecase = true
   [remote "github"]
   	url = github项目地址
   	fetch = +refs/heads/*:refs/remotes/origin/*
   [remote "gitee"]
   	url = gitee项目地址
   	fetch = +refs/heads/*:refs/remotes/origin/*
   [branch "master"]
   	remote = origin
   	merge = refs/heads/master
   ```

3. 推送代码时，对两个仓库分别执行一次

   ```
   git push github master
   
   git push gitee master
   ```

## 一次推送

1. 输入命令将`GitHub`项目地址和`Gitee`项目地址添加到本地项目的一个`remote`里面。

   ```
   git remote set-url --add origin gitee项目地址/github项目地址
   ```

2. 通过修改本地项目`.git`里面的`config`配置文件。如下。

   ```
   [core]
   	repositoryformatversion = 0
   	filemode = false
   	bare = false
   	logallrefupdates = true
   	symlinks = false
   	ignorecase = true
   [remote "origin"]
   	url = github项目地址
   	url = gitee项目地址
   	fetch = +refs/heads/*:refs/remotes/origin/*
   [branch "master"]
   	remote = origin
   	merge = refs/heads/master
   ```

3. 推送时，只需要执行一条命令

   ```
   git push
   ```

## 遇到的问题

1. 如果遇到以下问题

   ```
   xxxxx@DESKTOP-LB4I5JU MINGW64 ~/Desktop/xxxxxx (master)
   $ git push -u origin master
   To github.com:xxxxxxxxx/xxxxxx.git
    ! [rejected]        master -> master (fetch first)
   error: failed to push some refs to 'github.com:xxxxxxxxx/xxxxxx.git'
   hint: Updates were rejected because the remote contains work that you do
   hint: not have locally. This is usually caused by another repository pushing
   hint: to the same ref. You may want to first integrate the remote changes
   hint: (e.g., 'git pull ...') before pushing again.
   hint: See the 'Note about fast-forwards' in 'git push --help' for details.
   Warning: Permanently added the ECDSA host key for IP address 'xxx.xxx.xxx.xxx' to the list of known hosts.
   To gitee.com:xxxxxxx/xxxxxx.git
    ! [rejected]        master -> master (fetch first)
   error: failed to push some refs to 'gitee.com:xxxxxxx/xxxxxx.git'
   hint: Updates were rejected because the remote contains work that you do
   hint: not have locally. This is usually caused by another repository pushing
   hint: to the same ref. You may want to first integrate the remote changes
   hint: (e.g., 'git pull ...') before pushing again.
   hint: See the 'Note about fast-forwards' in 'git push --help' for details.
   
   ```

2. 这个时候你只需要一条命令即可

   ```
   git pull
   ```

3. 然后再进行推送本地代码

   ```
   git add .
   git commit -m""
   git push
   ```

   

   > https://www.cnblogs.com/poloyy/p/12215199.html

