## 查看仓库当前状态

```git
git status 
```

## 查看文件修改内容

```git
git diff
```

## 查看提交历史

```git
git log
git log --pretty=oneline
```

## 版本回退

```git
git reset --hard HEAD^
```

注意：只能回退到已提交的那些版本，并且每次提交都有一个commit id，也可以通过commit id回退

```git
git reset --hard <commit id>
```

由于版本回退后使用 git log，只能查看之前的版本的 commit id，如果不想回退想恢复怎么半？看下一条

## 查看历史命令

```git
git reflog
```

## 工作区和暂存区

工作区（Working Directory）：就是在电脑上能看到的目录。

版本库（Repository）：工作区有一个隐藏目录（.git），这个不算工作区，而是 Git 的版本库。版本库中存了很多东西，其中最重要的是称为 stage （或者叫index）的暂存区，还有当前分支，和指向当前分支的指针 head。

git add，将文件添加到暂存区。

git commit，将暂存区的所有内容提交到当前分支。

## git管理的是修改，而不是文件

第一次修改 --> git add --> 第二次修改 -->  git commit

会发现，只有第一次修改提交了，第二次修改没有被提交 

## 撤销修改

1、没有 git add 到暂存区

```git
git checkout -- <file name>
```

2、已经 git add 到了暂存区

```git
git reset HEAD <file name>
```

git reset 即可以回退版本，又可以把暂存区的修改回退到工作区。（之后再使用 git checkout -- <filename> 即可）

## 删除文件

```git
git rm <filename>
```

