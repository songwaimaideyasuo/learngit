## GitHub的使用
我们一直用GitHub作为免费的远程仓库，如果是个人的开源项目，放到GitHub上是完全没有问题的。其实GitHub还是一个开源协作社区，通过GitHub，既可以让别人参与你的开源项目，也可以参与别人的开源项目。

在GitHub上，利用Git极其强大的克隆和分支功能，真正可以自由参与各种开源项目了。

下面我们来参与一个开源项目：
比如人气极高的bootstrap项目，这是一个非常强大的CSS框架，你可以访问它的项目主页https://github.com/twbs/bootstrap，点“Fork”就在自己的账号下克隆了一个bootstrap仓库
![在这里插入图片描述](https://img-blog.csdnimg.cn/238249d8a9bd4c85bdf4dc3bb6c2b459.png)

然后，从自己的账号下clone：
git clone git@github.com:songwaimaideyasuo/bootstrap.git


一定要从自己的账号下clone仓库，这样你才能推送修改。如果从bootstrap的作者的仓库地址git@github.com:twbs/bootstrap.git克隆，因为没有权限，你将不能推送修改。
现在他们的关系就像下图显示的那样：
![在这里插入图片描述](https://img-blog.csdnimg.cn/313423bf793644f5b55466037c4bc9e1.png)

如果你想修复bootstrap的一个bug，或者新增一个功能，立刻就可以开始干活，干完后，往自己的仓库推送。

如果你希望bootstrap的官方库能接受你的修改，你就可以在GitHub上发起一个pull request。当然，对方是否接受你的pull request就不一定了。


**小结**
在GitHub上，可以任意Fork开源仓库；
自己拥有Fork后的仓库的读写权限；
可以推送pull request给官方仓库来贡献代码。

