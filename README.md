# How to git

## What is git and why do we need it?
git是一个分布式版本控制软件，最初目的是为更好地管理Linux内核开发而设计，但后来git内核已经成熟到可以独立地用作版本控制。[Wikipedia](https://zh.wikipedia.org/wiki/Git)
我们为什么需要版本控制？组织和工程化管理需要版本控制，而最重要的一点是版本控制是我们代码不断演进中的后悔药和任意门，难能可贵。


## How to install git?
git有各种操作系统的发行版本，你甚至可以拉取源码从零进行编译（一般人不会这么玩）。对于MacOS和Linux或其他大多数Unix like系统来说，git已经被默认安装了。而对于windows来说，推荐去[Git](https://git-scm.com)网站上下载Git Bash来安装，Git Bash中包含一个Git发行版本和一个类Bash的终端。使开发者在Windows环境下获得与Unix like系统接近的命令和开发体验。

安装完成后，在终端中运行以下命令，当git安装正常时此命令会返回并显示当前git的版本：
```bash
$> git --version
git version 2.19.0
```


## git init
当我们确认git安装正常之后，第一件事就是初始化一个git代码仓库(以下以MacOS为例)：
```bash
$> cd Workspace
$> mkdir git-101 && cd git-101
$> git init
已初始化空的 Git 仓库于 /Users/<USER_NAME>/Workspace/git-101/.git/
```

现在再用`ls -a`命令打印 `git-101`目录下的文件列表：
```bash
├── .
├── ..
├── .git
```
可以看到我们的文件夹里多了`.git`文件夹，这个文件夹里记录着与git相关的信息，切勿删除。


## .gitignore
当我们初始化完毕后，我们先不要着急写代码，许多时候我们都是在与框架或生态打交道。就拿前端常用的`npm`为例，`npm install`会按照`package.json`为我们安装很多依赖，而这些依赖又不是我们需要通过git同步到代码仓的数据，那么这时候把`node_modules`（`npm`统一把依赖都安装在这个文件夹）添加入`.gitignore`就可以让git忽略`nodule_modules`文件夹的各种变更（包括`node_modules`文件夹本身）。通常，我们还需要把编译后的文件夹`dist`加入到`.gitignore`。

值得注意的是，如果一旦文件被git跟踪（track）了，那么在该文件被删除的时候依然会被加入到`commit`中。而如果要把这个文件彻底地从代码仓库中抹去，应当为已经被跟踪的文件设置取消跟踪（untrack）。


## git add -> git commit
现在我们的仓库被创建好了，你可以通过`git status`命令来查看当前git工作区的状态。如果你做了之前的一步，那么现在`git status`的将会打印类似下面这种信息。
```bash
$> git status
位于分支 master

尚无提交

未跟踪的文件:
  （使用 "git add <文件>..." 以包含要提交的内容）

	.gitignore

提交为空，但是存在尚未跟踪的文件（使用 "git add" 建立跟踪）
```
现在，我们将`.gitignore`加入到我们的暂存区（stage）。
```bash
git add .gitignore
```
然后我们再运行一次`git status`来看看发生了什么。
```bash
$> git status
位于分支 master

尚无提交

要提交的变更：
  （使用 "git rm --cached <文件>..." 以取消暂存）

	新文件：   .gitignore

```
现在`.gitignore`的变更仅仅被暂存到了我们的电脑中，我需要要用`git commit`命令来实际地提交这次改动（提交到HEAD）。
```bash
git commit -m "第一次提交"
[master（根提交） 85323ee] 第一次提交
 1 file changed, 2 insertions(+)
 create mode 100644 .gitignore
```

## git remote add
因为我们的仓库是在本地电脑上创建的，我们的仓库目前应该还没有设置远程服务器。我们通过`git remote add origin <server>`来为本地仓库添加远程服务器。这个操作一般情况下只需要做一次。

## git push
设置好远程服务器之后，我们通过`git push origin master`来把我们本地的变更推送到服务器上。


## git clone
当我们切换到一台新的电脑或者新的工作区的时候我们通常需要用`git clone`命令来下载仓库。

## git branch
git的一大特性是分支功能，分支是用来将特性开发绝缘开来的。我们可以通过`git branch`命令来查看当前仓库的分支。git的默认主分支是`master`。

## git checkout
当我们需要实现一个新特性的时候，我们可以用`git checkout -b feature-name`来创建一个新的分支并切换到`feature-name`这个分支。当特性被实现，并且所有变更都被提交或stash之后，你可以再次用`git checkout <BRANCH_NAME>`切换分支。

更多git的高级使用教程可以查看[【廖雪峰的git教程】](https://www.liaoxuefeng.com/wiki/896043488029600)


# How to GitHub
当你在自己的分支上完成了特性开发，想要把该特性合入到主分支时，通常有两种方式：
1. 直接用`git merge`命令合入目标分支
2. 创建一个**PR(Pull Request)**拉取请求来合入目标分支

社区开发更青睐的是第2种方式：创建拉取请求来合入目标分支。因为这样的合入方式让一切合入主分支的变更清晰明了，我们可以从PR中得到这个变更是一个特性还是一个bugfix，并且PR可以让代码更方便地接受到同行检视(Peer Review)。

这里可以参考[【GitHub的官方指南】](https://guides.github.com/introduction/flow/)或知乎上的中文文章[【团队协作中的 Github flow 工作流程】](https://zhuanlan.zhihu.com/p/39148914)