# 安装Git

在Windows上安装Git
在Windows上使用Git，可以从Git官网直接下载安装程序，然后按默认选项安装即可。
安装完成后，在开始菜单里找到“Git”->“Git Bash”，蹦出一个类似命令行窗口的东西，就说明Git安装成功！
![在这里插入图片描述](https://img-blog.csdnimg.cn/195a29ffea664e56b827c72a46a99656.png)
安装完成后，还需要最后一步设置，在命令行输入：

```shell
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```
可以再输入$ git config user.name然后回车，如果设置成功了就会显示你刚刚设置的用户名，同理，可以用$ git config user.email来查看你设置的邮箱

## 创建版本库
版本库又名仓库，可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。

首先，选择一个合适的地方，创建一个空目录：

```powershell
$ mkdir learngit
$ cd learngit
$ pwd
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/2e84441bc80a4ca0b52d6a58835014ee.png)第二步，通过git init命令把这个目录变成Git可以管理的仓库：

```powershell
$ git init
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/76d5b6a02dd74eb68a6718d79fdc43d8.png)
当前目录下多了一个.git的目录，这个目录是Git来跟踪管理版本库的，没事千万不要手动修改这个目录里面的文件，不然改乱了，就把Git仓库给破坏了。（如果你没有看到.git目录，那是因为这个目录默认是隐藏的，用ls -ah命令就可以看见）

**把文件添加到版本库**
*windows注意*
千万不要使用Windows自带的记事本编辑任何文本文件。原因是Microsoft开发记事本的团队使用了一个非常弱智的行为来保存UTF-8编码的文件，他们自作聪明地在每个文件开头添加了0xefbbbf（十六进制）的字符，你会遇到很多不可思议的问题，比如，网页第一行可能会显示一个“?”，明明正确的程序一编译就报语法错误，等等，都是由记事本的弱智行为带来的。

现在我们编写一个HelloWorld.txt文件，内容如下：Hello World
一定要放到learngit目录下（子目录也行），因为这是一个Git仓库，放到其他地方Git再厉害也找不到这个文件。

第一步，用命令git add告诉Git，把文件添加到仓库：

```powershell
$ git add HelloWorld.txt
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/5859748a10df4e27b9725568bd61697a.png)

第二步，用命令git commit告诉Git，把文件提交到仓库：

```powershell
$ git commit -m "this is a .txt file"
```
-m后面输入的是本次提交的说明
![在这里插入图片描述](https://img-blog.csdnimg.cn/f44d460d95c4433dac95a2a830b2ffde.png)
执行成功后，1 file changed：1个文件被改动（我们新添加的HelloWorld.txt文件）；1 insertions：插入了1行内容（HelloWorld.txt有两行内容）。

为什么Git添加文件需要两步呢？
因为commit可以一次提交很多文件，所以你可以多次add不同的文件。

### 版本回退
修改HelloWorld.txt文件如下：
Hello World
Hello ZhangSan

然后尝试提交：

```powershell
$ git add HelloWorld.txt
$ git commit -m "append ZhangSan"
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/b574cb2d14bd45d093193ef2394b9493.png)
用git log命令查看：

```powershell
$ git log
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/53eaf5c0b4c541e6907a6dfdea978dad.png)
如果嫌输出信息太多，看得眼花缭乱的，可以试试加上--pretty=oneline参数：

```powershell
$ git log --pretty=oneline
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/06c17d439b124ee3a555a12653775629.png)

现在我们准备把readme.txt回退到上一个版本
首先，Git必须知道当前版本是哪个版本，在Git中，用HEAD表示当前版本，也就是最新的提交。
上一个版本就是HEAD^
上上一个版本就是HEAD^^
当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。

现在，我们要把当前版本append zhangsan回退到上一个版本，就可以使用git reset命令：

```powershell
$ git reset --hard HEAD^
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/550ecad4484047e08f07f9b008812124.png)
使用cat查看内容

```powershell
$ cat HelloWorld.txt
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/00d395b326ce43149eaa8fc21ec80d1d.png)
用git log再看看现在版本库的状态：

```powershell
$ git log
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/173320c8a1874e229b052a18705d3794.png)
最新的那个版本append ZhangSan已经看不到了。
想要回答最新的，只要上面的命令行窗口还没有被关掉，你就可以顺着往上找啊找啊，找到那个append ZhangSan的commit id是c674ddd，于是就可以指定回到未来的某个版本：
$ git reset --hard c674ddd
![在这里插入图片描述](https://img-blog.csdnimg.cn/fc2e77e62081490d85d134fd5c33f27a.png)
此外Git提供了一个命令git reflog用来记录你的每一次命令：

```powershell
$ git reflog
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/ab2ad543108e45d1a32864016c1f5ffe.png)
可以看到commit id

Git的版本回退速度非常快，因为Git在内部有个指向当前版本的HEAD指针，然后顺便把工作区的文件更新了。所以你让HEAD指向哪个版本号，你就把当前版本定位在哪。

#### 工作区和暂存区

工作区（Working Directory）
就是你在电脑里能看到的目录，比如我的learngit文件夹就是一个工作区。
版本库（Repository）
工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。
Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。
![在这里插入图片描述](https://img-blog.csdnimg.cn/a83fdbf992ed42aca0142a9f7f7f4468.jpeg)
我们再练习一遍，先对HelloWorld.txt做个修改：
Hello World
Hello ZhangSan
chat GPT
然后，在工作区新增一个LICENSE文本文件。
先用git status查看一下状态：

```powershell
$ git status
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/446fc59dcbc747d290db52c58dd47044.png)
Git非常清楚地告诉我们，HelloWorld.txt被修改了，而LICENSE还从来没有被添加过，所以它的状态是Untracked。

现在，使用两次命令git add，把readme.txt和LICENSE都添加后，用git status再查看一下：

```powershell
$ git status
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/1b30d1c2727846689c8e36665f508e3f.png)
git add命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行git commit就可以一次性把暂存区的所有修改提交到分支。

```powershell
$ git commit -m "understand how stage works"
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/45883441714f490ab20af1b80dbc7439.png)
一旦提交后，如果你又没有对工作区做任何修改，那么工作区就是“干净”的：

```powershell
$ git status
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/e03d41e7fa6f46209c5532e6ac2d336a.png)

##### 管理修改

为什么Git比其他版本控制系统设计得优秀？
因为Git跟踪并管理的是修改，而非文件。

第一步，对HelloWorld.txt做一个修改，比如加一行内容：
Hello World
Hello ZhangSan
chat GPT
Gpt is Generative Pre-Trained Transformer

然后，添加：
```shell
$ git add HelloWorld.txt
$ git status
```
再修改HelloWorld.txt：
Hello World
Hello ZhangSan
chat GPT
Gpt is Generative Pre-Trained Transformer，The AI big model is more like the human brain.

提交：

```powershell
$ git commit -m "GPT Readme"
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/e58d062c3387413e94daa1fa36d0969b.png)

再看看状态：

```shell
$ git status
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/0622684eb3db45f493865e703cfcc598.png)
怎么第二次的修改没有被提交？
第一次修改 -> git add -> 第二次修改 -> git commit
当你用git add命令后，在工作区的第一次修改被放入暂存区，准备提交，但是，在工作区的第二次修改并没有放入暂存区，所以，git commit只负责把暂存区的修改提交了，也就是第一次的修改被提交了，第二次的修改不会被提交。

提交后，用git diff HEAD -- HelloWorld.txt命令可以查看工作区和版本库里面最新版本的区别：

```powershell
$ git diff HEAD -- HelloWorld.txt 
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/da96abbbc87c4428bcfd1a7569aaeec8.png)
注意：+后面是版本库缺少的。

###### 撤销修改
git checkout -- file可以丢弃工作区的修改：

```powershell
$ git checkout -- HelloWorld.txt
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/d2089a8219ca4231bfadba65513ebd91.png)
git checkout -- file命令中的--很重要，没有--，就变成了“切换到另一个分支”的命令。

如果已经git add到暂存区了，在commit之前，你发现了这个问题。用git status查看一下，修改只是添加到了暂存区，还没有提交：
![在这里插入图片描述](https://img-blog.csdnimg.cn/b825c649de684e2caf3d6309c0f99906.png)
用命令git reset HEAD <file>可以把暂存区的修改撤销掉（unstage），重新放回工作区：

```powershell
$ git reset HEAD HelloWorld.txt
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/74c60f069c0447bebe4b7ebf298b857e.png)
git reset命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用HEAD时，表示最新的版本。
再用git status查看一下，现在暂存区是干净的，工作区有修改：
![在这里插入图片描述](https://img-blog.csdnimg.cn/cea308971833465b80c25b3944f9b909.png)

####### 删除文件
先添加一个新文件test.txt到Git并且提交：
![在这里插入图片描述](https://img-blog.csdnimg.cn/8ddd248d46b14ae79438848eaaa6e0b6.png)
如果你直接用rm命令删了：

```powershell
$ rm test.txt
```
这个时候，Git知道你删除了文件，因此，工作区和版本库就不一致了，git status命令会立刻告诉你哪些文件被删除了：

```powershell
$ git status
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/0a9bcf27ee1a41199bee4a7c3ae2c7cc.png)

要确实从版本库中删除该文件，那就用命令git rm删掉，并且git commit：
```powershell
$ git rm test.txt
$ git commit -m "remove test.txt"
```
现在，文件就从版本库中被删除了。![在这里插入图片描述](https://img-blog.csdnimg.cn/c62c095518d34079b2e807711c0c14c6.png)
小结：
git rm test.txt 相当于是删除工作目录中的test.txt文件,并把此次删除操作提交到了暂存区。
使用git checkout -- test.txt相当于是让工作目录test.txt恢复到暂存区中test.txt的状态,但是工作目录中test.txt已经被删除,无法找到文件来再次删除所以报错,必须先使用git reset head test.txt在暂存区中将删除操作丢弃,然后在git checkout -- test.txt就是直接将工作目录中test.txt恢复到版本库中的状态。