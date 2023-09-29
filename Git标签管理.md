#  创建标签

在Git中打标签非常简单，首先，切换到需要打标签的分支上：
$ git branch
$ git checkout master
![在这里插入图片描述](https://img-blog.csdnimg.cn/10c173961fbb425d8e1de81be30422e3.png)

然后，敲命令git tag <name>就可以打一个新标签：
$ git tag v1.0
可以用命令git tag查看所有标签：
$ git tag
![在这里插入图片描述](https://img-blog.csdnimg.cn/359b7aa3c26e4c1887db66dd74b19415.png)
默认标签是打在最新提交的commit上的。

有时候，如果忘了打标签，比如，现在已经是周五了，但应该在周一打的标签没有打，怎么办？
方法是找到历史提交的commit id，然后打上就可以了：
$ git log --pretty=oneline --abbrev-commit
![在这里插入图片描述](https://img-blog.csdnimg.cn/2c554e95a55b4452b07e6fe6e3140dc7.png)

比方说要对add China这次提交打标签，它对应的commit id是446f141，敲入命令：
$ git tag v0.9 446f141
再用命令git tag查看标签：
$ git tag
![在这里插入图片描述](https://img-blog.csdnimg.cn/347b0fb87c3a4a0c91b08fa8947f69cc.png)

标签不是按时间顺序列出，而是按字母排序的。可以用git show <tagname>查看标签信息：
$ git show v0.9
![在这里插入图片描述](https://img-blog.csdnimg.cn/e6bccd3af7ab4d38bb73596195da9342.png)
可以看到，v0.9确实打在add merge这次提交上。

还可以创建带有说明的标签，用-a指定标签名，-m指定说明文字：
$ git tag -a v0.1 -m "version 0.1 released" fa6d0e7
用命令git show <tagname>可以看到说明文字：
$ git show v0.1
![在这里插入图片描述](https://img-blog.csdnimg.cn/383dcab54f9740f79a277b7ec50e04f2.png)

##  操作标签

如果标签打错了，也可以删除：
$ git tag -d v0.1
![在这里插入图片描述](https://img-blog.csdnimg.cn/23b7757097974dba9f71299767ea3865.png)
因为创建的标签都只存储在本地，不会自动推送到远程。所以，打错的标签可以在本地安全删除。

如果要推送某个标签到远程，使用命令git push origin <tagname>：
$ git push origin v1.0
![在这里插入图片描述](https://img-blog.csdnimg.cn/b766703e2b4d4996886924d480b3650b.png)

如果标签已经推送到远程，要删除远程标签就麻烦一点，先从本地删除：
$ git tag -d v0.9
然后，从远程删除。删除命令也是push，但是格式如下：
$ git push origin :refs/tags/v0.9
![在这里插入图片描述](https://img-blog.csdnimg.cn/871f0470e5c94179bf7d59d073a412a2.png)

这时候标签就从远程库删除了
![在这里插入图片描述](https://img-blog.csdnimg.cn/b6bb0ebb371f4b979fb27c859c067657.png)

**小结：**
查看分支 git branch

查看远程分支 git branch -r

查看所有分支 git branch -a

删除本地分支 git branch -d 分支名  比如 git branch -d dev

强制删除本地分支 git branch -D 分支名  

删除远程分支 git push 远程仓库名 :分支名     比如  git push origin :dev

查看标签 git tag

创建标签 git tag -a 标签名 -m '描述'

删除本地标签 git tag -d 标签名

强制删除本地标签 git tag -D 标签名

删除远程标签 git push 远程仓库名 :标签名