title: linux 学习笔记

date: 2014-05-09 21:19:42

---



> TODO - 待整理


# 一些概念

- bytes stream 字节流

	linux 执行一个程序时会自动打开三个流：标准输入流、标准输出流、标准错误流
	
	输出流用 ">" 或 ">>" 表示
	
	输入流用 "<" 表示
	
	错误流用 ">&" 表示
	
		// 输出文本流到屏幕
		$ echo '我是小赖'
		// echo 输出信息到 a.txt
		$ echo '我是小赖' > a.txt
		// 追加文本流到 a.txt
		$ echo '我才是小赖' >> a.txt

		// 输出命令执行结果文本流到屏幕
		$ ls
		// 重新定向, 这样 ls 命令的输出文本流就会写到这个文件上
		$ ls > a.txt
		// 若 a.txt 已存在，则将ls 命令的输出文本流追加到这个文件上
		$ ls >> a.txt 
		
		// 输入文本流
		$ cat < a.txt
		// 复制 a.txt 到 b.txt
		$ cat < a.txt > b.txt
		
		// 输出错误，假定 wrongDir 是不存在的目录
		$ cd void >& a.txt
		
- pipe 管道

	使用管道，可以将一个命令的输出流当做另一个命令的输入流
	
	管道用 "|" 表示
	
		// 输出 "cat > a.txt" 当做命令 "wc" 的输入
		// wc 即 word count：输出文本的行、词和字符总数
		$ cat < a.txt | wc

<!-- more -->			
	
# 帮助类命令

- type 查看某个命令的类型

类型可为：1.可执行文件 2.内建函数 3.别名

		$ type ls
		$ type cd
		$ type open

- which 查看命令的绝对路径

		$ which ls
		
- where 更大范围查看命令的绝对路径		

		$ whereis ls

- whatis 查看命令的介绍

		$ whatis ls	

- man 查询命令的帮助文档
		
		// 学习 linux 必备！
		$ man ls	

- info 查询命令的更详细帮助文档

		$ info ls

- history 查看输入的命令历史

		$ history 
		
- alias 别名

		// 查看所有别名
		$ alias
		// 设置别名，llss 为 ls 的别名
		$ alias lllsss = ls	

- env 环境变量

		// 查看所有环境变量
		$ env
		// 设置环境变量
		// $ export [key]=[value]	
		$ export testKey=testVal
		
- finger 查看用户信息
		
		// 查看所有用户信息
		$ finger
		// 查看特定用户信息
		$ finger xiaolai
		
- who am I 显示当前用户

		$ who am I
		
- su 成为超级用户

		$ su
		// 或者用超级用户执行命令：
		// $ sudo [commmand]	

- passwd 修改密码
		
		$ passwd	
	
		
	
					
	
# 文件管理类命令
	
- touch 新建文件

		// 如果文件已经存在，则只修改时间信息
		$ touch a.txt	

	
- ls 列出目录/文件信息 
		
		// 显示当前目录下的文件
		$ ls
		// 显示桌面目录下的文件
		$ ls ~/Desktop
		// 显示目录下所有文件的信息
		$ ls -l
		// 显示目录下特定文件的信息
		$ ls -l a.txt
		// 显示目录下多个文件的信息
		$ ls -l a.txt b.txt c.txt d.txt
		// 列出当前目录下的文件的详细信息，包括隐藏文件
		$ ls -l -a
		// 或
		$ ls -la
		// 列出当前目录下特定文件的详细信息，包括隐藏文件
		$ ls -l -a a.txt
		// 或
		$ ls -la a.txt

- cp 复制
 
		// 将 a.txt 复制到 b.txt
		$ cp a.txt b.txt
		// 将 a.txt 复制到父目录下的 a.txt
		$ cp a.txt ..

- mv 移动				

		// 移动 a.txt 到 b.txt ，此时相当于重命名了
		$ mv a.txt b.txt
		// 移动 a.txt 到桌面目录下
		$ mv a.txt /Desktop

- rm 删除文件

		// 删除 a.txt 文件
		$ rm a.txt
		
- rm -r 删除目录-目录不一定非空

		// 删除 /home/xiaolai 整个目录，参数 -r 是 recursive 重复删除之意
		$ rm -r /home/xiaolai	
		
		// 慎用 rm -rf 即强制删除目录不提供确认！！
		// $rm -rf /home/xiaolai
	
- pwd 显示当前路径
		
		$ pwd
				
- cd 切换路径
		
		// 切换到 /home/xiaolai
		$ cd /home/xiaolai
		// 切换到之前的路径
		$ cd -	
	
		
- mkdir 创建目录

		// 创建目录 /home/xiaolai/newdir
		$ mkdir /home/xiaolai/newdir

- rmdir 删除目录

		// 目录为空时才可删除
		$ rmdir /home/xiaolai/newdir	

- chmod 修改权限

		// 修改 a.txt 的权限为 755
		$ chmod 755 a.txt

- chown 修改拥有者

		// 修改 a.txt 的拥有者为 root, sudo 指以超级权限运行
		$ sudo chown root a.txt 	

- chgrp 修改拥有组

		// 修改 a.txt 的拥有组为 root 组
		$ sudo chgrp root a.txt	
		
- cat 查看文件内容
		
		// 命令行中列出文件内容
		$ cat a.txt	
		// 链接显示 a.txt 和 b.txt
		$ cat a.txt b.txt

- head -1 显示文件第一行

		$ head -1 a.txt

- tail -2 显示文件倒数第二行

		$ tail -2 a.txt
		
- diff 文件对比
		
		// 显示 a.txt 和 b.txt 的差异
		$ diff a.txt b.txt
		
- du 文件占用的磁盘空间
		
		// du	

- df 文件系统的磁盘空间占用情况

		// df							

- wc 显示文件内容的字符、词和行数 			

		$ wc a.txt	

		
- od -c 使用ASCII查看文件内容

		$ od -c a.txt	
	
	
- open 打开文件

		// 打开一个应用
		$ open /Applications/Safari.app/
		
		// 打开一个目录
		$ open /Applications/
		// 打开当前目录
		$ open ./
		
		// 使用默认软件打开文件
		$ open fa.css 
		// 使用文本编辑器打开文件
		$ open fa.css 
		// 指定一个软件打开一个文件，如这里指定用 sublime text 打开
		$ open test.txt -a /Applications/Sublime\ Text.app/	
- du 查看文件夹大小

		$ du /home/xiaolai
		// -h 人类可读单位，-s 只显示摘要	
		$ du -sh /home/xiaolai

- find 查找文件
		
		// 查找test.txt
		$ find  test.txt

- locate 查找匹配名文件

		// 向下查找文件名中含有 test 的文件
		$ locate test
		
		// 与 find 不同的是，locate 并不是实时查找，需要更新数据库才能获取到最新信息
		$ updatedb
		$ locate test

- 其他命令
	
		// 时间
		$ date	
		// 休眠 300s
		$ sleep 300
		// 系统日志
		$ dmesg
	
	硬件信息
		
		// 系统信息
		$ uname
		// 系统详细信息
		$ uname -a
		// 所有硬盘的使用情况
		$ df -lh
		// 所有硬盘使用情况
		$ mount
		// 所有分区
		$ sudo fdisk -l
		// 架构信息
		$ arh
		// CPU信息
		$ cat /proc/cpuinfo
		// 内存信息
		$ cat /proc/meminfo
		// 内存使用情况
		$ free
		// 内存page大小(KB)
		$ pagesize
		
	网络信息
		
		// 网络接口信息
		$ ifconfig
		// 路由表
		$ route
		// 网络连接状态
		$ netstat
		// 发送 ping 包
		$ ping [IP]
		// 探测路由路径
		$ traceroute [IP]
		// 向DHCP发送请求，获取IP地址和其他设置信息
		$ dhclient
		// DNS查询domain对应的IP
		$ host [domain]
		// DNS查询IP对应的domain
		$ host [IP]
		// 使用 wget 下载 url 指定的资源
		$ wget [url]
		

# 进程

- top 显示进程信息
		
		$ top

- ps 列出进程

- ps -e -o 列出进程特定信息

		// -e 列出全部进程
		$ ps -e
		// -o pid,comm,cmd 列出 PID,COMMAND,CMD,PPID 信息
		$ ps -e -o pid,comm,cmd,ppid

- fork 创建进程

	通过复制父进程来得到子进程，子进程有个 ppid 属性保存了父进程 id
	
		// 显示父子进程
		$ ps -o pid, ppid, cmd
		// 显示进程树
		$ pstree	
		
- ps -ajx 显示较完整的进程信息

		$ ps -ajx	
	
- ps -o pgid
	
	进程组的作用在于可以将一个新号发送给这个组
	
		// pgid 表示进程组的领导进程的 id
		$ ps -p pid,,ppid,pgid,cmd

- ps -o sid

	几个进程组可以组成一个会话，会话领导进程的PID为SID
	
	会话中的每个进程组都是一个工作(job)，每个会话可以连接一个终端(control terminal)
	
	会话的作用在于可以将多个工作囊括在一个终端，并取其中的一个作为前台(foreground)，其他工作则进行在后台(background)
	
		// 用 & 将ping工作在后台运行, 并将输出流写到log文件中
		$ ping localhost > log &

# 信号

	常见信号：SIGINT, SIGQUIT, SIGCONT, SIGTSTP, SIGALRM
		
		// 查询信号
		$ man 7 signal
	
	按下键盘 CTRL+C 时，发出 SIGINT 信号，默认操作是中断(INTERRUPT)该进程	
	按下键盘 CTRL+\ 时，发出 SIGQUIT 信号，默认操作是退出(QUIT)该进程
	
	按下键盘 CTRL+Z 时，发出 SIGTSTP，默认操作是暂停(STOP)该进程
	
	SIGCONT 用于通知暂停的进程继续
	
	SIGALRM 用作定时器：一定时间后才生成该信号
	
		// 运行一个进程
		$ ping localhost
		// 按下键盘 CTRL+Z 发出 SIGTSTP 信号，暂停该进程
		// CTRL+Z,显示：
		// [1]+ Stopped		ping localhost
		// 查询这个ping进程的pid
		$ ps -e -o cmd,pid
		// 查询到 5132，使用 kill 来发送SIGCONT信号，继续该进程
		$ kill -SIGCONT 5132
		// 接着ping进程就会继续了
		
# 用户

	用户登录后，有用户id(UID)和组id(GID)
	
	用户信息保存在 /etc/passwd
	组信息保存在 /etc/group
	
		
# SSH 登录 VPS

- 登录到远程主机

		$ ssh root@123.123.123.123
	
- 修改root用户密码

		$ passwd
	
- 添加用户组

		$ addgroup admin
	
- 添加用户

		$ useradd -d /home/xiaolai -s /bin/bash -m xiaolai
	
	参数 -d 指定用户主目录，-s 指定用户的shell，-m 指定目录不存在则创建	
- 设置新用户的密码

		$ passwd xiaolai
	
- 添加用户到用户组

		$ usermod -a -G admin xiaolai
	
- 为用户设定sudo权限

		$ visudo
	
	visudo会打开/etc/sudoers 在：
	root    ALL=(ALL:ALL) ALL 后添加：
	xiaolai    ALL=(ALL:ALL) ALL	
	
	
# 压缩与归档

- zip 压缩

		// 将 file1 和 file2 压缩到 file.zip
		$ zip file.zip file1 file2

- unzip	解压缩

		$ unzip file.zip	
	
- gzip 压缩

		// file1 压缩到 file.gz
		$ gzip -c file1 > file.gz

- gunzip 解压缩

		$ gunzip file.gz

- tar -cf 创建归档
		
		// 将 file1 和 file2 归档到 file.tar
		$ tar -cf file.tar file1 file2	

- tar -zcvf 创建归档并压缩		

		$ tat -zcvf file.tar file1 file2
		
- tar -xf 释放归档
		
		$ tar -xf file.tar

- tar -zxf 解压并释放归档

		$ tar -zxf file.tar.gz	
		
			
		
		



	

	




	