# git

## 常用命令

### 本地

#### 初始化

- 本地初始化库: `git init`

#### 工作区

- 查看工作区与版本库区别 : `git diff HEAD -- readme.txt`

- 丢弃工作区修改: `git checkout -- readme.txt`

- 删除文件: `rm readme.txt`

#### 暂存区

- 提交到暂存区: `git add readme.txt`

- 撤销暂存区修改: `git reset HEAD readme.txt`

#### 本地库

- 提交到仓库: `git commit -m "wrote a readme file"` 

- 删除版本库文件: `git rm test.txt`

- 显示提交日志: `git log或git log --pretty=oneline` 

- 从版本库恢复文件到本地: `git checkout -- test.txt`

- 版本调整: `git reset --hard HEAD^`上个版本,`git reset --hard commitId`指定commiti的版本

- 查看本地/远程库分支: `git branch`

#### 分支

- 创建分支: `git branch <name>`

- 查看分支: `git branch`

- 切换分支: `git checkout <name>` 或者 `git switch -c <name>`

- 创建+切换分支： `git checkout -b <name>` 或者 `git switch -c <name>`

- 合并到当前分支： 
  
  - `git merge <name>` : 创建一个新节点合并
  
  - `git rebase <name>`: 合并到当前节点

- 删除分支： `git branch -d <name>`

- 查看分支合并图: `git log --graph`

- 禁用Fast forward合并分支 `git merge --no-ff -m "merge with no-ff" dev``


输入命令的记录: `git reflog` 

查看状态: `git status` 

 

### 远程库相关

- 本地库关联远程库 : `git remote add origingit@github.com:lijinsheng415/div.git`

- 本地库推送到远程库: 
  
  - 远程库为空使用`git push -u origin main` 
  
  - 远程库不为空使用`git push origin main

- 查看远程库信息: `git remote -v`

- 删除远程库 `git remote rm origin`

- 远程库克隆到本地: `git clone git@github.com:lijinsheng415/git.git`

- 查看本地/远程库分支: `git branch -r`

## git安装

1.下载git国内windows 下载地址 : [CNPM Binaries Mirror](https://registry.npmmirror.com/binary.html?path=git-for-windows/)

2. 安装,按流程安装后,开始菜单出现 “Git”->“Git Bash” 就是安装成功

3. 在命令行 设置自己的名字邮箱
   
   ```
   $ git config --global user.name "Your Name"   //你的名字
   $ git config --global user.email "email@example.com"    邮箱地址
   ```

    **注意:**`git config`命令的`--global` 参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名

## 创建版本库

### 创建本地版本库

#### windows

- 1.在想要创建仓库的地方创建文件夹,**如果使用Windows系统，为了避免遇到各种莫名其妙的问题，请确保目录名（包括父目录）不包含中文**
- 2.进入文件夹后打开命令行,输入 `git init`,即可初始化git版本库,`.git`文件夹默认是隐藏的
- Git命令必须在Git仓库目录内执行（git init除外），在仓库目录外执行是没有意义的

## 提交文件

在仓库目录或仓库子目录下创建任意文件 编辑完成后

git add :用于将文件提交到暂存区 `git add 路径名/文件名`  

git commit:将暂存区文件提交到本地仓库,`git commit -m "说明"` ,m后为说明
