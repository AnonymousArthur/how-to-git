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


### git init
当我们确认git安装正常之后，第一件事就是初始化一个git仓库(以下以MacOS为例)：
```bash
$> cd Workspace
$> mkdir git-101 && cd git-101
$> git init
已初始化空的 Git 仓库于 /Users/<USER_NAME>/Workspace/git-101/.git/
```

现在再用`ls -la`命令打印 `git-101`目录下的文件列表：
```bash
    ├── .
    ├── ..
    ├── .git
```
可以看到我们的文件夹里多了`.git`文件夹，这个文件夹里记录着与git相关的信息，切勿删除。


## .gitignore
当我们初始化完毕后，我们先不要着急写代码，许多时候我们都是在与框架或生态打交道。就拿前端常用的`npm`为例，`npm install`会按照`package.json`为我们安装很多依赖，而这些依赖又不是我们需要通过git同步到代码仓的数据，那么这时候把`node_modules`（`npm`统一把依赖都安装在这个文件夹）添加入`.gitignore`就可以让git忽略`nodule_modules`文件夹的各种变更（包括`node_modules`文件夹本身）。

值得注意的是，如果一旦文件被git跟踪（track）了，那么在该文件被删的时候依然会被加入到`commit`中。而如果要把这个文件彻底地从代码仓库中抹去，应当做的事是为已经被跟踪的文件设置取消跟踪（untrack）。

TBC...
