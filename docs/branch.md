## 分支

> 使用分支意味着你可以把你的工作从开发主线上分离开来， 以免影响开发主线。也正因为这一特性，使得 Git 从众多版本控制系统中脱颖而 出。 为何 Git 的分支模型如此出众呢? Git 处理分支的方式可谓是难以置信的轻量，创建新分支这一操作几乎能 在瞬间完成，并且在不同分支之间的切换操作也是一样便捷。 与许多其它版本控制系统不同，Git 鼓励在工作流 程中频繁地使用分支与合并，哪怕一天之内进行许多次。

## 分支简介

> Git 保存的不是文件的变化或者差异，而是一系列不同时刻的文件快照。

[参考文章](https://www.jianshu.com/p/893f159e28b0)

### 分支创建

`git branch testing`

![](http://ww1.sinaimg.cn/large/006t9e3Igy1fuxwiznn4gj31no0p8tcf.jpg)

Git 又是怎么知道当前在哪一个分支上呢? 也很简单，它有一个名为 HEAD 的特殊指针。
![](http://ww1.sinaimg.cn/large/006t9e3Igy1fuxwkixwqej31om0yadj0.jpg)

### 分支切换

`git checkout testing`

HEAD 指向当前所在的分支

![](http://ww1.sinaimg.cn/large/006t9e3Igy1fuxwlzay9fj31ri0zu0vy.jpg)

再提交一次

![](http://ww1.sinaimg.cn/large/006t9e3Igy1fuxwn8a2ibj31oa0p476p.jpg)

HEAD 分支随着提交操作自动向前移动

`git checkout master`

![](http://ww1.sinaimg.cn/large/006t9e3Igy1fuxwo4bumsj31mm0powgw.jpg)

 检出时 HEAD 随之移动。

 这条命令做了两件事。 一是使 HEAD 指回 master 分支，二是将工作目录恢复成 master 分支所指向的快照内容。 

 再稍微做些修改并提交:

 ![](http://ww1.sinaimg.cn/large/006t9e3Igy1fuxwuj51zkj31hu0wqmzo.jpg)

 运行 `git log --oneline --decorate --graph --all`，它会输出你的提交历史、各个分支的指向以及项目的分支分叉情况。

 你可以在不同分支间不断地来回切换和工作，并在时机成熟时将它们合并起来。 而所有这些工作，你需要的命令只有 `branch`、`checkout` 和 `commit`。

 ## 分支的新建与合并

 让我们来看一个简单的分支新建与分支合并的例子，实际工作中你可能会用到类似的工作流。 你将经历如下步 骤:
1. 开发某个网站。
2. 为实现某个新的需求，创建一个分支。
3. 在这个分支上开展工作。

正在此时，你突然接到一个电话说有个很严重的问题需要紧急修补。 你将按照如下方式来处理:

1. 切换到你的线上分支(production branch)。
2. 为这个紧急任务新建一个分支，并在其中修复它。
3. 在测试通过之后，切换回线上分支，然后合并这个修补分支，最后将改动推送到线上分支。 4. 切换回你最初工作的分支上，继续工作。

### 新建分支

- 假设你正在你的项目上工作，并且已经有一些提交。

![](http://ww1.sinaimg.cn/large/006t9e3Igy1fuxx0sp2woj31mq0ki0uz.jpg)

- 现在，你已经决定要解决你的公司使用的问题追踪系统中的 #53 问题。 想要新建一个分支并同时切换到那个分
支上，你可以运行一个带有 `-b` 参数的 `git checkout` 命令:

`git checkout -b iss53`

![](http://ww1.sinaimg.cn/large/006t9e3Igy1fuxx2ad1qjj31qk0vsq60.jpg)

- 你继续在 #53 问题上工作，并且做了一些提交。 在此过程中，iss53 分支在不断的向前推进，因为你已经检出
到该分支(也就是说，你的 HEAD 指针指向了 iss53 分支)

![](http://ww1.sinaimg.cn/large/006t9e3Igy1fuxx3u2hwmj31lw0l0abu.jpg)

- 有了 Git 的帮助，你不必把这个紧急问题和 iss53 的修改 混在一起，你也不需要花大力气来还原关于 53# 问题的修改，然后再添加关于这个紧急问题的修改，最后将这 个修改提交到线上分支。 你所要做的仅仅是切换回 master 分支。

![](http://ww1.sinaimg.cn/large/006t9e3Igy1fuxx70vjshj31my0redij.jpg)

- 确保你的修改是正确的，然后将其合并回你的 master 分支来部署到线上。 你可以使用
`git merge` 命令来达到上述目的:

![](http://ww1.sinaimg.cn/large/006t9e3Igy1fuxx82r7nij31l60z8q5p.jpg)

- 删除 hotfix 分 支，因为你已经不再需要它了 —— master 分支已经指向了同一个位置。 你可以使用带 `-d` 选项的 `git branch` 命令来删除分支:

`git branch -d hotfix`

![](http://ww1.sinaimg.cn/large/006t9e3Igy1fuxx9n9zfjj31mg0okjtd.jpg)

### 分支的合并

- 你已经修正了 #53 问题，并且打算将你的工作合并入 master 分支。

- Git 会使用两个分支的末端所指的快照(C4 和 C5 )以及这两个分支的工作祖先(C2)，做一个简单的三方合并。

![](http://ww1.sinaimg.cn/large/006t9e3Igy1fuxxf35pyuj31m80oawiy.jpg)

- Git 将此次三方合并的结果做了一个新的快照并且自动创建一个新的提
交指向它。 这个被称作一次合并提交，它的特别之处在于他有不止一个父提交。

![](http://ww1.sinaimg.cn/large/006t9e3Igy1fuxxfuybs3j31kg0lyjt6.jpg)