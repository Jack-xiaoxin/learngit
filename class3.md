## 分布式版本控制系统

Git是分布式版本控制系统，同一个Git仓库，可以分布到不同的机器上。最早，肯定只有一台机器上有一个原始版本库，此后，别的机器可以“克隆”这个原始版本库，而且每台机器的版本库其实都是一样的，并没有主次之分。

有GitHub这个神奇的网站之后，我们只需要注册一个GitHub账号，就可以免费获得Git远程仓库。



#### 设置步骤：

1、创建 SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果有了，直接下一步。否则，打开命令行窗口，运行：

```git
ssh-keygen -t rsa -C "youremail@example.com"
```

如果顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的密钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心告诉别人。

2、登录GitHub，打开“Account setting”，“SSH Keys” 页面，点击"Add SSH Key"，填上任意Title，在Key文本框里粘贴id_rsa.pub的内容。

GitHub允许添加多个Key，假定有若干台电脑，一会儿在公司提交，一会儿在家里提交，只要把每台电脑上的Key添加到GitHub，就可以在每台电脑上往GitHub推送了。



#### 添加远程仓库

现在的情景是，已经在本地创建了一个Git仓库，又想在GitHub上创建一个仓库，并且让两个仓库同步，这样，GitHub上的仓库即可以作为备份，又可以让其他人通过该仓库来协作，一举多得。

1、登录GitGub，在右上角点击“Create a new repo”，创建一个新仓库，假设名为 learngit。

2、目前，这个learngit仓库还是空的，我们运行以下命令将本地仓库和远程仓库关联起来

```
git remote add origin https://github.com/Jack-xiaoxin/learngit.git
```

这样，远程仓库的的名字就是origin了。

把本地所有内容推送到远程库上：

```git
git push -u otigin master
```

由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不仅会把本地的master分支内容推送远程新的master分支，还会把本地的master分支和远程的master分支关联起来。以后的推送或拉取时可以简化命令。

如果想接触与远程库的关联，可以使用：

```git
git remote rm origin
```

#### 从远程库克隆

```git
git clone https://github.com/Jack-xiaoxin/learngit.git
```

