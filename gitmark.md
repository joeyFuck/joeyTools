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
# 示例

## D:\javaProduct\信用定价\vue-hengtai-admin>git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   public/static/config/env.js
        modified:   src/api/menu.js
        modified:   src/api/workflow.js
        modified:   src/settings.js
        modified:   src/views/workflow/taskDealed/list.vue

no changes added to commit (use "git add" and/or "git commit -a")

## D:\javaProduct\信用定价\vue-hengtai-admin>git branch
* master

## D:\javaProduct\信用定价\vue-hengtai-admin>git add .
warning: LF will be replaced by CRLF in public/static/config/env.js.
The file will have its original line endings in your working directory.
...

## D:\javaProduct\信用定价\vue-hengtai-admin>git commit -m "配置文件本地暂存"
[master warning: LF will be replaced by CRLF in public/static/config/env.js.
The file will have its original line endings in your working directory.
warning: LF will be replaced by CRLF in src/api/menu.js.
The file will have its original line endings in your working directory.
...
 5 files changed, 279 insertions(+), 69 deletions(-)

## D:\javaProduct\信用定价\vue-hengtai-admin>git checkout develop
error: pathspec 'develop' did not match any file(s) known to git.

## D:\javaProduct\信用定价\vue-hengtai-admin>git pull
fatal: unable to get credential storage lock: File exists
remote: Enumerating objects: 35, done.
remote: Counting objects: 100% (35/35), done.
remote: Compressing objects: 100% (19/19), done.
remote: Total 19 (delta 11), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (19/19), done.
From http://gitlab.xquant-cdb.com/design/vue-hengtai-admin
 * [new branch]      develop    -> origin/develop
 * [new branch]      vue_dev_jmm -> origin/vue_dev_jmm
Already up-to-date.

## D:\javaProduct\信用定价\vue-hengtai-admin>git branch -a
* master
  remotes/origin/develop
  remotes/origin/master
  remotes/origin/vue_dev_jmm

## D:\javaProduct\信用定价\vue-hengtai-admin>git checkout develop
Branch develop set up to track remote branch develop from origin.
Switched to a new branch 'develop'

## D:\javaProduct\信用定价\vue-hengtai-admin>git branch
* develop
  master

## D:\javaProduct\信用定价\vue-hengtai-admin>git merge master
Updating a6b2ca9..28b6e89
Fast-forward
 public/static/config/env.js                        |    4 +-
 src/api/menu.js                                    |  211 ++-
 .../creditPricing/microSpreads/corp/index.vue      |  490 +++++++
 src/views/workflow/taskDealed/list.vue             |  120 +-
 11 files changed, 4978 insertions(+), 69 deletions(-)
 create mode 100644 src/views/creditPricing/microSpreads/bond/data.vue
 create mode 100644 src/views/creditPricing/microSpreads/bond/degreeOfDeviation.vue
...

## D:\javaProduct\信用定价\vue-hengtai-admin>git checkout public/static/config/env.js

## D:\javaProduct\信用定价\vue-hengtai-admin>git status
On branch develop
Your branch is ahead of 'origin/develop' by 2 commits.
  (use "git push" to publish your local commits)
nothing to commit, working directory clean

## D:\javaProduct\信用定价\vue-hengtai-admin>git checkout src/api/menu.js

## D:\javaProduct\信用定价\vue-hengtai-admin>git checkout src/settings.js

## D:\javaProduct\信用定价\vue-hengtai-admin>git checkout  src/settings.js

## D:\javaProduct\信用定价\vue-hengtai-admin>git status
On branch develop
Your branch is ahead of 'origin/develop' by 2 commits.
  (use "git push" to publish your local commits)
nothing to commit, working directory clean

## D:\javaProduct\信用定价\vue-hengtai-admin>git add .

## 把master内容合并过来
## D:\javaProduct\信用定价\vue-hengtai-admin>git commit -m "merge master"
On branch develop
Your branch is ahead of 'origin/develop' by 2 commits.
  (use "git push" to publish your local commits)
nothing to commit, working directory clean

## D:\javaProduct\信用定价\vue-hengtai-admin>git pull origin develop
fatal: unable to get credential storage lock: File exists
From http://gitlab.xquant-cdb.com/design/vue-hengtai-admin
 * branch            develop    -> FETCH_HEAD
Already up-to-date.

## D:\javaProduct\信用定价\vue-hengtai-admin>git push origin develop
fatal: unable to get credential storage lock: File exists
Counting objects: 15, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (14/14), done.
Writing objects: 100% (15/15), 3.45 KiB | 0 bytes/s, done.
Total 15 (delta 11), reused 0 (delta 0)
remote:
remote: To create a merge request for develop, visit:
remote:   http://gitlab.xquant-cdb.com/design/vue-hengtai-admin/-/merge_requests/new?merge_request%5Bsource_branch%5D=develop
remote:
To http://gitlab.xquant-cdb.com/design/vue-hengtai-admin.git
   a6b2ca9..28b6e89  develop -> develop





