Git is a distributed version control system.
Git is free software distributed under the GPL.


1、安装git
2、创建版本库
	$ mkdir learngit (learngit为仓库名/目录名)
	$ cd learngit
	$ pwd
	/Users/Administrator/learngit
	
3、初始化把目录变成Git可以管理的仓库
	$ git init
	
   仓库建好了，目录下会自动生成.git文件夹
   
4、把一个文件放到git仓库，需要两步：

5、 把要管理的文件添加到仓库
	$ git add readme.txt
   

6、 把文件提交到仓库（后面引号内内容为提交说明）
	$ git commit -m "write anything"
   
   
7、查看状态
	$ git status
	
8、查看修改内容
	$ git diff
   按Q可以退出diff
   
9、提交修改(和前面提交文件两步相同)
    $ git add .  （. 代表add所有文件，也可以添加具体文件 git add readme.txt）
	$ git commit -m "write anything"
   
10、版本回退
	$ git log 显示提交日志
	$ git reset --hard HEAD^ 回退到上一个版本
	$ git reset --hard HEAD^^ 回退到上上个版本
	$ git reset --hard HEAD~5 回退到上5个版本
	$ git reset --hard 1094a  回退到指定版本（1094a 为版本ID/commit id前5位）
	$ cat readme.txt  查看文件内容
	
	$ git reflog 记录你的每一次命令（每条记录前几位就是commit id）
	
11 工作区（working directory）
	任意文件夹都可以是工作区
12、版本库
	工作区有一个目录.git，就是Git的版本库
	
	git add 添加文件到暂存区(stage)
	git commit 提交更改(把暂存区stage的内容提交到当前分支)
	Git会为我们自动创建第一个分支master
	
13、git checkout -- readme.txt (撤销文件在工作区的修改)
	让这个文件回到最近一次git commit或git add 时的状态
	
14、git reset HEAD readme.txt 可以把暂存区的修改撤销掉，重新放回工作区
    这个命令之后可以执行13，此时工作区的修改也被撤销了
	
15、如果是提交了的文件想撤回，则用前面说的版本回退处理

16、删除文件
	rm test.txt
	此时用git status 查看状态，系统会告诉你哪些文件被删除了
	
	（1）继续执行
	git rm test.txt
	git commit -m "remove test.txt"
	文件成功被删除
	
	（2）如果不想删了，则执行
	git checkout --test.txt (实质是用版本库里的版本替换工作区的版本)

17、远程仓库
	可以找一台电脑充当服务器角色，把它作为远程仓库
	也可以注册一个GitHub账号，免费获得Git远程仓库
	
18、创建 SSH Key
	 ssh-keygen -t rsa -C "xiexianqi2017@gmail.com"
	 
19、登陆github,找到Account settings--SSH Keys--add SSH Key
	key 文本框里粘贴id_rsa.pub文件的内容（添加公钥，公钥所有人才有权利提交代码到github）
	
20、在本地关联一个远程库
	git remote add origin git@github.com:xiexianqi163/learngit.git
	origin为远程库名称(一般默认这个名字，也可以自己改一名)
	origin后面为ssh地址或https地址
	
21、关联后，第一次推送master分支的所有内容
	git push -u origin master
	
22、以后推送可以不加 -u
	git push origin master
	
23、创建远程库并克隆到本地库
	git clone git@github.com:xiexianqi163/gitskills.git

24、分支
	假设你准备开发一个新功能，需要两周才能完成，第一周你写了50%代码，如果立刻提交，由于代码还没写完，
不完整的代码库会导致别人不能干活了，如果等代码全部写完再一次提交，又存在丢失每天进度的风险。有了分支
就不用怕了，你创建了一个属于自己的分支，别人看不到，还继续在原来分支上正常工作，而你在自己的分支上干
活，想提交就提交，直到开发完毕后，再一次性合并到原来的分支上

25、创建分支
	git checkout -b dev    创建并切换
	dev是分支名    -b表示创建并切换，相当于以下两条命令：
	git branch dev         创建分支
	git checkout dev	   切换分支
	
26、查看当前分支
	git branch
	
27、在新建的分支上工作，将成果add并commit之后，切换回master分支就可以完成合并动作了

28、合并分支
	git checkout master  切换回主分支
	git merge dev        将dev分支工作成果合并到master(当前)分支
	git branch -d dev    删除dev分支
	
29、创建分支的另一种命令
	git switch -c dev   创建并切换分支
	git switch master   直接切换分支
	
30、当git无法自动合并分支时，就必须首先解决冲突
	git merge dev
	当存在冲突，文件中会出现
	<<<<<<< HEAD
	Creating a new branch is quick & simple.
	=======
	Creating a new branch is quick AND simple.
	>>>>>>> dev
	git自动把两个分支的不同点列出
	此时需要我们手动修改成我们想要的内容后再提交
	
	
	rna721
	
31、禁用fast forward模式合并
	git merge --no--ff -m "merge with no-ff" dev
	因为本次合并要创建一个新的commit，所以加上-m参数
	
32、分支管理原则
	master分支应该是非常稳定的，仅用来发布新版本，平时不能在上面干活;
	干活在dev分支上；
	修复一个代号101的bug,可创建一个分支issue-101来修复它
	
33、git stash 
	把当前工作现场“储藏”起来，等以后恢复现场后继续工作
	git stash list   
	查看工作现场
	
34、git stash apply   恢复储藏的工作现场
	git stash drop    删除stash
	git stash pop     恢复储藏的工作现场并删除stash
	
35、在master分支上修复的bug，想要合并到当前dev分支，可以用
	git cherry-pick 4c805e2 (issue-101分支提交时的commit id)
	
36、feature分支
	每添加一个新功能，最好新建一个feature分支，在上面开发，完成后，合并，最后删除该feature分支
	git checkout -b feature-vulcan     创建并切换
	
	git branch -d feature-vulcan     删除分支
	git branch -D feature-vulcan	   强制删除（未合并的分支删除时会提示未合并，可以使用强制删除）
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
   