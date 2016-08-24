# Git使用简介

## 安装
参考 [Git权威指南－安装Git章节](http://www.worldhello.net/gotgit/01-meet-git/030-installation.html)

## 设置个人信息（姓名、邮箱）
- `git config --global user.name "<yourname>"`
- `git config --global user.email "<yourEmail>"`

## 初次操作，熟悉git工作流程
1. 在一个目录下初始化git版本库 `git init`
2. 添加目录下已经存在的文件到暂存区（stage） `git add <file>`
3. 提交 `git commit -m 'initial commit'`
4. 查看日志 `git log`

## 基本概念
- 工作区：新建或修改并保存文件后，未提交到暂存区的文件
- 暂存区（stage）：执行`git commit`时，暂存区记录的文件变动会成为一个提交（commit），之后暂存区被清空
- 提交（commit）：记录了一个或多个父提交到本次提交之间的文件变动，它的名称（或者说id）是一个hash值。
  commit是git的一个基本单位，git很多功能都是以commit为基础做的。
- HEAD: 指向一个commit的指针，代表当前正在工作的位置

## 常用命令
- `git <command> -h` git命令的简短帮助文档

- `git <command> --help` git命令的完整帮助文档

- `git status` 查看工作区与暂存区的差异
  - `git status -s` 简化输出内容，推荐在熟练以后使用

- `git stash` 保存当前工作进度。会对暂存区和工作区的状态分别保存。适用于当前手上的工作暂时没有完成，
  不想提交， 而要拉取的远端最新代码和工作区修改的文件冲突。
  - `git stash pop`: `stash -> git pull -> stash pop`
  - `git stash list` 查看`stash`保存的列表

- `git add <file/dir> <file/dir>...` 将指定文件／目录从工作区添加到暂存区，可以用空格隔开添加多个
  - `git add <file/dir> -i` 进入交互式add模式，推荐使用
  - 建议不要使用`git add .`或`git add -a`添加目录下所有文件到暂存区。第一：容易出错；第二：应该拆分成多个小的、有意义的提交

- `git pull` 拉取远端库

- `git push` 推送到远端库（注意：先拉后推）

- `git diff`
  - `git diff <file>` 比对该文件的工作区与暂存区版本
  - `git diff <commit1> <commit2>` 比对2个commit的差异，如果只写一个commit是与HEAD比对

- `git reset` 等价于`git reset HEAD`,常用于清空暂存区到工作区。
  - `--hard`等参数使用少，可以用到再查文档

- `git reflog` 查看本地操作日志

- `git commit`
  - `git commit -m 'commit messages'` 简短的提交说明
  - `git commit --amend` 对上一次提交重新提交，以修改提交说明或提交内容

- `git tag` tag（里程碑）是commit的语义化别名
  - `git tag <tagName> -m '<tagDesc>'` 对当前commit设立一个tag，并附上tag描述信息
  - tag命名规范：（个人理解）tag是写给人看的，人能看懂就行。单个项目的tag命名要保持一致性
  - `git push --tags` 同步tag到远端，本地创建的tag默认是不同步的
  - `git tag` 查看所有tag
  - `git tag -ln1` 查看所有tag及描述信息

- `git checkout`
  - `git checkout -- <file>` 清除工作区改动，用暂存区文件覆盖工作区文件
  - `git checkout <commit>` 检出到指定提交，进入分离头状态
  - `git checkout <branch>` 检出到指定分支
  - `git checkout -b <newBranch>` 创建一个新分支并检出

## 其它
### 别名（alias）：可以在操作系统shell里设置别名，也可以在git中设置
`git config --global alias.<aliasName> '<command>'`

### .gitignore文件
- 所有空行或#开头的行都会被忽略
- 文件或目录前加 / 表示仓库根目录的对应文件
- 匹配模式最后跟反斜杠 / 说明要忽略的是目录
- 要特殊不忽略某个文件或目录，可以在模式前加上取反`!`
- 已经进入版本库的文件不受忽略规则影响，需要使用`git rm --cached <file>`删除
- 示例

```
# OSX
#
.DS_Store

# Xcode
#
build/
*.pbxuser
!default.pbxuser
*.mode1v3
!default.mode1v3
*.mode2v3
!default.mode2v3
*.perspectivev3
!default.perspectivev3
xcuserdata
*.xccheckout
*.moved-aside
DerivedData
*.hmap
*.ipa
*.xcuserstate
project.xcworkspace

# Android/IJ
#
*.iml
.idea
.gradle
local.properties

# node.js
#
node_modules/
npm-debug.log

# BUCK
buck-out/
\.buckd/
android/app/libs
android/keystores/debug.keystore
```
