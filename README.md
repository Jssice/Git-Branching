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

// 符号"HEAD", 指向你正在其基础上进行工作的提交记录

// cat .git/HEAD 查看， 如果 HEAD 指向的是一个引用，还可以用 git symbolic-ref HEAD 查看它的指向。

// git log 来查查看提交记录的哈希值






// 分离HEAD

从 bugFix 分支中分离出 HEAD 并让其指向一个提交记录。

通过哈希值指定提交记录。每个提交记录的哈希值显示在代表提交记录的圆圈中。

<img width="929" alt="image" src="https://user-images.githubusercontent.com/33156021/207018527-43826273-0016-4793-bec9-2fb0a8c5cc8b.png">

''' Linux
$ git checkout c4
'''

// “相对引用（^）”，使用 ^ 向上移动 1 个提交记录

切换到 bugFix 的父节点。这会进入分离 HEAD 状态。

<img width="929" alt="image" src="https://user-images.githubusercontent.com/33156021/207019790-0338d6ef-a3d6-44ff-84fa-5c62b3cbf637.png">

$ git checkout bugFix^

// “相对引用2（~）”，使用 ~<num> 向上移动多个提交记录，如 ~3。使用 -f 选项让分支指向另一个提交。git branch -f main HEAD~3。-f 则容许我们将分支强制移动到那个位置。

移动 HEAD，main 和 bugFix 到目标所示的位置。

<img width="929" alt="image" src="https://user-images.githubusercontent.com/33156021/207021132-2c3711d5-24b3-44d3-b90f-bf0c754bfb01.png">

$ git checkout bugFix; git branch -f bugFix HEAD~3;
  
$ git checkout c6; git branch -f main HEAD;
  
$ git checkout c1;

// “撤销变更”，git reset 向上移动分支，原来指向的提交记录就跟从来没有提交过一样，$ git reset HEAD~1, $ git revert HEAD. 

<img width="956" alt="image" src="https://user-images.githubusercontent.com/33156021/207025264-745a61d4-0b97-4f4c-8225-c5da2c10a9ec.png">

$ git branch -f local HEAD~1; git checkout pushed; git resert HEAD;


### 整理提交记录

// “Git Cherry-pick”,







  
## References
【『教程』简单明了的Git入门】 https://www.bilibili.com/video/BV1Cr4y1J7iQ/?share_source=copy_web&vd_source=0345e3adc20ae50104198aff12c0c9e6
