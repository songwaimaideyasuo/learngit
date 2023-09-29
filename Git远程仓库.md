# 添加远程仓库
你在本地创建了一个Git仓库后，又想在GitHub创建一个Git仓库，并且让这两个仓库进行远程同步，这样，GitHub上的仓库既可以作为备份，又可以让其他人通过该仓库来协作。

首先，登陆GitHub，然后，在右上角找到“Create a new repo”按钮，创建一个新的仓库。在Repository name填入learngit，其他保持默认设置，点击“Create repository”按钮，就成功地创建了一个新的Git仓库。
![在这里插入图片描述](https://img-blog.csdnimg.cn/1e8d78114a0542dbbab317fe2dd3c60d.png)
我们根据GitHub的提示，在本地的learngit仓库下运行命令：
$ git remote add origin git@github.com:songwaimaideyasuo/learngit.git
![在这里插入图片描述](https://img-blog.csdnimg.cn/57bfd526f2124aff98424bd6772e080c.png)
注意：songwaimaideyasuo是我的用户名，替换成你的。

添加后，远程库的名字就是origin，这是Git默认的叫法，也可以改成别的，但是origin这个名字一看就知道是远程库。

下一步，就可以把本地库的所有内容推送到远程库上：
$ git push -u origin master
![在这里插入图片描述](https://img-blog.csdnimg.cn/4a1a6fb071954352ad3ea8cd6e7ae1c6.png)

当你第一次使用Git的clone或者push命令连接GitHub时，会得到一个SSH警告：
The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established.
RSA key fingerprint is xx.xx.xx.xx.xx.
Are you sure you want to continue connecting (yes/no)?
这是因为Git使用SSH连接，而SSH连接在第一次验证GitHub服务器的Key时，需要你确认GitHub的Key的指纹信息是否真的来自GitHub的服务器，输入yes回车即可。

Git会输出一个警告，告诉你已经把GitHub的Key添加到本机的一个信任列表里了：
Warning: Permanently added 'github.com' (RSA) to the list of known hosts.
这个警告只会出现一次，后面的操作就不会有任何警告了。

如果你实在担心有人冒充GitHub服务器，输入yes前可以对照GitHub的RSA Key的指纹信息是否与SSH连接给出的一致。

推送成功后，可以立刻在GitHub页面中看到远程库的内容已经和本地一模一样：
![在这里插入图片描述](https://img-blog.csdnimg.cn/3782bf3d19f94a6ebbb5143679c6293f.png)

从现在起，只要本地作了提交，就可以通过命令：
$ git push origin master
把本地master分支的最新修改推送至GitHub，现在，你就拥有了真正的分布式版本库！

删除远程库
如果添加的时候地址写错了，或者就是想删除远程库，可以用git remote rm <name>命令。使用前，建议先用git remote -v查看远程库信息：
$ git remote -v
![在这里插入图片描述](https://img-blog.csdnimg.cn/ddb33eaa18c24eb0b81933a7424cb052.png)
然后，根据名字删除，比如删除origin：
$ git remote rm origin
此处的“删除”其实是解除了本地和远程的绑定关系，并不是物理上删除了远程库。远程库本身并没有任何改动。要真正删除远程库，需要登录到GitHub，在后台页面找到删除按钮再删除。

小结：
把本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程。
由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。

## 从远程库克隆
现在，假设我们从零开发，那么最好的方式是先创建远程库，然后，从远程库克隆。

首先，登陆GitHub，创建一个新的仓库，名字叫gitskills，我们勾选Initialize this repository with a README，这样GitHub会自动为我们创建一个README.md文件。创建完毕后，可以看到README.md文件。

现在，远程库已经准备好了，下一步是用命令git clone克隆一个本地库：
$ git clone git@github.com:songwaimaideyasuo/gitskills.git
![在这里插入图片描述](https://img-blog.csdnimg.cn/b0975ecb09cc44e0a09790e8b395cf11.png)





