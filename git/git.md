## git

> git 提交树，所有的提交 分支创建都可以看成是一颗数

## git commit

> git 仓库中的提交记录保存的是你目录下所有文件的快照，就像是把整个目录复制，然后再粘贴，但比复制粘贴优雅许多

> git 希望提交记录尽可能地轻量，因此在你每次进行提交时，它并不会盲目的复制整个目录。条件允许的情况下，它会将当前版本与仓库中的上一个版本进行对比，并把所有差异打包到一起作为一个提交记录

> git 还保留了提交历史记录 这也是为什么大多数提交记录上面都有父节点的原因

## git branch

> git 的分支也很轻量。它们只是简单地指向**某个提交记录**，

> 这是因为即使创建再多的分支也不会造成存储或内存上的开销，并且按逻辑分解工作到不同的分支要比维护那些特别臃肿的分支简单多了

> 记住：使用分支其实就相当于说：“我想基于这个提交以及它所有的父提交进行新的工作”

```
git branch newBranch  //创建一个名为newBranch的分支
git checkout newBranch //切换到newBranch分支

git checkout -b newBranch //创建新分支同时切换到新分支
```

## 分支与合并

### git merge

> 我要把这两个父节点本身以及它们所有的祖先都包含进来

```
//基于上面新建的分支 newBranch 我们在main分支上合并新分支
//这样main指向一个新的提交记录-这个提交记录同时指向newBranch 和 main原先指向的记录
git merge newBranch
```

### git rebase

> rebase 实际上就是取出一系列的提交记录， “复制” 它们,然后在另外一个地方逐个的放下去

> rebase 的优势就是可以创造更线性的提交记录，如果只允许使用 rebase 的话，代码库的提交历史将会变得异常清晰

```
/**
* 1.假设有两个分支 newBranch 和 main它们都有各自的提交记录
  2.现在需要将newBranch中的提交记录合并到main分支
  3.此时我们在newBranch分支上
**/
git rebase main //此时newbugFix分支上包含了main分支的所有提交记录
git checkout main //切换到main分支上 注意此时的 main 分支并没有变化
git rebase newBranch //这样main分支就和newBranch指向同一个提交记录 此时俩分支代码同步
```

## 在提交树上移动

### HEAD

> HEAD是一个对当前检出记录的符号引用——也就是指向你正在其基础上进行的提交记录

> HEAD总是指向当前分支上最近一次提交记录，大多数修改提交树的git命令都是从改变HEAD的指向开始

> HEAD通常情况下是指向分支名的（newBranch），在你提交时，改变了 newBranch 的状态

```
/**
* 1.假设有 newBranch 和 main 俩分支
  2.此时我们在main分支上，那么HEAD指向的就是就是main当前最近的一次提交记录
  3.如果我们需要移动HEAD指向，首先我们需要知道你要移动到的提交记录的哈希值
  4.使用 git log 可以查看当前分支的所有提交记录的哈希值
    例如：`fed2da64c0efc5293610bdd892f82a58e8cbc5d8`
  5.这么长也不是一定都需要全都写，git对哈希的处理很智能，你只需要提供能够唯一标识提交记     录的前几个字符就可， 例如`fed2`
**/
```

### 相对引用

> 通过哈希值指定提交记录很不方便，所以 git 引入了相对引用，这个就很厉害了！
>
> 使用相对引用的话，你就可以从一个易于记忆的地方（比如bugFix 分支或 HEAD） 开始计算

#### ^ 向上移动 1 个提交记录

```
/**
* 1.可以将HEAD作为相对引用的参照，然后一直使用HEAD^向上移动
  2.假设在main分支上有四个提交记录，此时我们想要指向第一个提交记录
**/

git checkout HEAD^ //此时HEAD指向第三个提交记录
git checkout HEAD^ //此时HEAD指向第二个提交记录
git checkout HEAD^ //此时HEAD指向第一个提交记录 结束！
```

#### ~<num> 向上移动多个提交记录  如 ~3

> 如果想要在提交树中向上移动很多步 要敲那么多 ^ 貌似也挺烦人的，所以引入了操作符 ~

> 该操作符后面可以跟一个数字(可选，不跟数字时与^相同，向上移动一次)，指定多少次，就向上移动多少次

```js
/**
* 1.还是按照上面的假设 我们需要倒退三个提交记录
**/
git checkout HEAD~3 
```

#### 强制修改分支的位置

> 使用相对引用最多的就是移动分支，可以直接使用 `-f`选项让分支指向另一个提交

> 注意，所有的提交记录都还是存在的！！！！

```js
/**
* 1.假设同上 两分支newBranch main 有不同的提交
  2.现需要将newBranch 指向main最近一次提交记录
**/
git branch -f newBranch main
```

## 撤销变更

> 和提交一样，撤销变更由底层部分(暂存区的独立文件或片段) 和上层部分(变更到底是通过哪种方式被撤销的) 组成

### git reset

> 通过把分支记录回退几个提交记录来实现撤销改动，你可以将这想象成“改写历史”。git reset向上移动分支，原来指向的提交记录就跟从来没有提交过一样，但是代码还是存在的

```js
git reset HEAD^ //回到当前分支的上一步
```

> 这种方式在本地分支中使用很方便，但是这种改写历史的方法对大家一起使用的远程分支是无效的



### git revert

> 撤销更改——即在撤销提交记录的同时，相应的代码也会撤销 ，并分享给别人

```
git revert HEAD^ 
```

> 此时查看日志可看到，在我们要撤销的提交记录后面居然多了一个新提交C2`，这是因为新提交记录引入了更改 ，这些更改刚好是用来撤销要撤销的提交记录C2这个提交的，新的提交记录状态与C1(原本C2的上一个提交记录)是一致的

## 自由修改提交树

### git cherry-pick <提交号>

> 如果你想将一些提交复制到当前所在的位置（HEAD）下面的话，cherry-pick是最直接的方式

> 要在心里牢记 cherry-pick 可以将提交树上任何地方的提交记录取过来追加到 HEAD 上（只要不是 HEAD 上游的提交就没问题）。

```
/**
* 1.假设基于main我们有side bugFix another三个分支
  2.现需要在main分支上将bugFix的C3(提交记录)、side中的C4和another的C7复制到main分   支上
**/
git cherry-pick C3 C4 C7 
```

> 此方法需要你知道你所需要的提交记录(并且还知道这些提交记录的哈希值) 时，用次方法是最简单的

### 交互式的 rebase

> 如果你不清楚你想要的提交记录的哈希值呢？这就 需要 使用到交互的 rebase，如果你想从一系列的提交记录中找到想要的记录，这就是最好的方法

> 交互式 rebase 指的是 使用带参数 --interactive 的 rebase 命令，简写为 `-i`

> 如果 你在命令后增加这个选项，git会打开一个UI界面并列出将要被复制到目标的备选提交记录，它还会显示每个提交记录的哈希值和提交说明，提交说明有助于你理解这个提交进行了哪些更改

> 当 rebase UI界面打开时,你可以做三件事
>
> - 调整提交记录的顺序
> - 删除你不想要的提交
> - 合并提交

```
git rebase --abort //终止
```

## 修改git提交记录 

```
git commit --amend
```

> 假如你需要修改刚才提交记录的 信息
>
> 可以使用此命令

## git tags

> 经过上面的学习，分支的切换，复制，移动，意味着，分支很容易被人为移动，并且当有新的提交时，它也会移动，分支很容易被改变，大部分还只是临时的，并且还一直在变

> 那有没有什么可以永远指向某个提交记录的标识呢，比如软件发布新的大版本，或者是修正一些重要的bug 或是增加了某些新特性，有没有比分支更好的可以永远指向这些提交的方法呢？

> 当然有！ git 的 tag 就是干这个用的，它们可以（在某种程度上——因为标签可以被删除后重新在另外一个位置创建同名标签）永久地将某个特定的提交命名为里程碑，然后就可以像分支一样引用

> 更难得的是 它们并不会随着新的提交而移动，你也不能切换到某个标签上面进行修改提交，它就像是提交树上的一个锚点，标识了某个特定的位置

```
git tag v1 C1 //在C1这个提交记录上加上一个v1tag标签
```

## git describe

> 由于标签在代码库中起着 “锚点” 的作用，git 还为此专门设计了一个命令用来描述离你最近的锚点（也就是标签），它就是 git describe

> git describe 能帮你在提交历史中移动了多次以后找到方向，当你用 git bisect (一个查找产生 Bug 的提交记录的指令) 找到某个提交记录时，或者是当你坐在你那刚刚度假回来的同事的电脑前时，可能需要用到这个命令

```js
git describe 的语法:
git describe <ref>
<ref> 可以是任何能被git 识别成提交记录的引用，如果你没有指定的话，git 会以你目前所检出的位置（HEAD） 它输出的结果是这样：
<tag>_<numCommit>_g<hash>
tag 表示的是离ref最近的标签，numCommits是表示这个ref与tag相差有多少个提交记录，hash表示的是你所给定ref所表示的提交记录哈希值的前几位
当ref提交记录上有某个标签时，则只输出标签名称
```

## 强制推送到远程

```
git push -f origin main
```



## 问题

### 1.git push时报了这个错：fatal: unable to access 'https://github.com/.......': OpenSSL SSL_read: Connection was reset, errno 10054。

解决：

```
git config --global http.sslVerify "false"
```

再次git push 成功

## git 多账号切换、账号重置

```
git config --global user.name "name"
git config --global user.email "email"
```

> 当git中有多个账号，我们需要制定把项目拉取到某个账号下面，一下加上 ff@ 表示用ff这个账号拉取项目

```
git clone http://ff@git.rxgmy.com/wc-platform/zsgt-front-end.git
```

## push或者pull 时git报错不能连接 端口号 443

![image-20220302091945983](D:\FfWork\notes\git\git.assets\image-20220302091945983.png)

>  由于所拉取的gitlab项目没有配置ssh安全证书，自然连接不上

方法：

```
git remote set-url origin http://ff@git.rxgmy.com/jaccount/manager-account.git
```

> 重新设置远程url 为http

##  查看git 配置

```git
vim ~/.gitconfig
```

## 一个项目两个git地址

[参考文章](https://www.cnblogs.com/teamemory/p/11607613.html)

## GitLab合并请求时出现 Validate branchesCannot Create: This merge request already existed

[参考文章](https://blog.csdn.net/qq_36722039/article/details/80137454)

> 发起合并的时候，前面还有一个合并请求打开没有合并操作也没有关闭，需要把前面那个关闭或者合并掉
