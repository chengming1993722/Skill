# gitlab使用
____________
## 1gitlab创建工程
点击页面右上角的“username”弹出下拉框可以选择Project创建新的工程
###1.1Visibility Level
权限分为三个等级：
* Private 私有的，只有你自己或者组内的成员能访问
* Internal 所有登录的用户
* Public 公开的，所有人都可以访问
### 1.2naemspace
这个选择是用来决定这个工程所属的，可以选User为你自己。或者选择组，这个会影响到后面工程的url。

## 2Git的使用
____________    
git仓库之间的代码传输协议主要使用ssh协议。而一般搭建gitlab的时候使用的git用户是没有密码的，因此直接ssh是不能登录的，就需要使用ssh-keygen上传公钥，使用非对称加密传输。
### 2.1 生成sshkey
在终端中敲下面的命令：
ssh-keygen -t rsa -C "$your_email"  ''' 生成一对私钥和公钥 '''
cat ~/.ssh/id_rsa.pub  '''查看公钥字符串'''
### 2.2保存sshkey到gitlab 
在面板上依次点击Profile Settings –> SSH Keys –> Add SSH Keys。然后把上一步中的id_rsa.pub中的内容拷贝出来粘贴到输入框中，保存。
### 2.3初始上传代码
  *  进入工程目录： cd $project_root
  *  初始化git仓库：git init
  *  添加文件到仓库：git add .
  *  提交代码到仓库：git commit -m 'init commit'
  *  链接到git server：git remote add origin git@example.com:namespace/projectname.git
  *  push代码到服务器：git push origin master
### 2.4克隆代码到本地
克隆会把整个远程仓库复制到本地仓库，终端命令如下：
git clone git@example.com:namespace/projectname.git 

# git常用命令

### 目录变成git仓库
 git init 

### 把工作区的修改提交到Git仓库的暂存区
 git add filename 

### 把暂存区的所有内容提交到当前分支
 git commit -m "add file"   <!--  提交内容解释说明 --> 

### 把本地仓库添加远程库 
 git remote add origin git@github.com:jarevrygo/learngit.git 

### 把本地库master的所有内容推送到远程库
 git push -u origin master (-u参数在第一次推送相应分支的时候用) 

### 从远程库克隆出一个本地库
 git clone git@github.com:jarevrygo/learngit.git 

### 查看版本历史记录
  git log(详细提交日志)
  git log --pretty=oneline(简略)
  git reflog 

### 回退到上一个版本
 git reset --hard HEAD^(上一个版本就是HEAD^,上上一个版本就是HEAD^^,往上n个版本   可以写成HEAD~n.)git reset --hard commit_id   <!--  可以使用git log 查看commit_id -->
 git reflog <!--  ///可以查看出所有历史信息 -->

### 查看当前分支修改状态
 git status

### 查看工作区和版本库里面最新版本的区别
 git diff HEAD -- readme.txt 

### 丢弃工作区的修改
 git checkout -- readme.txt 
 <!-- git checkout其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原” -->

### 把暂存区的修改撤销掉（unstage），重新放回工作区
 git reset HEAD filename (git reset命令既可以回退版本，也可以把暂存区的修改回退到工作区)然后 git checkout -- readme.txt 

### 从版本库中删除该文件
  git rm test.txt
  git commit -m "remove test.txt"
  git push 

## 分支管理<p>
### 创建dev分支，然后切换到dev分支
  git checkout -b dev
  git branch dev
  git checkout dev 

### 查看当前分支
 git branch 

### 合并到master分支
 git merge dev 

### 删除分支
 git branch -d dev

### 查看分支合并图或看看分支历史
 git log --graph --pretty=oneline --abbrev-commit  ''' 合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并
git merge --no-ff -m "merge with no-ff" dev
git log --graph --pretty=oneline --abbrev-commit  '''

### 创建远程origin的dev分支到本地
 git checkout -b dev origin/dev 

### 指定本地dev分支与远程origin/dev分支的链接
 git branch --set-upstream dev origin/dev 

### git 删除远程分支
 git branch -r -d origin/branch-name
 git push origin :branch-name 
### git拉取远程分支到本地
 git fetch，可以将远程分支信息获取到本地
  git checkout -b local-branchname origin/remote_branchname  就可以将远程分支映射到本地命名为local-branchname  的一分支 
### 创建标签
 git tag v1.0 
'''命令git tag <name>用于新建一个标签，默认为HEAD，也可以指定一个commit id；
git tag -a <tagname> -m "blablabla..."可以指定标签信息；
git tag -s <tagname> -m "blablabla..."可以用PGP签名标签；
命令git tag可以查看所有标签。'''

/** [git简用](https://www.liaoxuefeng.com/) */
/** [git官网](https://git-scm.com/) */
