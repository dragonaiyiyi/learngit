###冯根龙-本周报告-2016.1.15###
---
####一.git创建版本库

    git status           查看当前状态
    git add -i           列出根据需要的条件查询变化的文件
    git add  文件名      将文件加入版本库，其实是暂缓区以后再说该内容。
    git commit -m "xxx"  提交，需要输入log记录

####二.时光穿梭机
    1.版本退回
    git log                               查看变化日志
    git reflow                            查看版本退回后等的，日志
    git reset —hard  版本id (或者HEAD^)    执行退回某个版本，HEAD为上一个版本
                                          —hard 把本地文件也一同退回上一个版本
    小技巧：
    vim .gitingore                        修改无视的文件内容
  
    2.工作区和暂缓区(stage区域) -> 概念性内容
      1)工作区修改和新建文件，这时没有任何变化。
      2)当执行一步或多步git add 之后，被执行的文件就被放入暂缓区stage。
	  3)再在执行git commit之后stage暂缓区里面的修改就被更新到master分支中，完成更新。

	3.管理修改  ->  git原理
    git跟踪并管理的是修改，而不是文件。其意义在于，git commit只针对于git add后的东西，没有git add的文件git commit并不理会。

	4.撤销修改
      情景1:当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- 文件名称
      情景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，
            第一步：用命令git reset HEAD  文件名称  ,就回到了场景1
            第二步：执行情景1.
      情景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

    5.删除文件
      确定删除：git rm 文件名称  再执行  git commit -m “xxx"
      由于误删除想恢复：git checkout  -- 文件名称

####三.远程仓库
    首先先拥有远程仓库，此处以github的远程仓库为例。
     1.先去github网站注册一个账户。
     2.查看本机的ssh是否已有id_rsa和id_rsa.pub。
        没有则需要创建：ssh-keygen -t rss -C “xxx.@xxx.com"
     3.复制id_rsa.pub中的内容(公钥)，在Github中的Account settings的SSH Keys进行添加。
       到此为止可以进行本机到个人的GitHub的ssh链接。

    1.添加远程库
      首先在GitHub上新建一个库。
       1)在GitHub上找到Create a new repo。
       2)Repository name(仓库名字)可以随意填写，但要记住。
       3)执行 git remote add xxx(远程库的名字) git@github.com:xxx(git的个人名字)/xxx(仓库名字).git
       4)执行 git push -u xxx(远程库名字) master 。
       5)完成。以后只要执行 git push xxx master 即可。

    注意：第一次使用的时候可能会出现一下内容，表示第一次链接服务器本机担心是否可行。
	   The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established.
       RSA key fingerprint is xx.xx.xx.xx.xx.
       Are you sure you want to continue connecting (yes/no)?


