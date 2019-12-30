# git和github的相关操作

## 安装配置
1. git config配置文件  
Linux: /etc/gitconfig（系统级）; ~/.gitconfig（用户级）; .git/config（项目级）  
Windows：\$HOME变量指定目录：C:\Documents and Settings\\$USER\\.gitconfig  

2. 查看配置信息：  
\$ git config --list  
\$ git config user.name  

3. 配置用户信息：  
\$ git config --global user.name "seele"  
\$ git config --global user.email 1421720829@qq.com  
\$ git config --global core.editor vscode  

4. 查看工作区到缓存区的状态  
\$ git status -s  
??（未添加）、A（已添加）、AM（改动未添加）  

## 基本概念
- **工作区** ：就是你在电脑里能看到的目录。
- **暂存区** ：暂存区有时也叫作索引（index），存放在（.git/index）
- **版本库** ：工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。

&emsp;&emsp;当对工作区修改（或新增）的文件执行 "git add" 命令时，暂存区的目录树被更新，同时工作区修改（或新增）的文件内容被写入到对象库中的一个新的对象中，而该对象的ID被记录在暂存区的文件索引中。  
&emsp;&emsp;当执行提交操作（git commit）时，暂存区的目录树写到版本库（对象库）中，master 分支会做相应的更新。即 master 指向的目录树就是提交时暂存区的目录树。  
&emsp;&emsp;当执行 "git reset HEAD" 命令时，暂存区的目录树会被重写，被 master 分支指向的目录树所替换，但是工作区不受影响。  
&emsp;&emsp;当执行 "git rm --cached <file>" 命令时，会直接从暂存区删除文件，工作区则不做出改变。  
&emsp;&emsp;当执行 "git checkout ." 或者 "git checkout -- <file>" 命令时，会用暂存区全部或指定的文件替换工作区的文件。这个操作很危险，会清除工作区中未添加到暂存区的改动。  
&emsp;&emsp;当执行 "git checkout HEAD ." 或者 "git checkout HEAD <file>" 命令时，会用 HEAD 指向的 master 分支中的全部或者部分文件替换暂存区和以及工作区中的文件。这个命令也是极具危险性的，因为不但会清除工作区中未提交的改动，也会清除暂存区中未提交的改动。  

## 基本操作

1. 创建仓库  
在项目根目录下使用git bash创建，生成.git文件夹：  
\$ git init

2. 克隆项目：  
git clone 时，可以所用不同的协议，包括 ssh, git, https 等，其中最常用的是 ssh，因为速度较快，还可以配置公钥免输入密码。各种写法如下：  
\$ git clone git@github.com:fsliurujie/test.git         --SSH协议  
\$ git clone git://github.com/fsliurujie/test.git          --GIT协议  
\$ git clone https://github.com/fsliurujie/test.git      --HTTPS协议  

3. 向缓存区添加文件：  
\$ git add *.c  
\$ git add README.md  
\$ git status -s  

4. 将缓存区内容提交到仓库中：  
\$ git commit -m README.md  
\$ git commit -a  


5. git commit、git push、git pull、 git fetch、git merge 的含义与区别  
&emsp;git commit：是将本地修改过的文件提交到本地库中；  
&emsp;git push：是将本地库中的最新信息发送给远程库；  
&emsp;git pull：是从远程获取最新版本到本地，并自动merge；  
&emsp;git fetch：是从远程获取最新版本到本地，不会自动merge；  
&emsp;git merge：是用于从指定的commit(s)合并到当前分支，用来合并两个分支；  

6. 查看提交历史  
\$ git log [--oneline, --author, --reverse]  


## 与github链接
1. 使用ssh创建和github链接的ssh-key  
\$ ssh-keygen -t rsa -C "starshadowmj@gmail.com"  
&emsp; 会生成公开/私有RSA key pair。  
其中包括：id {\$HOME/.ssh/id_rsa}；public key {\$HOME/.ssh/id_rsa.pub}；fingerprint

2. 将public key复制拷贝到github  
打开：https://github.com/settings/keys；
选择new SSH key，添加标题和public key

3. 查看是否链接成功
\$ ssh -T git@github.com
Hi wieSeele! You've successfully authenticated, but GitHub does not provide shell access.

## 向github推送
执行 git push origin master 时，它的意思是推送本地的 master 分支到远程 origin，涉及到远程以及分支，当然也得分开写了。  
\$ git add readme.txt  
\$ git commit -m "添加到远程"  
\$ git push orgin master  