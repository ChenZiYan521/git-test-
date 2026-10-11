# 第一天，常用命令和含义

## 一、如何创建git工作区

找到代码存放的文件夹，随后进行右键，选择git打开。

### 1.1 如何添加新文件夹

如果需要在工作区添加新文件夹，可以输入：

``` bash
git mkdir 文件夹名称
```

### 1.2 如何删除文件夹

如果需要在工作区删除某一个文件夹，可以输入：

```bash
rm -rf 文件夹名称
```

## 二、配置用户名和邮箱

输入：

```bash
git config --global user.name "你的名字"
git config --global user.email "你的邮箱"
```

验证：

```bash
git config --global --list
```

## 三、初始化git仓库

在代码存放文件夹下输入：

```bash
git init -b main
```

等文件夹下新建一个.git文件夹即可

## 四、上传文件到本地仓库

### 4.1 将文件提交到暂存区

上传文件主要流程：工作区-暂存区-本地仓库。

当新文件创建后，输入：

```bash
git status
```

后可以看到：

```bash
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        README.md
```

这就意味着git没有跟踪到这个文件，所以需要输入：

```bash
git add README.md
```

后，将文件提交至暂存区，等待进一步提交到本地仓库。同时，如果一次性添加了多个新文件，可以输入：

```bash
git add .
```

来进行提交。

当文件提交到暂存区后，可以输入：

```bash
git status
```

来查看文件状态，一般显示：

```bash
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   README.md
```

当显示上述情况时，意味着文件已经在暂存区等待进一步提交。

### 4.2 将文件提交到本地仓库

当文件提交到暂存区后，可以输入：

```bash
git commit -m "docs: 添加 README"
```

来将文件提交到本地仓库，一般显示：

```bash
[main (root-commit) a1b2c3d] docs: 添加 README
 1 file changed, 3 insertions(+)
 create mode 100644 README.md
```

可以通过输入：

```bash
git log --oneline
```

来查看历史提交信息。

### 4.3 修改文件后提交

当文件被修改后，通过输入：

```bash
git status
```

来查看信息，一般显示为：

```bash
Changes not staged for commit:
        modified:   README.md
```

意思是，文件已经修改，但是没有放进暂存区。

同时为了查看修改的内容，可以输入：

```bash
git diff
```

来进行查看，一般显示为：

```bash
+## 今天学会的命令
+
+- git init
+- git status
+- git add
+- git commit
+- git log
```

`+` 表示新增的行，`-` 表示删除的行。

确认无误后，可以输入：

```bash
git add README.md
git commit -m "docs: 记录第一天命令"
git log --oneline
```

来进行提交，一般历史提交记录显示为：

```bash
b2c3d4e docs: 记录第一天命令
a1b2c3d docs: 添加 README
```

同时注意到，每一次提交前都会存在一串字符比如：`a1b2c3d`；意思为这一次提交的哈希值，哈希值具有唯一性。

## 五、如何查看某文件的修改信息

已知每一次的提交，都会输出一个具有唯一性的哈希值，所以只需要通过对应历史的哈希值即可进行范文，输入：

```bash
git show HEAD~1
```

可以查看上一版的提交记录，如果要查看前几版，可以通过修改`~`后的数字来实现。同时也可以通过输入：

```bash
git log --oneline
```

来查看历史提交记录信息，比如输出：

```bash
249b0c1 (HEAD -> main) 把文件夹调整到主文件夹下。
xxxxxxx 第二次提交
yyyyyyy 第一次提交
```

随后可以输入：

```bash
git show xxxxxxx\yyyyyyy
```

来进行对应版本的查看。

### 5.1 查看某文件在某一版的改动信息：git show

```bash
git show HEAD
```

查看最新一次提交的详细信息，包括：

- 提交哈希
- 作者、时间
- 提交说明
- 具体改了哪些文件、哪些行

#### 5.1.1 看上一版：

```bash
git show HEAD~1
```

#### 5.1.2 看指定版本：

```bash
git show 249b0c1
```

#### 5.1.3 看某次提交里某个文件：

```bash
git show 249b0c1 -- README.md
```

#### 5.1.4 输出里的符号：

- `+` 新增的行
- `-` 删除的行
- `@@` 表示改动在文件的哪一段

如果需要查看某文件在某一个版本的改动，可以输入：

```bash
git show HEAD -- README.md
```

如果进入`less`模式，按`q`即可推出。

### 5.2 查看同一文件两版本之间的差异：git diff

#### 5.2.1 工作区和最新提交比

```bash
git diff
```

意思是：我还没提交的修改，和 `HEAD` 比，差在哪。

#### 5.2.2 暂存区和最新提交比

```bash
git diff --staged
```

意思是：我已经 `git add` 但还没提交的内容，和 `HEAD` 比，差在哪。

#### 5.2.3 两个提交之间比

```bash
git diff 249b0c1 HEAD
```

意思是：从 `249b0c1` 到 `HEAD`，一共改了什么。

更早和更晚：

```bash
git diff HEAD~2 HEAD~1
```

#### 5.2.4 两个分支之间比

```bash
git diff main feature
```

意思是：`feature` 比 `main` 多了哪些改动。

#### 5.2.5 只看某个文件

```bash
git diff 249b0c1 HEAD -- README.md
```

### 5.3 查看某文件的历史：git log

#### 5.3.1 简洁列表

```
git log --oneline
```

输出：

```text
249b0c1 (HEAD -> main) 修改说明
57ff4f3 第二次提交
320f7e1 第一次提交
```

#### 5.3.2 带作者和时间

```bash
git log
```

#### 5.3.3 图形化

```bash
git log --oneline --graph --all
```

有分支时特别有用。

#### 5.3.4 看某个文件的历史

```bash
git log --oneline -- README.md
```

只显示改过 `README.md` 的提交。

#### 5.3.5 看每次提交改了哪些文件

```bash
git log --stat
```

输出每个提交改了哪些文件、增删多少行。

#### 5.3.6 看每次提交的具体内容

```bash
git log -p
```

相当于对每个提交依次执行 `git show`。

#### 5.3.7 看某几行是谁改的

```bash
git log -L 1,10:README.md
```

查看 `README.md` 第 1 到 10 行的修改历史。

### 5.4 看某个文件在某一版的内容：git show 版本:文件

```bash
git show HEAD:README.md
git show 249b0c1:README.md
git show HEAD~1:one.txt
```

注意冒号前后不能有空格：

```bash
git show 249b0c1:README.md
```

这不会修改工作区，只是把那个版本的文件内容打印出来。

**如果想导出到文件：**

```bash
git show 249b0c1:README.md > old-readme.md
```

## 六、第一天常用命令汇总

| 目的             | 命令                                                         |
| :--------------- | :----------------------------------------------------------- |
| 创建文件夹       | mkdir 文件夹名称                                             |
| 删除文件夹       | rm -rf 文件夹名称                                            |
| 配置用户信息     | git config --global user.name "你的名字"<br/>git config --global user.email "你的邮箱" |
| 查看用户配置信息 | git config --global --list                                   |
| 创建工作区       | git init -b main                                             |
| 提交暂存区       | git add 文件名<br/>git add .                                 |
| 提交本地仓库     | git commit -m "提交说明："                                   |
| 检查仓库状态     | git status                                                   |
|                  |                                                              |
|                  |                                                              |
|                  |                                                              |
|                  |                                                              |