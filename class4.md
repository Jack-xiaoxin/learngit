## 分支管理

分支就是科幻电影里面的平行宇宙，当你正在电脑前例如学习Git的时候，另一个你正在平行宇宙努力学习SVN。如果两个平行宇宙互不干扰，那对现在的你也没啥影响。不过在某个时间点，两个平行宇宙合并了，结果，你既学会了Git，又学会了SVN！

当我们创建了一个属于我们自己的分支后，别人看不到，继续在原来的分支上正常工作，而你在自己的分支上干活，想提交就提交，直到开发完毕后，再一次性合并到原来的分支上。这样既安全，又不影响别人工作。



## 创建与合并分支

我们已经知道，每次提交，Git都把它们串成一条时间线，这条时间线就是一个分支。

一开始的时候，master分支是一条线，Git用master指向最新的提交，再用Head指向master，就能确定当前分支，以及当前分支的提交点。

![image-20210425105339089](C:\Users\91501\AppData\Roaming\Typora\typora-user-images\image-20210425105339089.png)

每次提交，master分支都会向前移动一步，这样，随着我们不断提交，master分支的线也越来越长。

当我们创建新的分支，例如dev时，Git新建了一个指针叫dev，指向master相同的提交，再把HEAD指向dev，就表示当前分支在dev上。

![image-20210425105557652](C:\Users\91501\AppData\Roaming\Typora\typora-user-images\image-20210425105557652.png)

从现在开始，对工作区的修改和提交就是针对dev分支了，比如新提交一次，dev指针往前移动一步，而master指针不变：

![image-20210425105727415](C:\Users\91501\AppData\Roaming\Typora\typora-user-images\image-20210425105727415.png)

假如我们在dev上的工作完成了，就可以把dev合并到master上，直接把master指向dev当前的提交就完成了合并：

![image-20210425105832950](C:\Users\91501\AppData\Roaming\Typora\typora-user-images\image-20210425105832950.png)

#### 实战练习

1、创建并切换到分支

```
git switch -c dev
```

这条指令的作用与以下两条指令一样：

```git
git branch dev
git switch dev
```

2、查看分支

```git
git branch
```

3、分支合并（执行此命令时先切换到master分支）

```git
git merge dev
```

4、删除分支

```git
git branch -d dev
```



## 解决冲突

当所创建的分支和当前分支均有新的提交时，合并时会发生冲突：

![image-20210425110756192](C:\Users\91501\AppData\Roaming\Typora\typora-user-images\image-20210425110756192.png)



![image-20210425153617369](C:\Users\91501\AppData\Roaming\Typora\typora-user-images\image-20210425153617369.png)



查看readme.md的内容，发现不同分支的内容被标记了出来：

![image-20210425153808695](C:\Users\91501\AppData\Roaming\Typora\typora-user-images\image-20210425153808695.png)

我们手动更改这个文件，然后git add，git commit即可：

![image-20210425154004391](C:\Users\91501\AppData\Roaming\Typora\typora-user-images\image-20210425154004391.png)

![image-20210425154029591](C:\Users\91501\AppData\Roaming\Typora\typora-user-images\image-20210425154029591.png)

#### 查看分支情况

```git
git log [--graph]
```

![image-20210425154225705](C:\Users\91501\AppData\Roaming\Typora\typora-user-images\image-20210425154225705.png)

## 分支管理策略

通常合并分支时，Git默认会采用Fast-forward模式。如果强制禁用Fast forward模式，Git会在merge时生成一个新的commit，这样，从分支历史就可以看出分支信息。

```git
git merge --no-ff -m "merge with no-ff" dev
```

![image-20210425155245709](C:\Users\91501\AppData\Roaming\Typora\typora-user-images\image-20210425155245709.png)

## Bug分支

在Git中，由于分支是如此强大，所以，每个bug都可以通过一个新的临时分支来修复，修复后，合并分支，然后将临时分支删除。

当接到一个修复一个代号为101的bug的任务时，很自然地，我们想创建一个分支issue-101来修复它，但是，当前在dev上进行的工作还没有提交。假设dev上的工作还有一天完成，而bug只需要两个小时就能完成，怎么办呢？

```git
git stash
```

git stash可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作。

当我们修复好bug并合并到master时，可以使用以下命令恢复现场继续dev的工作：

```git
git stash apply [stash@{0}]
```

可以使用以下命令查看有哪些stash：

```git
git stash list
```

往往dev上也有类似的bug，我们只需要把bug merge到master的commit的命令的commit id记住，然后：

```git
git cherry-pick {commit id}
```

## Feature分支

开发一个新feature，最好新建一个分支

如果要丢弃一个没有合并过的分支，可以通过以下命令：（注意D是大写的，表示强制删除）

```git
git branch -D <name>
```

## 多人协作

#### 查看远程仓库的情况

```
git remote
git remote -V
```

![image-20210425161930504](C:\Users\91501\AppData\Roaming\Typora\typora-user-images\image-20210425161930504.png)

上面显示了可以抓取和推送的origin的地址，如果没有推送权限，就看不到push的地址。

#### 推送分支

```git
git push origin master
```

如果要随送其他分支：

```git
git push origin dev
```

未完待续.....