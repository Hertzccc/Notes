# git 学习笔记

- git checkout $brachname: 切换到branch

- git checkout -b $branchname: 创建一个branch，并切换到该branch
  - git merge $branchname: 合并两个分支，即所在分支和$branchname
- ^是当前branch的parent节点：git checkout HEAD^
- git branch -f main HEAD~3： 将main分支强制指向HEAD的第三级parent提交
- git reset HEAD^1：直接撤回提交，在本地像从来不存在之前的新提交分支
- git revert HEAD: 相当于在云端新建了一个分支，这个分支是用来保存”撤销“
- git cherry-pick C1 C2 C3: 将C1,C2,C3复制到当前分支
- git rebase -i HEAD~4: 调出UI界面，
- git commit --amend: 提交最近的小改动
- git tag V1 C1: 给C1打上V1的里程碑（标签
- git tag -d V1: 删掉V1 tag
- git describe main: 返回 tag_num_hash: 
  - tag: 距离ref（这里是main）最近的tag
  - num：ref距离tag有几个节点
  - hash：ref对应的hash
- git checkout HEAD^2: 切换到第二条parent分支，默认是切换为第一个parent分支，如果不加^2
- git checkout HEAD~2: 切换到grandparent分支



远程

- 远程分支: origin/main，即使在origin/main提交，也不会更新。因为origin/main只有在远程仓库中相应分支更新后才会更新。此时git变成了分离HEAD状态

  - 输入<img src="./git%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0.assets/Screen%20Shot%202024-03-11%20at%2014.36.00-0138968.png" alt="Screen Shot 2024-03-11 at 14.36.00" style="zoom: 33%;" />

  - 

<img src="./git%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0.assets/Screen%20Shot%202024-03-11%20at%2014.36.28-0138994.png" alt="Screen Shot 2024-03-11 at 14.36.28" style="zoom:33%;" />

- git fetch: 理解为下载操作
- git pull: 是 git fetch 和 git merge的缩写, 
- git push：推送本地的变更到远程仓库
- git pull --rebase: 就是git fetch;  git rebase的简写