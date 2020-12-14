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










