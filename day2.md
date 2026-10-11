# 如何上传GitHub

## 一、检查本地仓库是否全部上传

进入仓库地址，输入：

```bash
git status
```

如果显示：

```bash
On branch main
nothing to commit, working tree clean
```

如果显示还有文件没提交，则需要输入：

```bash
git add 文件名
git commit -m "提交说明"
```

## 二、检查有没有嵌套仓库

输入：

```bash
find . -name .git -type d
```

如果显示：

```bash
./.git
./test/.git
```

则说明`test`为嵌套仓库，在此阶段使用·`rm -rf`删除，输入：

```bash
rm -rf test/.git
git add .
git commit -m "chore: 移除嵌套仓库，整理目录"
```

## 三、GitHub上建立远程仓库

登入GitHub后，进入主页，点击**`new repository`**创建新仓库，同时需注意，不要勾选**`Add a README file`**，**`Add .gitignore`**，**`Choose a license`**因为在创建本地git仓库时，文件已经存在，为避免冲突，则需要创建一个远程空仓库。

创建仓库成功后，页面会显示`HTTPS`或`SSH`，显示大致如下：

```htto
https://github.com/你的用户名/git-day1.git
git@github.com:你的用户名/git-day1.git
```

这里为了方便，我们选择`HTTPS`方式来进行上传。

## 四、关联仓库：git remote add origin

在git内输入：

```bash
git remote add origin https://github.com/你的用户名/git-day1.git
```

### 查看是否添加成功：git remote -v

应该显示如下：

```bash
origin  https://github.com/你的用户名/git-day1.git (fetch)
origin  https://github.com/你的用户名/git-day1.git (push)
```

如果显示：

```bash
error: remote origin already exists.
```

则表示已经添加过，可以直接进行修改地址，输入：

```bash
git remote set-url origin https://github.com/你的用户名/git-day1.git
```

## 五、确保分支名是main：git branch -m main

意思为把当前分支强制命名为main，输入：

```bash
git branch -m main
```

## 六、推送到GitHub：git push -u origin main

代码解释：**`push`**：上传；**`-u`**：设置上有分支，以后直接`push`即可，**`origin`**：远程仓库名字。**`main`**：要推送的主分支。

第一次或许会弹出登入，直接按照提示进行操作即可。

上传成功后，刷新GitHub界面查看是否有内容显示。

## 七、拉取远程更新：git pull

因为在前端我们输入了：

```bash
git push -u origin main
```

所以在拉取远程更新时，只需要输入：

```bash
git pull
```

## 八、如何克隆仓库：git clone

进入到一个空文件夹，随后在git内输入：

```bash
git clone HTTPS/SSH
```

等待一会便发现仓库的文件夹内容已经复制到文件夹下，如果需要查看提交内容，则进入对应文件夹下，输入：

```bash
git log --oneline
```

即可。

## 九、删除已上传文件

### 9.1 git删除，本地也删除：git rm 文件名

输入：

```bash
git rm 文件名
git rm -r 文件夹名字
```

随后输入：

```bash
git commit -m "删除文件"
git push
```

即可。

### 9.2 git删除，保留本地文件：git rm -cached

需要取消追踪文件，输入：

```bash
git rm -cached 文件名
```

要想确认文件有没有被追踪，可以输入：

```bash
git ls-files 文件名
```

将文件从暂存区里删除后，输入：

```bash
git commit -m "不追踪文件"
```

### 9.3 加入`.gitignore`

如果想要文件不上传，可以通过写入`gitignore`，输入：

```bash
echo "文件名" >> .gitignore
```

然后提交即可。

## 十、回退文件版本：git restore --source=HEAD 文件名

如果文件或文件夹在某一次的修改后发生了错误，需要进行回退，输入：

```bash
git log --oneline -- 文件名
```

获得到文件的哈希值后，输入：

```bash
git show HEAD:文件名
```

恢复到工作区，输入：

```bash
git restore --source=HEAD 文件名
```

随后查看差异，确认无误后提交即可。

## 十一、所使用的代码

|               命令               |             含义             |
| :------------------------------: | :--------------------------: |
|            git status            |   查看仓库内容是否全部上传   |
|    find . -name .git -type d     |     查看是否有嵌套的仓库     |
|      git remote add origin       |       添加远程仓库地址       |
|    git remote set-url origin     |       修改远程仓库地址       |
|          git remote -v           | 查看远程仓库地址是否添加成功 |
|        git branch -m main        |     当前分支强命名为main     |
|     git push -u origin main      |         上传main分支         |
|             git pull             |         拉取远程仓库         |
|            git clone             |         复制远程仓库         |
|        git log --oneline         |       查看历史提交信息       |
|              git rm              |    git和本地删除文件信息     |
|          git rm -cached          |    删除git，保留本地文件     |
|   echo "文件名" >> .gitignore    |    将忽略文件加入到忽略区    |
| git restore --source=HEAD 文件名 |  将文件恢复到对应的HEAD版本  |
