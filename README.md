# Git-Branching


##### 符号解释

符号 * 表示当前分支


## [交互练习git](https://learngitbranching.js.org/?locale=zh_CN)

// 选择关卡 $ level rampup2 

//合并分支 

git merge main

// 合并分支rebase，取出一系列的提交记录，“复制”它们，另外一个地方逐个的放下去。优势就是可以创造更线性的提交历史。

新建并切换到 bugFix 分支

提交一次

切换回 main 分支再提交一次

再次切换到 bugFix 分支，rebase 到 main 上

<img width="929" alt="image" src="https://user-images.githubusercontent.com/33156021/207017295-ff73a33e-7167-421d-9454-63e7c8a34240.png">

$ git checkout -b bugFix; git commit;

$ git checkout main; git commit; 

$ git checkout bugFix; git rebase main



### 树上前后移动

符号"HEAD", 指向你正在其基础上进行工作的提交记录。```cat .git/HEAD``` 查看， 如果 HEAD 指向的是一个引用，还可以用 ```git symbolic-ref HEAD``` 查看它的指向。 ```git log``` 来查查看提交记录的哈希值


// 分离HEAD

从 bugFix 分支中分离出 HEAD 并让其指向一个提交记录。

通过哈希值指定提交记录。每个提交记录的哈希值显示在代表提交记录的圆圈中。

<img width="929" alt="image" src="https://user-images.githubusercontent.com/33156021/207018527-43826273-0016-4793-bec9-2fb0a8c5cc8b.png">

```
$ git checkout c4
```

// “相对引用（^）”，使用 ^ 向上移动 1 个提交记录

切换到 bugFix 的父节点。这会进入分离 HEAD 状态。

<img width="929" alt="image" src="https://user-images.githubusercontent.com/33156021/207019790-0338d6ef-a3d6-44ff-84fa-5c62b3cbf637.png">

```$ git checkout bugFix^```

// “相对引用2（~）”，使用 ~<num> 向上移动多个提交记录，如 ~3。使用 -f 选项让分支指向另一个提交。git branch -f main HEAD~3。-f 则容许我们将分支强制移动到那个位置。

移动 HEAD，main 和 bugFix 到目标所示的位置。

<img width="929" alt="image" src="https://user-images.githubusercontent.com/33156021/207021132-2c3711d5-24b3-44d3-b90f-bf0c754bfb01.png">

```
$ git checkout bugFix; git branch -f bugFix HEAD~3;
  
$ git checkout c6; git branch -f main HEAD;
  
$ git checkout c1;
```

// “撤销变更”，git reset 向上移动分支，原来指向的提交记录就跟从来没有提交过一样，$ git reset HEAD~1, $ git revert HEAD. 

<img width="956" alt="image" src="https://user-images.githubusercontent.com/33156021/207025264-745a61d4-0b97-4f4c-8225-c5da2c10a9ec.png">

```$ git branch -f local HEAD~1; git checkout pushed; git resert HEAD;```

### 整理提交记录

// “Git Cherry-pick”，将一些提交复制到当前所在的位置（HEAD）下面，

<img width="1012" alt="image" src="https://user-images.githubusercontent.com/33156021/207032408-51d4be60-4df5-4bec-8f93-7c71367558f9.png">

```$ git cherry-pick c3 c4 c7```

// "交互式的 rebase"。git rebase 把所在分支复制到目标参数上的分支上并且带有'。带参数 --interactive 简写为 -i，rebase UI界面打开时, 你能做3件事：1 提交记录的顺序（通过鼠标拖放来完成）；2 不想要的提交（通过切换 pick 的状态来完成，关闭就意味着你不想要这个提交记录）；3 提交。 遗憾的是由于某种逻辑的原因，我们的课程不支持此功能，因此我不会详细介绍这个操作。简而言之，它允许你把多个提交记录合并成一个。rebase 的优缺点： 优点: Rebase 使你的提交树变得很干净, 所有的提交都在一条线上 缺点: Rebase 修改了提交树的历史

要通过本关, 做一次交互式的 rebase，整理成目标窗口中的提交顺序。 记住，你随时都可以用 undo、reset 修正错误，

$ git rebase -i HEAD~4

// “只取一个提交记录”，本地栈式提交，把 bugFix 分支里的工作合并回 main 分支了。你可以选择通过 fast-forward 快速合并到 main 分支上，但这样的话 main 分支就会包含我这些调试语句了。可以使用 git rebase -i git cherry-pick 来达到目的。

<img width="956" alt="image" src="https://user-images.githubusercontent.com/33156021/207037769-c35ca3cc-f0a1-4c91-8f39-1f3b51de0504.png">

```$ git rebase -i HEAD~3; git branch -f main HEAD; ```

//“提交的技巧 #1”，先用 git rebase -i 将提交重新排序，然后把我们想要修改的提交记录挪到最前 然后用 git commit --amend 来进行一些小修改 接着再用 git rebase -i 来将他们调回原来的顺序 最后我们把 main 移到修改的最前端

<img width="956" alt="image" src="https://user-images.githubusercontent.com/33156021/207039240-645f1369-db6b-439c-8239-6be354c9dc92.png">

```
$ git rebase -i HEAD~2; $ git rebase -i HEAD~1; $ git rebase -i HEAD~2; git branch -f main HEAD;
```

// “提交的技巧 #2”，cherry-pick 可以将提交树上任何地方的提交记录取过来追加到 HEAD 上（只要不是 HEAD 上游的提交就没问题）。

通过 --amend 改变提交记录 C2

<img width="953" alt="image" src="https://user-images.githubusercontent.com/33156021/207040898-0ee9e6f0-7afc-4979-abab-0f91e32603da.png">

```
  $ git checkout c2; git commit --amend; git rebase -i HEAD~2;
  $ git branch -f main HEAD;
```

//  “Git Tag”，比分支更好的可以永远指向这些提交的方法，```git tag v1 c1```

在这个关卡中，按照目标建立两个标签，然后切换到 v1 上面，要注意你会进到分离 HEAD 的状态 —— 这是因为不能直接在v1 上面做 commit。

<img width="982" alt="image" src="https://user-images.githubusercontent.com/33156021/207042742-0a6f43e6-5805-4586-aecb-0d8a58abf726.png">

``` $ git tag v0 c1; git checkout c2; git tag v1; ```

// “Git Describe”，描述离你最近的锚点（也就是标签），用 git bisect（一个查找产生 Bug 的提交记录的指令）找到某个提交记录时，或者是当你坐在你那刚刚度假回来的同事的电脑前时， 可能会用到这个命令。输出的结果：```<tag>_<numCommits>_g<hash>```，```tag``` 表示的是离 ref 最近的标签， ```numCommits``` 是表示这个 ref 与 tag 相差有多少个提交记录，``` hash``` 表示的是你所给定的 ref 所表示的提交记录哈希值的前几位。```git tag v2 c3```
<img width="1045" alt="image" src="https://user-images.githubusercontent.com/33156021/207043681-c5644954-8200-43e2-96b9-290fdf5ad107.png">

![image](https://user-images.githubusercontent.com/33156021/207044247-c387f710-8979-4937-8dcd-db71efeeafa8.png)

git describe 就是这样了！试着在这个关卡指定几个位置来感受一下这个命令吧！

// “多次 Rebase”

![image](https://user-images.githubusercontent.com/33156021/207044519-1f8188bd-79cc-4bb1-841d-cdd8c3ed8e56.png)

```
$ git rebase main bugFix

$ git rebase bugFix side

$ git rebase side another

$ git rebase another main
```






// 选择父提交记录，链式操作

要完成此关，在指定的目标位置创建一个新的分支。

``` $ git branch bugWork main^^2^```


// “纠缠不清的分支”


  
  
### 远程1 Push & Pull —— Git 远程仓库！
远程仓库是一个强大的备份； 远程让代码社交化了。

// “Git Clone”，git clone 后本地仓库多了一个名为 o/main 的分支或者叫远程分支。<remote name>/<branch name>。o/main 的分支或者叫远程分支，分支就叫 main，远程仓库的名称就是 o (origin)。

// “远程分支”,

<img width="946" alt="image" src="https://user-images.githubusercontent.com/33156021/207225085-a305de55-667e-40ea-b5a3-472a384df31e.png">

// “Git Fetch”,从远程仓库获取数据。具体是：从远程仓库下载本地仓库中缺失的提交记录，然后更新远程分支指针(如 o/main)。

![image](https://user-images.githubusercontent.com/33156021/207225860-dbc5389e-a0c7-4e90-838c-f6215bb1bbb2.png)

// “Git Pull”,先抓取更新再合并到本地分支，git pull 就是 fetch 和 merge 的简写。```git pull``` = ```$ git fetch; git merge o/main;。其他方法：```git cherry-pick o/main; git rebase o/main; git merge o/main```


// “模拟团队合作”

![image](https://user-images.githubusercontent.com/33156021/207247190-16b42653-c4fe-4464-ab21-3458fe75eb4f.png)

// “Git Push”

要完成本关，需要向远程仓库分享两个提交记录。拿出十二分精神吧，后面的课程还会更难哦！

![image](https://user-images.githubusercontent.com/33156021/207248044-4825c7dc-365b-45b6-95cb-e5bda6c5bb8f.png)

```提交两次，一次push```

// “偏离的提交历史”，其他人提交的新的，本地的分支 不匹配 远程的分支时，无法使用push。先fetch下载远程，再rebase本地的提交新分支，在push上传。git pull --rebase 就是 fetch 和 rebase 的简写！

要完成本关，你需要完成以下几步：

克隆你的仓库
模拟一次远程提交（fakeTeamwork）
完成一次本地提交
用 rebase 发布你的工作

// “锁定的Main(Locked Main)”，远程服务器拒绝!(Remote Rejected)。

```$ git checkout -b feature; git branch -f main c1; git push;```

### 远程2 关于 origin 和它的周边 —— Git 远程仓库高级操作

// “推送主分支”，合并特性分支。

这里共有三个特性分支 —— side1 side2 和 side3
我需要将这三分支按顺序推送到远程仓库
因为远程仓库已经被更新过了，所以我们还要把那些工作合并过来

// “合并远程仓库”

![image](https://user-images.githubusercontent.com/33156021/207282733-290be8bf-b869-483a-a49b-a573dd7a2def.png)

```
$ git fetch

$ git branch -f main side1

$ git checkout main

$ git merge o/main

$ git branch -f main side2

$ git merge c9

$ git merge side3

$ git push
```

// “远程追踪”，git checkout -b totallyNotMain o/main，git branch -u o/main foo; git commit; git push

检出一个名叫 foo 的新分支，让其跟踪远程仓库中的 main，使用了隐含的目标 o/main 来更新 foo 分支。```git checkout -b foo o/main; git pull; ```

将一个并不叫 main 的分支上的工作推送到了远程仓库中的 main 分支上 ```git checkout -b foo o/main; git commit; git push; ```

另一种设置远程追踪分支的方法就是使用：```git branch -u o/main foo```。foo 就会跟踪 o/main 了。如果当前就在 foo 分支上, 还可以省略 foo：```git branch -u o/main```


$ git checkout -b side o/main

$ git commit

$ git pull --rebase

$ git push



// “Git push 的参数”，git checkout c0; git push origin main;

![image](https://user-images.githubusercontent.com/33156021/207307369-b50f36a3-97ca-4c2f-b5a0-61df3b23ccd0.png)

```$ git push origin main; git push origin foo;```

















































































## References
【『教程』简单明了的Git入门】 https://www.bilibili.com/video/BV1Cr4y1J7iQ/?share_source=copy_web&vd_source=0345e3adc20ae50104198aff12c0c9e6
