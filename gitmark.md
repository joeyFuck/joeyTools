最好用gitbash，cmd对应grep这种命令不支持


> 1、Updates were rejected because the tip of your current branch is behind
git bash 强制提交 git push -u origin master -f

> 2、忽略某个文件

忽略后，git status就看不到该文件了

```
D:\javaProduct\信用定价\vue-hengtai-admin>git update-index --assume-unchanged public/static/config/env.js
D:\javaProduct\信用定价\vue-hengtai-admin>git status
On branch develop
Your branch is up-to-date with 'origin/develop'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   src/api/menu.js
        modified:   src/settings.js

no changes added to commit (use "git add" and/or "git commit -a")

```

恢复
```
git update-index --no-assume-unchanged public/static/config/env.js
```

查看所有assume-unchanged的文件
```
git ls-files -v | grep '^h\ '
```

> 3、分支合并
```
1.先提交一波  为后续切分支准备

(xxx1为自己的分支  xxx2为想要拉取的分支)

git add .

git commit -m 'yyy'

git push origin xxx1

2.然后git切换到你所要拉取的分支xxx2  拉取该分支代码

git checkout xxx2

git pull origin xxx2 或者git fetch origin xxx2

3.切回自己的分支

git checkout xxx1

git merge xxx2

完事
```


> 4、提交步骤

https://blog.csdn.net/qq_42602515/article/details/107232894

```
current branch zhongtai-feature-dev1223
git add .
git commit -m "message"
git pull origin zhongtai-dev
--vi 
--confict
  git add
  git commit -m "fix conflict"
git push origin zhongtai-feature-dev1223:zhongtai-feature-devQj

再导gitlab zhongtai-feature-dev1223 =》 request merge into zhongtai-dev

merge pass


=====
git checkout zhongtai-dev
git pull origin zhongtai-dev
git checkout -b zhongtai-feature-dev1224

...
```

> 5、clone时指定分支

git clone -b branchA http://admin@192.168.1.101:7070/r/virtualbox_all_versions.git  文件夹名（optional）

> 6、windows下clone时，目录太长

git config --system core.longpaths true

> 7、git 查看commit

git log

git show

    首先，需要通过git log打印所有commit hashID，之后的git show都是基于commit hashID输出的。

1.查看最新的commit

git show

2.查看指定commit hashID的所有修改：

git show commitId

> 8、查看分支

git branch --all
删除分支
git branch -D <branchName>

> 9、git从指定的commit创建分支

先clone project对应分支

```
git checkout -b justin a9c146a09505837ec03b
This will create the new branch and check it out.

git branch justin a9c146a09505837ec03b
This creates the branch without checking it out.
```

> 10、放弃本地所有修改

```
git checkout . #本地所有修改内的。没有的提交的，都返回到原来的状态

git stash #把所有没有提交的修容改暂存到stash里面。可用git stash pop回复。
git reset --hard HASH #返回到某个节点，不保留修改。
git reset --soft HASH #返回到某个节点。保留修改

对于新增的文件，也舍弃。只需把文件夹都删了，再git checkout .
```

> 11、本地拉取远程分支
  
```
*将远程分支拉到本地：git fetch origin dev（dev即分支名）
 拉取后，通过git branch --all 查看所有分支
 再切换到该分支上
 git checkout dev 
```



