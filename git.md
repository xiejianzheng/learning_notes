# git常用技巧

##检查远方仓库是否有新分支
	
	git branch -a （会查remote） -r 只会查本地的仓库。
	git remote show origin 显示的比git branch -a 详细。

##给git子命令起缩写别名
	git命令再加上子命令名输入有点长。
	

## git branch 指令

git branch的功能包括“列表”、“创建”、“删除”分支的功能。

git branch 指令的简化形式：

* git branch [-r] 无指令参数， 无附加分支名
	列表

* git branch <分支名> 无指令参数，但加分支名
	创建一个新分支，但是不检出（这种方式有些麻烦，可以用 git checkout -b <新分支名> 替代）

   
指令参数：
* -d, --delete

	git branch -d <分支名>
	
* -m, --move

	git branch -m <旧分支名> <新分支名>

* -c, --copy

	git branch -c <旧分支名> <新分支名>

* -l, --list

	git -l <分支名模式>

选项参数：

* -r , --remotes

	和 list 和 delete 选项连用。
	用于设置list或delete命令时是操控本地分支还是远端分支。
	缺省时，list，delete命令操控的是本地分支。

* -v, -vv, --verbose
	
	使用冗余模式显示输出结果，会显示远端分支与本地分支的联系

## git checkout 指令

git checkout命令的作用是：切换分支或恢复工作树文件

格式：

	git checkout <分支>
	为了准备在<分支>上工作，切换到它，通过更新index还有文件在工作树，并且通过HEAD指针指向<分支>, 本地文件的修改，在工作树中的修改都被保持了，所以它们可以被提交到<分支>

	git checkout -b <新分支> [<开始点>]
	指定-b选项，会导致创建一个新分支, 就像git-branch指令被调用了一样。

## git config 配置指令

git config 

* 配置选项

git config [<配置级别>] <选项> <值>
配置级别一般有:

--local
是缺省的配置级别，配置信息将保留在当前仓库的.git/config 文件中
	
--global
这个是最省事的配置级别，一次配置，处处有效。


<选项>是带名字空间的，常见的配置域有：user，alias。

如: user.email, user.name

在alias配置域下，是各种命令的别名, git 会载入并理解alias配置域下的配置，
并把alias.后面的部分理解为value对应的别名。

如 

alias.co=checkout

alias.st=status

alias.br=branch

alias.ci=commit

* 配置列表

git config -l (--list)

* 乱码处理

如果git log 乱码，
可以使用 git config --global i18n.logOutputEncoding UTF-8来处理，
也可以使用 git config --global i18n.commitEncoding UTF-8 来处理，
因为，当调用git log 时， 如i18n.logOutputEncoding读取不到时，系统会尝试使用i18n.commitEncoding来解析日志。

git status的乱码，
需要用 git config --global core.quotepath false 来处理



