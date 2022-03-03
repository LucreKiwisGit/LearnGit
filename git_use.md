# Git 使用手册

![](E:\Learn\Git's Structure.png)

```
Remote:远程仓库
Repository:本地仓库
Index:缓冲区
Workspace:工作区
```

### 一、基本设置

```bash
配置个人信息
git config --global user.name "Lucre"
git config --global user.email "LucreKiwis@gmail.com"

创建本地仓库
git init
```

### 二、几个常用的命令

​		1.提交更改的文件到Index

```bash
提交目录中的所有文件
git add .

当然你也可以单独提交一个文件
git add git_use.md
```

​		2.提交缓冲区里的所有变动到仓库

```bash
git commit -m "Git的基本用法"
[master 8d59de5] Git的基本用法
 2 files changed, 31 insertions(+), 1 deletion(-)
 create mode 100644 Git's Structure.png
 rewrite git_use.md (100%)
 
-m之后的是对本次提交的文字说明
```

​		3.查看仓库与工作区的状态

~~~bash
c
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   git_use.md

no changes added to commit (use "git add" and/or "git commit -a")

查看具体变动
$ git diff
diff --git a/git_use.md b/git_use.md
index 9a9ca23..374129b 100644
--- a/git_use.md
+++ b/git_use.md
@@ -22,10 +22,40 @@ git init

 ### 二、几个常用的命令

-​               提交更改的文件到Index
+​               1.提交更改的文件到Index

-```
-t
+```bash
+提交目录中的所有文件
 git add .
+
+当然你也可以单独提交一个文件
+git add git_use.md
+```
+
+​               2.提交缓冲区里的所有变动到仓库
+
+```bash
+git commit -m "Git的基本用法"
+[master 8d59de5] Git的基本用法
+ 2 files changed, 31 insertions(+), 1 deletion(-)
+ create mode 100644 Git's Structure.png
+ rewrite git_use.md (100%)
+
+-m之后的是对本次提交的文字说明
+```
+
+​               3.查看仓库与工作区的状态
+
+```bash
+$ git status
+On branch master
+Changes not staged for commit:
+  (use "git add <file>..." to update what will be committed)
+  (use "git restore <file>..." to discard changes in working directory)
+        modified:   git_use.md
+
+no changes added to commit (use "git add" and/or "git commit -a")
+
+
 ```

(END)

~~~

​		4.版本回溯与日志查看

```bash
查看每次的提交日志
git log

查看所有的输入过的命令
git reflog

Git有个Head指针指向当前的版本，只需要更改Head指向不同的版本，即可迅速实现版本跳跃。
Head^代表当前版本的前一个版本，如若想要跳跃到之后的版本，可以通过Git Reflog命令查询版本号
git reset --hard Head^^
git reset --hard 8d59de5
```

​		5.丢弃工作区的修改

```bash
（1）如果该修改尚未提交至缓冲区，则撤销修改回到暂存区的状态
（2）如果缓冲区没有修改，则直接回溯到仓库的版本
git restore -- git_use.md

（3）如果已经提交至缓冲区
git reset head -- git_use.md
	此时，撤销缓冲区的修改，返回到工作区；回到（2）
	
（4）如果已经提交至Repository，此时只能进行版本回溯。
```

​		6.删除文件

```
（1）在工作区删除文件
rm git_use.md

(2)提交到缓冲区
git rm git_use.md

(3)提交到本地仓库
git commmit --m "删除文件"

```

