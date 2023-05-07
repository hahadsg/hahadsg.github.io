# 参考

https://git-scm.com/book/en/v2

# 符号注意

```
# 使用*需要转义
git add log/\*.log
```

# 常用命令

## branch

* new branch

```bash
git push -u origin <branch>
```

* delete branch

```bash
# 本地
git branch -d <branch>
# 远端
git push origin :<branch>
```

## tag

* add tag

```bash
# 增加标签
git tag -a v1.4 -m 'my version 1.4'
# push一个标签
git push origin v1.5
# push本地所有标签
git push origin --tags
```

* delete tag

```
# 本地
git tag -d v1.0
# remote
git push --delete origin v1.0
```

* show tag

```bash
# 按照taggerdate排序 显示annotate
git tag --sort=taggerdate -n
# taggerdate设为默认排序
git config tag.sort taggerdate
```

## config

```
# 显示所有配置
git config --list

# 显示单个配置
git config [config_name]

# 配置name email
git config --global user.name "Your Name"
git config --global user.email "email@example.com"

# 解决status中文乱码问题
git config --global core.quotepath false

# 配置push大小限制（500M）
git config --global http.postBuffer 524288000

# 开启颜色
git config --global color.status auto
git config --global color.diff auto
git config --global color.branch auto
git config --global color.interactive auto

# 保存credential 不用重复输入账号密码
git config --global credential.helper store
# 如果有多个git账号对应不同的仓库
git config --global credential.useHttpPath true
```

* set url

```
git remote set-url origin https://...
git remote set-url --push origin https://...
```

## diff

```
# This command compares your staged changes to your last commit
git diff --staged

# 显示diff的文件 以及删增情况
git diff --stat [commit]
```

## log

```
# 显示diff
git log -p/--patch
# 限制log数
git log -10

# log只显示为一行
git log --pretty=oneline
# 显示log树
git log --pretty=oneline --graph
```

* decorate

```bash
# 显示分支、tags等信息
git log --decorate
# 也可以通过配置默认开启
git config log.decorate auto
```

## HEAD

`HEAD`相当于指针，指向当前commit
`HEAD^`表示上一个commit
`HEAD^^`表示上上个commit
`HEAD~100`表示往前推100个commit
`HEAD^`与`HEAD~1`等价

## commit

* 漏掉一些文件没commit

```
git commit -m 'initial commit'
git add [forgotten_file]
git commit --amend
```

## reset

```
# 回退到某个commit
git reset --hard [commit]
```

## gitignore

* 忽略数据文件，除非在制定文件夹中

```
*.csv
*.txt
*.xlsx

!**/reserve/**

```

## clean

```bash
# show clean files(untracked files)
git clean -n
# remove untracked files
git clean -f

# remove dir
git clean -f -d
# remove ignored files
git clean -f -X
# remove ignored and non-ignored files
git clean -f -x
```

# 专题

## 清理所有git历史

### 方法1（有submodule也可以用）

Checkout

```sh
git checkout --orphan latest_branch
```

Add all the files

```sh
git add -A
```

Commit the changes

```sh
git commit -am "commit message"
```

Delete the branch

```sh
git branch -D master
```

Rename the current branch to master

```sh
git branch -m master
```

Finally, force update your repository

```sh
git push -f origin master
```

### 方法2

-- Remove the history from 
rm -rf .git

-- recreate the repos from the current content only
git init
git add .
git commit -m "Initial commit"

-- push to the github remote repos ensuring you overwrite history
git remote add origin git@github.com:<YOUR ACCOUNT>/<YOUR REPOS>.git
git push -u --force origin master

