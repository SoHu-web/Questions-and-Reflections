## git push报错

### 错误信息

本地commit完push时出错

### 报错信息

~~~tex
fatal: The current branch master has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin master

To have this happen automatically for branches without a tracking
upstream, see 'push.autoSetupRemote' in 'git help config'.

~~~

### 报错原因

与远程仓库未设置关联

### 解决方法

第一种如上图中的提示：git push --set-upstream origin master。其中的origin是你在clone远程代码时，git为你创建的指向这个远程代码库的标签，它指向repository。为了能清楚了解你要指向的repository，可以用命令git remote -v进行查看。master是你远程的branch，可以用git branch -a查看所有分支，远程分支是红色的部分。然后确定好这两个值后，将值换掉即可。
另一种方法是：git push -u origin master。同样根据自己的需要，替换origin和master。

两个命令的区别是第一条命令是要保证你的远程分支存在，如果不存在，也就无法进行关联。而第二条指令即使远程没有你要关联的分支，它也会自动创建一个出来，以实现关联。

### 连接地址

[Git master branch has no upstream branch的解决](https://blog.csdn.net/benben_2015/article/details/78803753)

