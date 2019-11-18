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
   
   
   
	
   