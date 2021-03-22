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

```
git cherry-pick <HashA> <HashB> ...
```

注意：操作类似于git rebase

#### 常见的参数

 -e/--edit

-n/--no-commit

-x

-s/--signoff

-m parent-number/ --mainline parent-number

#### 代码冲突

--continue

--abort

--quit

