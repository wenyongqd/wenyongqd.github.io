---
title: LearningGitBranching
date: 2020-03-31 22:40:36
tags:
---

<!-- TOC -->

- [Git Commit](#git-commit)
- [Git Branch](#git-branch)

<!-- /TOC -->

### Git Commit

- **Git** 仓库中的提交记录保存的是你的目录下所有文件的快照，就像是把整个目录复制，然后再粘贴一样，但比复制粘贴优雅许多！
- **Git** 希望提交记录尽可能地轻量，因此在你每次进行提交时，它并不会盲目地复制整个目录。条件允许的情况下，它会将当前版本与仓库中的上一个版本进行对比，并把所有的差异打包到一起作为一个提交记录。
- **Git** 还保存了提交的历史记录。这也是为什么大多数提交记录的上面都有父节点的原因 —— 我们会在图示中用箭头来表示这种关系。对于项目组的成员来说，维护提交历史对大家都有好处。

当前有两个提交记录 —— 初始提交 `C0` 和其后可能包含某些有用修改的提交 `C1`。
<img class="shadow" width="320" src="c1.png" />
`git commit`, 在下面创建一个新的提交记录。
<img class="shadow" width="320" src="c0.png" />

### Git Branch

Git 的分支也非常轻量。它们只是简单地指向某个提交纪录 —— 仅此而已。所以许多 Git 爱好者传颂：

**早建分支！多用分支！**

这是因为即使创建再多分的支也不会造成储存或内存上的开销，并且按逻辑分解工作到不同的分支要比维护那些特别臃肿的分支简单多了。

**1.** 接下来，利用 `git branch newImage`, 我们将要创建一个到名为 newImage 的分支。
<img class="shadow" width="320" src="c2.png" />
看到了吗，创建分支就是这么容易！新创建的分支 newImage 指向的是提交记录 C1。

**2.** 现在咱们试着往新分支里提交一些东西, git commit。
<img class="shadow" width="320" src="c3.png" />
哎呀！为什么 master 分支前进了，但 newImage 分支还待在原地呢？！这是因为我们没有“在”这个新分支上，看到 master 分支上的那个星号（\*）了吗？这表示当前所在的分支是 master。

**3.** 现在咱们告诉 Git 我们想要切换到新的分支上

下面的命令会让我们在提交修改之前先切换到新的分支上, `git checkout newImage`; `git commit`.
<img class="shadow" width="320" src="c4.png" />
我们的修改已经保存到新的分支里了。
**tips**: 有个更简洁的方式：如果你想创建一个新的分支同时切换到新创建的分支的话，可以通过 `git checkout -b <your-branch-name>` 来实现。
