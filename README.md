# Git-Branching


##### 符号解释

* 表示当前分支


//合并分支 
git merge main

// 合并分支rebase，取出一系列的提交记录，“复制”它们，另外一个地方逐个的放下去。优势就是可以创造更线性的提交历史。
新建并切换到 bugFix 分支
提交一次
切换回 main 分支再提交一次
再次切换到 bugFix 分支，rebase 到 main 上
<img width="1234" alt="image" src="https://user-images.githubusercontent.com/33156021/207016961-779a4bb1-37bb-4f99-879c-bf05baaab068.png">


[交互练习git](https://learngitbranching.js.org/?locale=zh_CN)






## References
【『教程』简单明了的Git入门】 https://www.bilibili.com/video/BV1Cr4y1J7iQ/?share_source=copy_web&vd_source=0345e3adc20ae50104198aff12c0c9e6
