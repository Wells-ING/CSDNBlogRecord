## Git高级用法

#### 1. GitHub版本回退

```shell
# 强行推送
git push -f 
```

### 2. 保存工作状态

```shell
# 列出所有保存的工作状态
git stash list
# 保存工作状态
git stash
# 保存工作状态，并添加保存信息
git stash save "some message"
# 恢复指定工作状态
git stash apply stash@{n}(n为整数数值)
# 恢复指定工作状态，并删除恢复后的工作状态
git stash pop stash@{n}(n为整数数值)
# 删除指定工作状态
git stash drop stash@{n}(n为整数数值)
# 删除所有工作状态
git stash clear
```

### 3. 合并指定分支

```shell
# 合并HashA分支
git cherry-pick <HashA>
# 合并多个分支
git cherry-pick <HashA> <HashB> ...
# 合并范围内分支，HashA不包含在合并的分支中
git cherry-pick <HashA>..<HashB>
## 注意：该命令HashA的提交历史必须早于HashB的提交历史
# 合并范围内分支，HashA包含在合并的分支中
git cherry-pick <HashA>^..<HashB>
```

注意：操作类似于git rebase，当与git rebase不同，git rebase作用是将多个分支组合成一个分支，被组合的分支不复存在，但是git cherry-pick 仍存存在被组合的分支，而且git cherry-pick是将某分支的最近一次提交，转移到当前分支（只cherry-pick一个commit ID的情况）。

#### 常见的参数

```shell
# 打开外部编辑器，编辑提交信息
git cherry-pick -e/--edit <HashA>
# 只更新工作区和暂存区，不产生新的提交
git cherry-pick -n/--no-commit <HashA>
## 注意：git add之后不需要git cherry-pick --continue
# 在提交信息的末尾追加一行（cherry picked from commit ...），方便以后查到这个提交是如何产生的
git cherry-pick -x <HashA>
# 在提交信息的末尾追加一行操作者的签名，表示是谁进行了这个操作
git cherry-pick -s/-signoff <HashA>
# 如果原始提交是一个合并节点，来自于两个分支的合并，那么cherry pick默认将失败，因为它不知道应该采用哪个分支的代码变动
-m 参数项告诉Git，应该采用哪个分支的变动。它的参数parent-number是一个从1开始的整数，代表原始提交的父分支编号
git cherry-pick -m/--mainline n <HashA>
## 注意：上面的命令表示，cherry pick采用提交HashA来自编号1的父分支的变动。一般来说，1号父分支是接收变动的分支（the branch being merged into），2号父分支是作为变动来源的分支（the branch being merged from）
```

-m parent-number/ --mainline parent-number

#### 代码冲突

--continue

用户解决代码冲突后，第一步将修改的文件重新加入暂存区（git add .），第二步使用git cherry-pick --continue，让cherry pick过程继续执行

--abort

发生代码冲突后，放弃合并，回到操作前的样子

--quit

发生代码冲突后，推出cherry pick，但是不会到操作前的样子

注意：在一定情况下，git cherry-pick可以代替git merge的工作