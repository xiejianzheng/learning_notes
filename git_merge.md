#Git分支——基本分支和合并

#基础的分支和合并
让我们来看一个简单的分支、合并的工作流程，那你可能会在真实世界中使用。

你将按下列步骤操作：
1. 在一个网站项目上工作。
2. 创建一个新的分支，为了一个新的用户故事，你正在工作的。
3. 在这个分支上做点事。

在这阶段，你会收到一个电话，说另一个问题很关键，你需要做个热补丁。
你将做下面的事情：

1. 切换到生产分支。
2. 创建一个一个分支去添加热补丁。
3. 通过测试后，合并热补丁分支到生产分支，并把新程序推送到生产。
4. 切换回原始的用户故事并且继续工作。

## 基础分支

首先，认我们假设你正在你的项目上工作并且已经进行了两次提交在master分支上。

c0是原始状态，c1是提交过一次的状态，c2是提交过两次的状态。

master就指向c2。

你已经决定要着手处理问题#53。

为了创建新分支并且同时切换到该分支，你可以运行git checkout 带上 -b 参数

	$ git checkout -b iss53
	Switched to a new branch "iss53"

	这是下面的快捷键：
	$ git branch iss53
	$ git checkout iss53


这个你在网站的项目上做一些提交。这时会导致iss53分支的指针往前移动。

例如新添加了一个提交c3， iss53就会向前移动指向c3。（即你的HEAD指向它）


现在，你又收到通知，网站存在问问，你需要立即修复它。
使用git，你不需要将修复和iss53的修改一起部署。
你也不需要花很多精力去还原这些修改，在你能够工作于应用你的补丁到生产之前。
所有你需要做的，只是，切换回master分支。

然而，在你做这些前，需要注意，如果你的工作目录或者暂存区有未提交的更改与你要检出的分支冲突，
git不会让你切换分支。这最好清理好工作状态当你切换分支时。

这里有一些方法可以解决此问题（即，隐藏和提交修改）那我们后续会覆盖到在Stashing和Cleaning章节。

当下，让我们假定你已经提交了你所有的改变，因此你能切换回master分支：

	$ git checkout master
	Switch to branch 'master'

在这个时刻，你的项目工作目录是以完全一致的方式在它原本在你开始工作在问题#53之前。并且你可以
集中注意力在你的hotfix上面。

这是要记住的要点：当你切换分支时，git会重置你的工作目录，让它看上去就像最后一次你提交到这个分支一样。
它添加、删除、修改文件自动地，确保你的工作目录看上去和你最后一次提交一样。

下一步， 你有一个热补丁需要制造。让我们创建一个hotfix分支来工作，直到工作完成。

	$ git checkout -b hotfix
	Switched to a new branch 'hotfix'
	$ vim index.html
	$ git commit -a -m 'Fix broken email address'
	[hotfix 1fb7853] Fix broken email addreee
	  1 file changed, 2 insertions(+)

你可以运行测试，确保热补丁是你想要的，并且最终合并热补丁分支到主干，发布到生产。你做这些使用git merge命令：

	$ git checkout master
	$ git merge hotfix
	Updating f42c576..3a08f74c
	Fast-forward
	  index.html | 2 ++
	  1 file changed, 2 insertions(+)

你注意到短语“快进”在合并中。因为hotfix指向的提交C4直接在C2后面。Git只是简单地移动指针向前。
换一种说法，就是，当你尝试合并一个提交和一个能通过第一提交历史到达的提交时，Git简化事情通过移动指针向前。
因为这里没有冲动的工作需要合并在一些————这个就是被叫为“快速向前”。

你的修改现在在提交的快照，指向被主分支，而且你可以部署修复。

在你超级重要的修补部署了，你已经准备好了切换回那个工作你过去正在做的在你被打短之前。
然而，第一步，你将要删除热修补分支。因为你不在需要它。master分支现在指向同一个地方。
你可以删除它用-d选项到git branch：
	
	$ git branch -d hotfix
	Deleted branch hotfix(3a0874c)

现在你可以切换回正在工作进行着的分支：问题 #53 并且继续工作在上面。

	$ git checkout iss53
	Switched to branch "iss53"
	$ vim index.html
	$ git commit -a -m 'Finish the new footer [issue 53]'
	[iss53 ad82d7a] Finish the new footer [issue 53]
	1 file changed, 1 insertion(+)
	
现在iss53的提交在c5。之前一个提交叫c3。c3之前是在主干c2提交上添加的。
主干原来指向c2，现在合并热补丁后，主干指向c4。


它值得注意的这里是指定的工作，你做了的在你的热补丁分支中是没有包含在指定的文件在你的iss53分支中。
如果你需要拉它进来，你可以合并你的master分支到你的iss53分支，通过执行 git merge master，或者你可以
等待去集成那些改变直到你决定去拉iss53分支回到master分支后面。

## 基础的合并

想象一下，你已经决定那你的问题#53工作是完成并且准备好被合并到你的master分支。为了做到那，你将要合并iss53分支到master分支，
很像你合并你的hotfix分支前面。所有你需要做的是检出你希望要合并到的分支，然后运行git merge 命令：

	$ git checkout master
	Switched to branch 'master'
	$ git merge iss53
	Merge made by the 'recursive' strategy.
	index.html | 1 +
	1 file changed, 1 insertion(+)

这看上去和你之前做的合并hotfix分支时看上去有些不同。在这种场景下， 你的开发历史已经背离从老一点的点。

	c0 <- c1 <- c2(公共祖先) <- c4（master 需要被合并到的快照）
			^
			|
			----------- c3 <--- c5 (iss53 需要被合并的快照）

替换仅仅是移动分支指针向前，git创建了一个新的快照，那结果是从3个路径合并且自动创建的一个新提交指向它。
这是被引用为一个合并提交，并且是特别的，在那它有多个父亲。

        
	c4 <- c6 (新master）
	      |
	c5 <--|

现在，那你的工作是被合并进来了，你不在需要iss53分支。你可以关闭问题在你的问题跟踪系统，并且删除对应的分支。

	$ git branch -d iss53

	
## 基础合并冲突

偶然地，这个过程不会顺利。如果你修改了相同文件的相同部分不同地在两个你正在合并的分支中。Git 不会有能力去清晰地合并它们。
如果你的修复为问题53修改了相同的部分文件作为热修复分支，你会取一个合并冲突，那看上去像一些东西向一些东西想这些：

	$ git merge iss53
	Auto-merging index.html
	CONFLICT （content）: Merger conflict in index.html
	Automatic merge failed: fxi conflicts then commit the result.

Git 没有 自动地创建一个新的合并提交。它已经中断了流程，当你解决冲突的时候。
如果你想看哪个文件是没合并的在任何点在合并冲突后。你能运行git status:

	$ git status
	On branch master
	You have unmerged paths.
	  (fix conflicts and run "git commit")
	Unmerged paths:
	  (use "git add <file>..." to mark resolution)

	    both modified:    index.html
	no changes added to commit (use "git add" and/or "git commit -a")


任何事情，那有合并冲突的并且没有被解决的被列为“未合并”。

Git添加标准的冲突决策标注标志到指定的文件那有冲突的， 因此你可以打开它们手动解决这些冲突。

你的文件包含一个部分，那看像是一些东西，像这样：
	
	<<<<<< HEAD:index.html
	<div id="footer"> contract : email.support@github.com</div>
	======
	<div id="footer">
	  please contact us at support@github.com
	</div>
	>>>>>> iss53:index.html

这意味版本在头（你的主分支，因为那过去是什么你检出的当你过去运行合并指令时）是块的顶部部分，同时版本在你的iss53分支看上去像
所有内容在底部部分





