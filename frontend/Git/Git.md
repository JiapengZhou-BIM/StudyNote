# Git

## 版本控制

- 版本控制需要使用版本控制软件
- 版本控制软件概念：版本控制软件是一个用来记录文件变化，以便将来查阅特定版本修订情况的系统，因此有时也叫做“**版本控制系统**”
- 通俗的理解：把手工管理文件版本的方式，改为软件管理文件的版本，这个负责管理文件版本的软件，叫做“**版本控制系统**”

- 使用软件的好处：
  - 操作简便：只需识记几组简单的终端命令，即可快速上手常见的版本控制软件
  - 易于对比：基于版本控制软件提供的功能，能够方便地比较文件的变化细节，从而查找出导致问题的原因。
  - 易于回溯：可以将选定的文件回溯到之前的状态，甚至将整个项目都回退到过去某个时间点的状态。
  - 不易丢失：在版本控制软件中，被用户误删除的文件，可以轻松的恢复回来。
  - 协作方便：基于版本控制软件提供的分支功能，可以轻松实现多人协作开发时的代码合并操作。



### 版本控制系统的分类

1. 本地版本控制系统
   - 单机运行，使维护文件版本的操作工具化
2. 集中化的版本控制系统
   - 联网运行，支持多人协作开发，性能差、用户体验不好
3. 分布式版本控制系统
   - 联网运行，支持多人协作开发，性能优秀、用户体验好



### 本地版本控制系统

- 特点：使用软件来记录文件的不同版本，提高了工作效率，降低了手动维护版本的出错率。
- 缺点：
  - 单机运行，不支持多人协作开发。
  - 版本数据库故障后，所有历史更新记录会丢失。



![image-20220326165805486](http://zjp.hxkj.live/MDImage/Git/%e6%9c%ac%e5%9c%b0%e7%89%88%e6%9c%ac%e6%8e%a7%e5%88%b6%e7%b3%bb%e7%bb%9f_2022-03-26_16-58-11.png)

### 集中化版本控制系统

- 典型代表：SVN。

- 特点：基于服务器、客户端的运行模型。
  - 服务器保存文件的所有更新记录。
  - 客户端只保留最新的文件版本。
- 优点：联网运行，支持多人协作开发。
- 缺点：
  - 不支持离线提交版本更新。
  - 中心服务器崩溃后，所有人无法正常工作。
  - 版本数据库故障后，所有历史更新记录会丢失。

![image-20220326165639534](http://zjp.hxkj.live/MDImage/Git/%e9%9b%86%e4%b8%ad%e5%8c%96%e7%89%88%e6%9c%ac%e6%8e%a7%e5%88%b6%e7%b3%bb%e7%bb%9f_2022-03-26_16-56-45.png)

### 分布式版本控制系统

- 典型代表：Git

- 特点：基于服务器、客户端的运行模型。
  - 服务器保存文件的所有更新版本。
  - 客户端是服务器的完整备份，并不是只保留文件的最新版本。
- 优点：
  - 联网运行，支持多人协作开发。
  - 客户端断网后支持离线本地提交版本更新。
  - 服务器故障或损坏后，可使用任何一个客户端的备份进行恢复。

![image-20220326165557159](http://zjp.hxkj.live/MDImage/Git/%e5%88%86%e5%b8%83%e5%bc%8f%e7%89%88%e6%9c%ac%e6%8e%a7%e5%88%b6%e7%b3%bb%e7%bb%9f_2022-03-26_16-56-09.png)



## Git 介绍

- Git 是一个开源的分布式版本控制系统，是目前世界上最先进、最流行的版本控制系统。开源快速高效地处理从很小到非常大的项目版本管理。

- 特点：项目越大越复杂，协同开发者越多，越能体现出 Git 的高性能和高可用性。
- 特性：Git 之所以快速和高效，主要依赖于它的两个特性：
  - 直接记录快照，而非差异比较
  - 近乎所有操作都是本地执行



### SVN 的差异比较

- 传统的版本控制系统（例如 SVN ）是基于差异的版本控制，它们存储的是一组基本文件和每个文件随事件逐步累积的差异。
- 好处：节省磁盘空间
- 缺点：耗时、效率低
- 在每次切换版本的时候，都需要在基本文件的基础上，应用每个差异，从而生成目标版本对应的文件。

![image-20220326170811573](http://zjp.hxkj.live/MDImage/Git/SVN%e7%89%88%e6%9c%ac%e6%8e%a7%e5%88%b6%e6%b5%81%e7%a8%8b_2022-03-26_17-08-28.png)

### Git 的记录快照

- Git 快照是在原有文件版本的基础上重新生成一份新文件，类似于备份。为了效率，如果文件没有修改，Git 不再重新存储该文件，而是只保存一个链接指向之前存储的文件。
- 缺点：占用磁盘空间较大
- 优点：版本切换时非常快，因为每个版本都是完整的文件快照，切换版本时直接恢复目标版本的快照即可。

![image-20220326171155487](http://zjp.hxkj.live/MDImage/Git/Git%e7%89%88%e6%9c%ac%e6%8e%a7%e5%88%b6%e6%b5%81%e7%a8%8b_2022-03-26_17-12-03.png)

### 近乎所有操作都是本地执行

- 在 Git 中绝大多数操作都只需要访问本地文件和资源，一般不需要来自网络上其他计算机的信息。
- 特性：
  - 断网后依旧可以在本地对项目进行版本管理。
  - 联网后，把本地修改的记录同步到云端服务器即可。



### Git 中的三个区域

- 使用 Git 管理的项目，拥有三个区域，分别是：
  1. 工作区 Working Directory
  2. 暂存区 Staging Area
  3. Git仓库 .git directory ( Repository )

![image-20220326172103326](http://zjp.hxkj.live/MDImage/Git/Git%e7%9a%843%e4%b8%aa%e5%8c%ba%e5%9f%9f_2022-03-26_17-21-10.png)



### Git 中的三种状态

1. 已修改 modified ：表示修改了文件，但还没将修改的结果放到暂存区。
2. 已暂存 staged ：表示对已修改文件的当前版本做了标记，使之包含在下次提交的列表中。
3. 已提交 committed ：表示已安全地保存在本地的 Git 仓库中。

- 注意：
  - 工作区的文件被修改了，但还没放到暂存区，就是已修改状态。
  - 如果文件已修改并放入暂存区，就属于已暂存状态。
  - 如果 Git 仓库中保存着特定版本的文件，就属于已提交状态。



### 工作流程

- 基本的 Git 工作流程如下：
  1. 在工作区中修改文件
  2. 将你想要下次提交的更改进行暂存
  3. 提交更新，找到暂存区的文件，将快照永久性存储到 Git 仓库



## Git 基础

### 下载

- [下载网址](https://git-scm.com/)
- 一路Next



### 配置用户信息

- 安装完 Git 之后，要做的第一件事就是设置自己的用户名和邮件地址。因为通过 Git 对项目进行版本管理的时候，Git 需要使用这些基本信息，来记录谁对项目进行了操作
- 注意：如果使用了 --global 选项，表示全局设置，那么该命令只需要运行一次，即可永久生效。



1. 桌面上右键选择 Git Bash Here，输入一下命令，配置用户名和邮件地址

```bash
git config --global user.name "zjp"
git config --global user.email "599211485@qq.com"
```

- 运行后配置的用户名和邮箱地址会写入到 Git 的全局配置文件，配置一次，永久生效。



### 全局配置文件

- 全局配置文件路径：C:\Users\用户名文件夹\ .gitconfig 文件夹中。

![image-20220326182128487](http://zjp.hxkj.live/MDImage/Git/Git%e7%9a%84%e9%85%8d%e7%bd%ae%e6%96%87%e4%bb%b6_2022-03-26_18-21-36.png)



### 检查配置信息

- 除了使用记事本查看全局的配置信息之外，还可以运行如下的终端命令，快速的查看 Git 的全局配置信息。

```bash
# 查看所有的全局配置项
git config --list --global
# 查看指定的全局配置项
git config user.name
git config user.email
```



### 获取帮助信息

```bash
# 无需联网即可在浏览器中打开帮助手册
git help <verb>
# 例如：
git help config

# 如果不想查看完整的手册，那么可以用 -h 选项获取终端中简明的 help 输出
git <verb> -h
# 例如：
git config -h
```



## 获取仓库的方式

- 有两种方式可以在自己电脑上得到一个可用的 Git 仓库
  1. 将尚未进行版本控制的本地目录转换为 Git 仓库。
  2. 从其他服务器克隆一个已存在的 Git 仓库。



### 在现有目录中初始化仓库

- 如果自己有一个尚未进行版本控制的项目目录，想要用 Git 来控制它，需要执行如下两个步骤：
  1. 在项目目录中，通过鼠标右键打开 "Git Bash" 。
  2. 执行 git init 命令将当前的目录转化为 Git 仓库。

```bash
# 初始化 Git 仓库
git init
```

- git init 命令会创建一个名为 .git 的隐藏目录，这个 .git 目录就是当前项目的 Git 仓库，里面包含了初始的必要文件，这个文件是 Git 仓库的必要组成部分。



## 工作区中文件的 4 种状态

- 工作区中的每一个文件可能有 4 种状态，这 4 种状态总共分为两大类
  1. 未被 Git 管理
     1. 未跟踪 (Untracked) ：不被 Git 管理的文件。
  2. 已被 Git 管理
     1. 未修改 (Unmodified) ：工作区中文件的内容和 Git 仓库中文件的内容保持一致。
     2. 已修改 (Modified)：工作区中文件的内容和 Git 仓库中文件的内容不一致。
     3. 已暂存 (Staged)：工作区中被修改的文件已被放在暂存区，准备将修改后的文件保存到 Git 仓库中。

![image-20220327065814699](http://zjp.hxkj.live/MDImage/Git/Git%e5%b7%a5%e4%bd%9c%e5%8c%ba%e4%b8%ad%e6%96%87%e4%bb%b6%e7%9a%844%e7%a7%8d%e7%8a%b6%e6%80%81_2022-03-27_06-58-34.png)

- Git 操作的终极结果：让工作区中的文件都处于 "未修改" 的状态。



### 检查文件的状态

- 可以使用 git status 命令查看文件处于什么状态。

```bash
# 检查文件的状态
git status
```



![image-20220327070428706](http://zjp.hxkj.live/MDImage/Git/%e6%a3%80%e6%9f%a5%e6%96%87%e4%bb%b6%e7%8a%b6%e6%80%81_2022-03-27_07-04-40.png)

- 在状态报告中可以看到新建的 index.html 文件出现在 Untracked files  (未跟踪的文件)  下面。
- 未跟踪的文件意味着 Git 在之前的快照（提交）中没有这些文件，Git 不会自动将之纳入跟踪范围，除非明确地告诉它 "我需要使用 Git 跟踪管理该文件" 。



### 以精简的方式显示文件状态

- 使用 git status 输出的状态报告很详细，但有些繁琐。如果希望以精简的方式显示文件的状态，可以使用如下两条完全等价的命令，其中 -s 是 --short 的简写形式：

```bash
# 精简方式检查文件的状态 
git status -s
git status --short
```

![image-20220327071517009](http://zjp.hxkj.live/MDImage/Git/%e6%a3%80%e6%9f%a5%e6%96%87%e4%bb%b6%e7%8a%b6%e6%80%81_2022-03-27_07-15-20.png)



## 跟踪新文件

- 使用命令 git add 开始跟踪一个文件。

```bash
# 跟踪新文件
git add <文件名>
# 示例
git add index.html
```

- 此时再运行 git status 命令，会看到 index.html 文件在Change to be committed 这行下面，说明已被跟踪，并处于暂存状态。
- 或者已精简的方式显示文件的状态 git status -s ，新添加到暂存区中的文件前面有绿色的 A 标记。

![image-20220327072111962](http://zjp.hxkj.live/MDImage/Git/%e8%b7%9f%e8%b8%aa%e6%96%b0%e6%96%87%e4%bb%b6_2022-03-27_07-21-14.png)



## 提交更新

- 现在暂存区中有一个 index.html 文件等着被提交到 Git 仓库中进行保存。可以执行 git commit 命令进行提交，其中 -m 选项后面是本次的提交信息，用来对提交的内容做进一步的描述。

```bash
# 提交更新
git commit -m "描述的内容"
# 例如
git commit -m "新建了 index.html 文件"
```

- 提交更新之后，再次检查文件的状态，得到提示会如下，所有文件都处于未修改状态，没有任何文件需要提交。

```bash
git status
On branch master
nothing to commit,working tree clean
```



![image-20220327073343083](http://zjp.hxkj.live/MDImage/Git/%e6%8f%90%e4%ba%a4%e6%9b%b4%e6%96%b0_2022-03-27_07-33-49.png)



![image-20220327073707091](http://zjp.hxkj.live/MDImage/Git/%e6%8f%90%e4%ba%a4%e6%9b%b4%e6%96%b0_2022-03-27_07-37-11.png)

## 清空终端内容

- 使用命令 clear 清空终端内容

```bash
# 清空终端内容
clear
```





## 对已提交的文件进行修改

- 当修改了文件的内容之后，再次运行 git status 和 git status -s 命令后

```bash
# 检查文件状态
git status
git status -s
```



![image-20220327080819918](http://zjp.hxkj.live/MDImage/Git/%e6%96%87%e4%bb%b6%e4%bf%ae%e6%94%b9%e5%90%8e%e7%9a%84%e7%8a%b6%e6%80%81_2022-03-27_08-08-32.png)

- 文件 index.html 出现在 Change not staged for commit 这行下面，说明已跟踪文件的内容发生了变化，但还没放在暂存区。
- 注意：修改过的、没有放入暂存区的文件前面有红色的 M 标记。



## 暂存已修改的文件

- 文件已修改后，如果要暂存这次修改，需要再次运行 git add 命令，这个命令是个多功能命令，有 3 个功效：
  1. 可以用它开始跟踪新文件
  2. 把已跟踪的、且已修改的文件放到暂存区
  3. 把有冲突的文件标记为已解决状态

```bash
# 暂存已修改的文件
git add <文件名>
# 实例
git add index.html
```



![image-20220327082022532](http://zjp.hxkj.live/MDImage/Git/%e6%9a%82%e5%ad%98%e5%b7%b2%e4%bf%ae%e6%94%b9%e7%9a%84%e6%96%87%e4%bb%b6_2022-03-27_08-20-29.png)



## 提交已暂存的文件

- 再次运行 git commit -m "提交信息" 命令，即可将暂存区中记录的 index.html 的快照，提交到 Git 仓库中进行保存。
- 检查工作区中文件的状态

```bash
# 提交已暂存的文件
git commit -m "描述的内容"
# 例如
git commit -m "修改了 index.html 文件"
```



![image-20220327082447818](http://zjp.hxkj.live/MDImage/Git/%e6%8f%90%e4%ba%a4%e5%b7%b2%e6%9a%82%e5%ad%98%e7%9a%84%e6%96%87%e4%bb%b6_2022-03-27_08-24-58.png)

![image-20220327082630635](http://zjp.hxkj.live/MDImage/Git/%e6%8f%90%e4%ba%a4%e5%b7%b2%e6%9a%82%e5%ad%98%e7%9a%84%e6%96%87%e4%bb%b6_2022-03-27_08-26-33.png)



## 撤销对文件的修改

- 撤销对文件的修改指的是：把对工作区中对应的文件的修改，还原成 Git 仓库中所保存的版本。
- 操作的结果：所有的修改会丢失，且无法恢复！危险性比较高，需慎重操作！

```bash
# 撤销对文件的修改
git checkout -- <文件名>
# 示例
git checkout -- index.html
```

- 撤销操作的本质：用 Git 仓库中保存的文件，覆盖工作区中指定的文件。

![image-20220327083955981](http://zjp.hxkj.live/MDImage/Git/%e6%92%a4%e9%94%80%e5%af%b9%e6%96%87%e4%bb%b6%e7%9a%84%e4%bf%ae%e6%94%b9_2022-03-27_08-39-59.png)



![image-20220327083318977](http://zjp.hxkj.live/MDImage/Git/%e6%92%a4%e9%94%80%e5%af%b9%e6%96%87%e4%bb%b6%e7%9a%84%e4%bf%ae%e6%94%b9_2022-03-27_08-33-30.png)



## 向暂存区一次性添加多个文件

- 如果需要被暂存的文件个数比较多，可以使用 git add . ，一次性将所有新增和修改过的文件加入暂存区。

```bash
# 向暂存区一次性添加多个文件
git add .
```

- 经常使用的命令，将新增和修改过的文件加入暂存区。

![image-20220327095052836](http://zjp.hxkj.live/MDImage/Git/%e4%b8%80%e6%ac%a1%e6%80%a7%e6%b7%bb%e5%8a%a0%e5%88%b0%e6%9a%82%e5%ad%98%e5%8c%ba_2022-03-27_09-51-10.png)



## 取消暂存的文件

- 如果需要从暂存区移除对应的文件，可以使用如下命令

```bash
# 取消暂存的文件
git reset HEAD <文件名>
# 示例
git reset HEAD index.html
# 取消暂存区所有的文件
git reset HEAD .
```

![image-20220327095552573](http://zjp.hxkj.live/MDImage/Git/%e5%8f%96%e6%b6%88%e6%9a%82%e5%ad%98%e7%9a%84%e6%96%87%e4%bb%b6_2022-03-27_09-55-59.png)



## 跳过使用暂存区域

- Git 标准的工作流程是工作区→暂存区→ Git 仓库，但是有时候这么做略显繁琐，此时可以跳过暂存区，直接将工作区中的修改提交到 Git 仓库（跳过 git add 阶段），这时候 Git 工作的流程简化为了工作区→ Git 仓库。
- Git 提供了一个跳过使用暂存区域的方法，只要在提交的时候，给 git commit 加上 -a 选项，Git 就会自动把所有已经跟踪过的文件暂存起来一并提交，从而跳过 git add 步骤。

```bash
# 跳过使用暂存区域
git commit -a -m "描述信息"
```



## 移除文件

- 从 Git 仓库中移除文件有两种：
  1. 从 Git 仓库和工作区中同时移除对应的文件。
  2. 只从 Git 仓库中移除指定的文件，但保留工作区中对应的文件。文件变成未被跟踪的状态。

```bash
# 从 Git 仓库和工作区中同时移除对应的文件。
git rm -f index.html
# 只从 Git 仓库中移除指定的文件，但保留工作区中对应的文件。
git rm --cached index.html
```



## 忽略文件

- 一般我们总会有些文件无序纳入 Git 的管理，也不希望它们总会出现在未跟踪文件列表。在这种情况下，我们可以创建一个名为 .gitignore 的配置文件，列出要忽略的文件的匹配模式。
- 文件 .gitignore 的格式规范如下
  - 以 # 开头的是注释
  - 以 /  结尾的是目录
  - 以 / 开头防止递归
  - 以 ! 开头表示取反
  - 可以使用 glob 模式进行文件和文件夹的匹配（ glob 值简化了的正则表达式）

### glob 模式

- 所谓的 glob 模式是指简化了的正则表达式：
  - 星号 * 匹配零个或多个任意字符
  - [abc] 匹配任何一个列在方括号中的字符。（此案例匹配一个 a 或匹配一个 b 或匹配一个 c ）
  - 问号 ? 只匹配一个任意字符
  - 在方括号中使用短划线分隔两个字符，表示所有在这两个字符范围内的都可以匹配（比如 [0-9] 表示匹配所有 0 到 9 的数字）
  - 两个星号 ** 表示匹配任何中间目录（比如 a/**/z 可以匹配 a/z、a/b/z 或 a/b/c/z 等）



### .gitignore 文件的例子

```.gitignore
# 忽略所有的 .a 文件
*.a

# 跟踪所有的 lib.a ，即使在前面忽略了 .a 文件
!lib,a

# 忽略当前目录下的 TODO 文件，而不忽略 subdir/TOOD
/TOOD

# 忽略任何目录下名为 build 的文件夹
build/

# 忽略 doc/notes.txt，但不忽略 doc/server/arch.txt
doc/*txt

# 忽略 doc/目录及其所有子目录下的 .pdf 文件
doc/**/*.pdf
```



## 查看提交历史

- 如果希望回顾项目的提交历史，可以使用 git log 这个命令。

```bash
# 按时间先后顺序列出所有的提交历史，最近的提交排在最上面
git log

# 只展现最新的两条提交历史，数字可以按需进行填写
git log -2

# 在一行上展示最近两条提交历史的信息
git log -2 --pretty=oneline

# 在一行上展示最近两条提交历史的信息，并自定义输出的格式
# %h 提交的简写哈希值  %an 作者名字  %ar作者修订日期，按多久之前的方式显示  %s提交说明
git log -2 --pretty=format:"%h | %an | %ar | %s"
```

![image-20220327104050759](http://zjp.hxkj.live/MDImage/Git/%e6%9f%a5%e7%9c%8b%e6%8f%90%e4%ba%a4%e5%8e%86%e5%8f%b2_2022-03-27_10-40-52.png)

## 回退到指定的版本

```bash
# 在一行上展示所有的提交历史
git log --pretty=oneline

# 使用 git reset --hard 命令，根据指定的提交 ID 回退到指定版本
git reset --hard <CommitID>
```

![image-20220327104642436](http://zjp.hxkj.live/MDImage/Git/%e5%9b%9e%e9%80%80%e5%88%b0%e6%8c%87%e5%ae%9a%e7%9a%84%e7%89%88%e6%9c%ac_2022-03-27_10-46-53.png)



```bash
# 在旧版本中使用 git reflog --pretty=oneline 命令，查看提交的历史
# 如果在旧版本中使用 git log --pretty=oneline ，则无法查看最新的提交历史
git reflog --pretty=oneline
# 再次根据最新的提交 ID ，跳转到最新的版本
git reset --hard <CommitID>
```

![image-20220327105210517](http://zjp.hxkj.live/MDImage/Git/%e5%9b%9e%e9%80%80%e5%88%b0%e6%8c%87%e5%ae%9a%e7%9a%84%e7%89%88%e6%9c%ac_2022-03-27_10-52-12.png)



## 总结

- 初始化 Git 仓库的命令

```bash
git inti
```

- 查看文件状态的命令

```bash
git status 
git status -s
```

- 一次性将文件加入缓存区的命令

```bash
git add .
```

- 将缓存区的文件提交到 Git 仓库的命令

```bash
git commit -m "提交信息"
```



# GitHub

## 开源和闭源

![image-20220328072644286](http://zjp.hxkj.live/MDImage/Git/%e5%bc%80%e6%ba%90%e5%92%8c%e9%97%ad%e6%ba%90_2022-03-28_07-26-51.png)

## 开源许可协议

- 开源并不意味完全没有限制，为了限制使用者的使用范围和保护作者的权利，每个开源项目都应该遵守开源许可协议( Open Source License )。

 

- 常见的 5 种开源许可协议
  1. BSD ( Berkeley Software Distribution )
  2. Apache License 2.0
  3. **GPL** ( GNU General Public License )
     - 具有传染性的一种开源协议，不允许修改后和衍生的代码作为闭源的商业软件发布和销售
     - 使用 GPL 的最著名的软件项目是：Linux
  4. LGPL ( GNU Lesser General Public License )
  5. **MIT** (Massachusetts Institute of Technology )
     - 是目前限制最少的协议，唯一的条件：在修改后的代码或者发行包中，必须包含原作者的许可信息。
     - 使用 MIT 的软件项目有：jQuery、Node.js



## 开源好处

- 开源的核心思想是“我为人人，人人为我”。
  1. 开源给使用者更多的控制权
  2. 开源让学习变得容易
  3. 开源才有真正的安全



- 开源是软件开发领域的大趋势，拥抱开源就像站在了巨人的肩膀上，不用自己重复造轮子，让开发越来越容易。



## 开源项目托管平台

- 专门用于免费存放开源项目源代码的网站，叫做开源项目托管平台。目前世界上比较出名的开源项目托管平台主要有：
  1. GitHub (全球最牛的开源托管平台)
  2. GitLab (对代码私有性支持较好，因此企业用户较多)
  3. Gitee (码云，是国产的开源项目托管平台，访问速度快，纯中文界面，使用友好)
- 注意：以上 3 个开源项目托管平台，只能托管以 Git 管理的项目源代码。



## GitHub

- GitHub 是全球最大的开源项目托管平台。因此只支持 Git 作为唯一的版本控制工具，故名 GitHub。
- 在 GitHub 中，可以做到：
  1. 关注自己喜欢的开源项目( Watch )，并为其点赞( Star )。
  2. 为自己喜欢的开源项目做贡献( Pull Request )。
  3. 和开源项目的作者讨论 Bug 和提需求( Issues )。
  4. 把喜欢的项目复制一份作为自己的项目进行修改( Fork )。
  5. 创建属于自己的开源项目
  6. 等等



## 注册 GitHub 账户

- 流程
  1. 访问 [GitHub](https://github.com/) 的官网首页。
  2. 点击"Sign up"按钮跳转到注册页面。
  3. 填写可用的用户名、邮箱、密码。
  4. 通过点击箭头的形式，将验证图片摆正。
  5. 点击" Create account "按钮注册新用户。
  6. 登录到第三步填写的邮箱中，点击激活链接，完成注册。



## 新建空白远程仓库

![image-20220328090228827](http://zjp.hxkj.live/MDImage/Git/新建远程仓库_2022-03-28_09-02-37.png)



## 远程仓库的访问方式

- GitHub 上的远程仓库，有两种访问方式，分别是 HTTPS 和 SSH 。它们的区别是：
  1. HTTPS：零配置。但是每次访问仓库时，需要重复输入 GitHub 的账户和密码才能访问成功。
  2. SSH：需要进行额外的配置。但是配置成功后，每次访问仓库时，不需重复输入 GitHub 的账户和密码。
- 注意：实际开发中，推荐使用 SSH 的方式访问远程仓库。



### 基于 HTTPS 将本地仓库上传到 GitHub

- 第一次运行执行以下操作，实现本地仓库关联同步到远程仓库
- 需要输入账户和密码

![image-20220328091516368](http://zjp.hxkj.live/MDImage/Git/HTTPS%e8%ae%bf%e9%97%ae%e6%a8%a1%e5%bc%8f_2022-03-28_09-15-27.png)





### SSH Key

- SSH Key 的作用：实现本地仓库和 GitHub之间免登陆的加密数据传输。
- SSH Key 的好处：免登陆身份认证、数据加密传输。
- SSH Key 由两部分组成：
  1. id_rsa (私钥文件，存放于客户端的电脑中即可)
  2. id_rsa.pub (公钥文件，需要配置到 GitHub 中)



#### 生成 SSH Key

1. 打开 Git Bash
2. 粘贴如下的命令，并将 your_email@example.com 替换为注册 GitHub 账户时填写的邮箱

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
# ssh-keygen -t rsa -b 4096 -C "599211485@qq.com"
```

3. 连续敲击 3 次回车，即可在 C:\Users\用户名文件夹\.ssh 目录中生成 id_rsa 和 id_rsa.pub 两个文件



#### 配置 SSH Key

1. 使用记事本打开 id_rsa.pub 文件，复制里面的文本内容
2. 在浏览器中登录 GitHub，点击头像 → Settings → SSH and GPG Keys → New SSH key
3. 将 id_rsa.pub 文件中的内容，粘贴到 Key 对应的文本框中
4. 在 Title 文本框中任意填写一个名称，来标识这个 Key 从何而来



#### 检测 SSH Key 是否配置成功

1. 打开 Git Bash ，输入如下命令。

```bash
ssh -T git@github.com
```

![image-20220329084948042](http://zjp.hxkj.live/MDImage/Git/%e6%a3%80%e9%aa%8cSSHKey%e9%85%8d%e7%bd%ae_2022-03-29_08-49-51.png)

2. 输入 yes 继续连接。

```bash
yes
```

![image-20220329085352168](http://zjp.hxkj.live/MDImage/Git/%e6%a3%80%e9%aa%8cSSHKey%e9%85%8d%e7%bd%ae_2022-03-29_08-53-56.png)

3. 出现 successfully 则证明，配置成功。



### 基于 SSH 将本地仓库上传到 GitHub

- 第一次运行执行以下操作，实现本地仓库关联同步到远程仓库
- 一旦配置了 SSH Key ，就无需输入账户密码

![image-20220329090911240](http://zjp.hxkj.live/MDImage/Git/%e5%9f%ba%e4%ba%8eSSH%e4%b8%8a%e4%bc%a0_2022-03-29_09-09-44.png)



### 本地仓库同步到远程仓库

- 当远程仓库关联完，本地进行了修改或者新建操作然后提交本地仓库后，若要进行远程仓库同步，需执行

```bash
# 本地仓库同步到远程仓库
git push
```



## 将远程仓库克隆到本地

1. 打开 Git Bash ，输入如下的命令并回车执行

```bash
git clone 远程仓库的地址
```



### 使用 HTTPS 克隆

```bash
# 使用 HTTPS 克隆
git clone https://github.com/JiapengZhou-HX/test.git
```



![image-20220329092453462](http://zjp.hxkj.live/MDImage/Git/%e4%bd%bf%e7%94%a8HTTPS%e5%85%8b%e9%9a%86_2022-03-29_09-25-04.png)

![image-20220329092528416](http://zjp.hxkj.live/MDImage/Git/%e4%bd%bf%e7%94%a8HTTPS%e5%85%8b%e9%9a%86_2022-03-29_09-25-30.png)

### 使用 SSH 克隆

```bash
# 使用 SSH 克隆
git clone git@github.com:JiapengZhou-HX/test.git
```



![image-20220329092818393](http://zjp.hxkj.live/MDImage/Git/%e4%bd%bf%e7%94%a8SSH%e5%85%8b%e9%9a%86_2022-03-29_09-28-20.png)



![image-20220329092743583](http://zjp.hxkj.live/MDImage/Git/%e4%bd%bf%e7%94%a8SSH%e5%85%8b%e9%9a%86_2022-03-29_09-27-50.png)

## 分支

- 概念：分支类似于平行宇宙，程序的平行宇宙



### 分支在实际开发中的作用

- 在进行多人协作开发的时候，为了防止互相干扰，提高协同开发的体验，建议每个开发者都基于分支进行项目功能的开发。

![image-20220329103150063](http://zjp.hxkj.live/MDImage/Git/%e5%88%86%e6%94%af%e5%bc%80%e5%8f%91_2022-03-30_09-16-26.png)

### master主分支

- 在初始化本地 Git 仓库的时候，Git 默认已经帮我们创建了一个名字叫做 master 的分支，通常我们把这个 master 分支叫做主分支。
- 在实际工作中，master 主分支的作用是：用来保存和记录整个项目已完成的功能代码。
- 因此，不允许程序员直接在 master 分支上修改代码，因为这样做的风险太高，容易导致整个项目崩溃。

![image-20220329103223757](http://zjp.hxkj.live/MDImage/Git/%e4%b8%bb%e5%88%86%e6%94%af_2022-03-30_09-17-15.png)

### 功能分支

- 由于程序员不能直接在 master 分支上进行功能的开发，所以就有了功能分支的概念。
- 功能分支指的是专门用来开发新功能的分支，它是临时从 master 主分支上分叉出来的，当新功能开发且测试完毕后，最终需要合并到 master 主分支上。

![image-20220329103516581](http://zjp.hxkj.live/MDImage/Git/%e5%8a%9f%e8%83%bd%e5%88%86%e6%94%af_2022-03-30_09-17-38.png)



### 查看分支列表

- 使用如下命令，可以查看当前 Git 仓库中所有的分支列表

```bash
# 查看分支列表
git branch
```

- 分支前面的 * 表示当前分支

![image-20220329110303222](http://zjp.hxkj.live/MDImage/Git/%e6%9f%a5%e7%9c%8b%e5%88%86%e6%94%af_2022-03-30_09-18-29.png)

- 注意：当上传到 GitHub 上时，主分支会被重命名为 main

![image-20220329110401698](http://zjp.hxkj.live/MDImage/Git/%e6%9f%a5%e7%9c%8b%e5%88%86%e6%94%af_2022-03-30_09-18-37.png)



### 创建新分支

- 使用如下命令，可以基于当前分支，创建一个新分支，此时，新分支中的代码和当前分支完全一样。

```bash
# 创建新分支
git branch 分支名称
# 示例
git branch login
```

- 注意：创建完分支之后，当前用户的所处的分支还是 master 主分支，并不是创建的分支。

![image-20220329111542439](http://zjp.hxkj.live/MDImage/Git/%e5%88%87%e6%8d%a2%e5%88%86%e6%94%af_2022-03-30_09-19-35.png)

![image-20220329111623047](http://zjp.hxkj.live/MDImage/Git/%e5%88%87%e6%8d%a2%e5%88%86%e6%94%af_2022-03-30_09-19-56.png)

### 切换分支

- 使用如下命令，可以切换到指定的分支上进行开发。
- 切换了分支，会使本地工作区的文件从 master 拷贝一份出来，当切换回 master，文件又会变成 master 的工作区文件。

```bash
# 切换分支
git checkout 需要切换的分支名
# 示例
git checkout login
```

![image-20220329111849126](http://zjp.hxkj.live/MDImage/Git/%e5%88%87%e6%8d%a2%e5%88%86%e6%94%af_2022-03-30_09-20-33.png)

### 分支的快速创建和切换

- 使用如下的命令，可以创建指定名称的新分支，并立即切换到新分支上。

```bash
# -b 指的是 branch 的简写，表示创建一个新分支
# checkout 表示切换到刚才新建的分支上
git checkout -b 分支名称
```



![image-20220329113002254](http://zjp.hxkj.live/MDImage/Git/%e5%88%86%e6%94%af%e5%bf%ab%e9%80%9f%e5%88%9b%e5%bb%ba%e5%88%87%e6%8d%a2_2022-03-30_09-22-08.png)

![image-20220329112729248](http://zjp.hxkj.live/MDImage/Git/%e5%88%86%e6%94%af%e5%bf%ab%e9%80%9f%e5%88%9b%e5%bb%ba%e5%88%87%e6%8d%a2_2022-03-30_09-21-52.png)



### 分支合并

- 功能分支的代码开发测试完毕之后，可以使用如下的命令，将完成后的代码合并到 master 主分支上。
- 注意：假设要把 C 分支的代码合并到 A 分支，则必须要切换到 A 分支上，再运行 git merge 命令，来合并 C 分支。

```bash
# 切换到 master 分支
git checkout master
# 在 master 分支上运行 git merge 命令，将 login 分支的代码合并到 master 分支
git merge login
```



![image-20220330092915728](http://zjp.hxkj.live/MDImage/Git/%e5%88%86%e6%94%af%e5%90%88%e5%b9%b6_2022-03-30_09-29-23.png)







### 删除分支

- 当把功能分支的代码合并到 master 主分支上以后，就可以使用如下命令，删除对应的功能分支：
- 注意：删除的分支不能是当前处于的分支

```bash
# 删除分支
git branch -d 分支名称
# 示例
git branch -d login
```



![image-20220330094458069](http://zjp.hxkj.live/MDImage/Git/%e5%88%a0%e9%99%a4%e5%88%86%e6%94%af_2022-03-30_09-45-02.png)

![image-20220330094218660](http://zjp.hxkj.live/MDImage/Git/%e5%88%a0%e9%99%a4%e5%88%86%e6%94%af_2022-03-30_09-42-26.png)



- 当分支进行了修改，但未合并，删除会出现错误，提示分支未合并到主分支。
- 需要进行强制删除

```bash
# 强制删除分支
git branch -D 分支名称

# 示例
git branch -D login
```



### 遇到冲突的时候分支合并

- 如果在两个不同的分支中，对同一个文件进行了不同的修改，Git 就没法干净的合并它们，因此，我们需要打开这些包含冲突的文件然后手动解决冲突。

```bash
# 假设，把 reg 分支合并到 master 分支期间，代码发生了冲突
git checkout master
git merge reg

# 打开包含冲突的文件，手动解决冲突之后，再执行如下命令
git add .
git commit -m "解决了分支合并冲突的问题"
```



![image-20220330100951146](http://zjp.hxkj.live/MDImage/Git/%e5%88%86%e6%94%af%e5%90%88%e5%b9%b6%e5%86%b2%e7%aa%81_2022-03-30_10-09-57.png)



### 将本地分支推送到远程仓库

- 如果是第一次将本地分支推送到远程仓库，需要运行如下命令
- 如果远程仓库已经有对应分支，只需要 git push 就可以把分支代码推送到远程仓库上。

```bash
# -u 表示把本地分支和远程分支进行关联，只在第一次推送的时候需要带 -u 参数
git push -u 远程仓库的别名 本地分支的名称:远程分支名称

# 示例
git push -u origin payment:pay

# 如果希望远程分支的名称和本地分支名称保持一致，可以对命令进行简化
git push -u origin payment
```

![image-20220330102556478](http://zjp.hxkj.live/MDImage/Git/%e6%8e%a8%e9%80%81%e5%88%b0%e8%bf%9c%e7%a8%8b%e4%bb%93%e5%ba%93_2022-03-30_10-26-09.png)

![image-20220330102749522](http://zjp.hxkj.live/MDImage/Git/%e6%8e%a8%e9%80%81%e5%88%b0%e8%bf%9c%e7%a8%8b%e4%bb%93%e5%ba%93_2022-03-30_10-27-51.png)



### 查看远程仓库中所有的分支列表

- 通过如下的命令，可以查看远仓库中，所有的分支列表信息。

```bash
# 查看远程仓库中所有的分支列表
git remote show 远程仓库名称

# 示例
git remote show origin
```


![image-20220330103045757](http://zjp.hxkj.live/MDImage/Git/%e8%bf%9c%e7%a8%8b%e4%bb%93%e5%ba%93%e7%9a%84%e5%90%8d%e5%ad%97_2022-03-30_10-30-47.png)



### 跟踪分支

- 跟踪分支指的是：从远程仓库中，把远程分支下载到本地仓库中。

```bash
# 从远程仓库中，把对应的远程分支下载到本地仓库，保持本地分支和远程分支名称相同
git checkout 远程分支的名称

# 示例
git checkout pay

# 从远程仓库中，把对应的远程分支下载到本地仓库，并把下载的本地分支进行重命名
git checkout -b 本地分支名称 远程仓库名称/远程分支名称

# 示例
git checkout -b payment origin/pay
```

![image-20220330103747908](http://zjp.hxkj.live/MDImage/Git/%e8%b7%9f%e8%b8%aa%e5%88%86%e6%94%af_2022-03-30_10-37-52.png)



### 拉取远程分支的最新的代码

- 可以使用如下命令，把远程分支最新的代码下载到本地对应的分支中

```bash
# 从远程仓库，拉取当前分支最新的代码，保持当前分支代码和远程分支代码一致
git pull
```

![image-20220330104628779](http://zjp.hxkj.live/MDImage/Git/%e6%8b%89%e5%8f%96%e8%bf%9c%e7%a8%8b%e5%88%86%e6%94%af%e4%bb%a3%e7%a0%81_2022-03-30_10-46-39.png)

### 删除远程仓库的分支

- 可以使用如下的命令，删除远程仓库中指定的分支

```bash
# 删除远程仓库中，指定名称的远程分支
git push 远程仓库名称 --delete 远程分支名称

# 示例
git push origin --delete pay
```



![image-20220330105029197](http://zjp.hxkj.live/MDImage/Git/%e5%88%a0%e9%99%a4%e8%bf%9c%e7%a8%8b%e4%bb%93%e5%ba%93%e7%9a%84%e5%88%86%e6%94%af_2022-03-30_10-50-36.png)





