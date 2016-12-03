#### 原创

##一些常用快捷键c(ctrl)
	1. c + l 清屏
	2. c + c 终止程序
	3. 
##历史命令切换: histroly
	1. 向上切换 c + p
	2. 向下 c + n
##  光标移动:
	1. 向左:c + b
	2. 右 c + f
	3. 行首 c + a
	4. 行尾 + e
## 根目录
	1. bin 存放我们常用的命令
	2. boot 开启启动linux的一些核心文件.包括连接文件和一些镜像文件
	3. dev  linux的外部设备文件(linux的一些皆文件)
	4. etc 系统管理所需要的配置文件和子目录(服务器配置)
	5. home 存放所有普通用户的目录
	6. lib 存放linux的动态库 也叫共享库  几乎所有的app都要用到这些文件
	7. lost+found 非法关机后,这里存放了一些文件
	8. media(自动) linux自动识别的设备,u盘光驱,识别后设备挂载到该目录下
	9. mnt(手动) 让用户临时挂载别的文件系统 
	10. opt 第三方软件
	11. proc 虚拟目录
	12. root 系统管理员,
	13. sbin 存放系统管理员使用的命令 ,即启动的应用程序
	14. usr 用户的很多app和文件都放在该目录下
	15. usr/bin app
## 目录切换
	pwd 打印当前目录
	cd - 切换左右目录
	cd ./ 当前目录
	cd ../ 到上一级目录
	cd ~ 进入 当前用户的家目录
	
## 用户管理操作
	1. sudo命令
		1. sudo su 切换到超级用户
		2. sudo su zzw 切换zzw用户
		3. sudo 其他用户暂时借用管理员权限(第一次需要输入当前用户的密码)
	2. 添加用户
		1. sudo adduser name(必须是小写的) 添加用户
		2. sudo useradd -s /bin/bash -g Robin -d /home/Robin -m Robin
	3. 给用户修改密码(新用户添加密码)
		1. sudo passwd Robin
		2. sudo passwd root 给超级管理员修改密码
	4. 删除用户:
		1. sudo deluser Robin (但是还需要手动删除/home/Robin)
		2. sudo userdel -r Robin (自动删除home目录下文件)
	5. 添加一个用户组
		1. sudo addgroup Robin (小写)
		2. sudo groupadd Robin
	6. 切换用户 
		1.  su命令 su+ name 切换用户 默认切换root
	7. 查看当前系统下存放的用户(etc/passwd文件每一行对应一个用户)
		1. etc/passwd 文件中查看是否存在创建的用户
## 下载软件
	1. sudo apt-get install tree 下载
	2. sudo aptitude show tree 显示是否下载了

## 文件颜色
	1. 白色 普通文件  
	2. 蓝色 目录    
	3. 绿色 可执行文件  
	4. 红色 压缩文件   
	5. 青色 链接文件 (快捷方式)
	6. 灰色 其他文件
	7. 黄色 设备文件
	8. 文件类型:
		1. -普通文件 d目录 I链接文件 b块设备 c字符设备 s:Socket文件 p管道
	
## 目录和文件相关
	1. ls -a 所有文件  .XX 指的是隐藏文件   -r:同时列出所有子目录层(tree)
	2. ls -l 列出文件的详细信息
		前边有10个字符
		第一个指的是文件的类型 
		后三个 对应的所有者的权限
		在三个 同组用户对应的权限
		在三个 其他用户的权限
		在一个 文件的硬链接数
		在一个 该文件的所有者
		在一个 该文件所属于的组
		在一个 占用的存储空间
		在一个 文件的最后修改是日期
		在一个 文件名
	3. mkdir 创建目录
	4. mkdir -p 创建复合目录
	5. rmdir 删除空目录
	6. rm -r 递归删除 -ri 删除时提示
	7. touch 文件不存在创建一个空文件 文件存在文件的修改时间会改变
	8.  查看文件内容的五种方式
		1. cat 只能显示部分 并且移动到尾部
		2. more  空格翻页 回车过行 无法返回
		3. less 能返回的more c+p 往前  c+n 往后一行  c+b往前翻页 c+f往后翻页
		4. head -10 显示前10行
		5. end  -10 显示后10行
	9. cp 复制文件或目录 -r 也需要递归的拷贝  cp xx xx -r
	10. mv 移动文件也可以重命名 mv XX xx 
	11. ln 
		1. -s 创建软连接 也是快捷方式 ln -s 绝对路径 链接名 
		2. ln xx xx 创建硬链接(Linux文件系统的存储单位是块,
		3. 每个文件有个inode节点保存文件信息,硬链接通过查找inode来得到文件的信息)
	12. 偏一点的操作 
		1. wc 文件名 查看文件的行数 和 字节数
		2. od -t(指定数据的显示格式)c 查看二进制文件
		3. 执行二进制文件 ./文件名
		4. du -h 查看当前目录的大小
		5. df -h 提示磁盘的使用情况
	13. which(外部命令) 命令解析器 查看命令所在的目录

#which 命令
	1. which ls  可以显示是在哪个目录找到了这个命令(命令可以理解为一个应用)
	2. which cd 没有显示  cd命令是linux的内嵌命令 不是外部的
# 修改文件的权限以及文件所属的组
	1. whoami 查看当前用户
	2. 修改文件权限
		1. 文字设定法 : chmod [who] [+|-|=] {mode}
			1. who :  文件所有者:u 同组:g 其他:o 所有:a
			2. +增加权限 - 减少 =直接等于设定的
			3. mode: r读 w写 x执行
		2. 数字设定法 : chomd 777 temp  给temp文件 777的满权限
			1. -:没有权限
			2. r:4  w:2  x:1   (相加来作为who的权限) w+x:3  rwx:7 rx:5
			3. 765: 7:文件所有者 6:同组  5:其他
			
	3. 修改文件的组
		1. chown john temp  把temp的所有权给john
		2. chgrp zzw temp 改变文件所属的组
		
	4. 目录必须要有执行(x) 的权限,否则无法查看目录的信息
#查找和检索文件
	1. 按文件属性进行查找:
		1. 文件名: find 查找的目录 -name +"文件的名字"(要用引号括起来)
		   通配符    *:一个或多个字符
					?:一个字符
					
		2. 文件大小: find 查找目录 -size +  +10k(大于10k) -10M(小于10M)
								 -size +10k -size -50k(大于10k小于50k)
		3. 文件类型: find 查找目录 -type 
	2. 按文件内容进行查找
		1. grep -r "查找的内容" 查找的路径 
##软件的安装和卸载
	1. 在线安装
		1.  sudo apt-get install tree(在线安装)
		2.  sudo apt-get remove tree(删除)
		3.  sudo apt-get update(更新软件列表(软件的名字和下载地址))
		4.  sudo apt-get clean (清理所有软件的安装包)
	2. deb包安装
		1.	sudo dpkg -i xxx.deb(安装)
		2.	sudo dpkg -r xxx(卸载)
	3. 源码安装
		1. 解压源代码包
		2. 进入安装目录 cd dir
		3. 检测文件是否缺失,创建makefile ,检测编译环境: ./configure(可执行文件,要有执行权限) 执行它
		4. 编译源码,生成库和可执行程序: make 命令
		5. 把库和可执行程序 ,安装到系统目录下: sudo make install
		6. 删除和卸载软件: sudo make distclean
		7. 应该先看readMe文件(有过程)
##基本概念
	1. shell 和 bash 都是命令解析器(unix 和 linux)同一个人写的

##压缩包管理
	1. 屌丝版:
		1. gzip --.gz格式的压缩包
			1. gzip *.txt   把当前目录所有的txt打包,并且不保存原文件.(但是不能压缩目录)
			2. gunzip *.gz 把当前目录的所有gz解压.
		2. bzip2 --.bz2格式
			1.	bzip2 *.txt 和gzip一样
			2.	bunzip2 .bz2 和 gzip一样
		3. 差异: bzip2 -k *.txt 可以保存原文件
	2. 高富帅版:
		1. .tar
			1. 参数:
				1. c--创建 -- 压缩
				2. x--释放 --解压缩
				3. v--显示提示信息 --压缩解压缩 --可以省略
				4. f -- 指定压缩文件的名字
				5. z-- 使用gzip的方式进行压缩文件 --gz
				6. j-- 使用bizp2的方式压缩文件 -- .bz2
			2. 压缩:
				1. tar zcvf 生成的压缩包的名字(xxx.tar.gz) 要压缩的文件或目录
				2. tar jcvf 生成的压缩包的名字(xxx.tar.bz2) 要压缩的文件或目录
			3. 解压
				1. tar zxvf 要解压的压缩包的名字(并且会将其解压到当前目录)
				2. tar jxvf 要解压的压缩包的名字(一样)
				3. tar zxvf 压缩包 -C 解压到的目录
		2. .rar(用户必须手动安装该软件)
			1. 参数:
				1. 压缩:   a
				2. 解压缩: x
			2. 压缩:
				1. rar a 生成的压缩文件的名字 压缩的文件或目录
			3. 解压缩:
				1. rar x 压缩的文件名 [可添加目录,不添加默认当前目录]
				2. rar 
		3. .zip;
			1. 参数
				1. 压缩目录一定要加-r
			2. 压缩
				1. zip 压缩包的名字 要压缩的文件
				2. zip -r 压缩包的名字 要压缩的目录 (递归压缩目录)
			3. 解压缩
				1. unzip 压缩包的名字 
				2. unzip 压缩包的名字 -d 指定的目录
##进程管理
	1. ps
		1. ps -a 查看当前的所有用户信息
		2. ps -au 查看的更详细
		3. ps -aux 查看不依赖于终端的进程(进程特别多)
	2. kill -SIGKILL + pid  杀死该进程  (也可以用kill -9 + pid)kill -l 查看信号序列
	3. 查看当前进程的环境变量(env):
		1. Linux下的环境格式: key-value(可以有多个value-->key-value:value:value)
	4.top命令 (和windows的任务管理器类似但是只能看不能进行操作)

##管道(|)
	1. 什么是管道
		1. 管道就是  指令1 | 指令2  指令1的输出作为指令2的输入,指令2处理完毕将信息输出到屏幕
		2. ps -aux|grep bash 查找前面输出的内容里边有没有bash
		
		4. 
##网路管理
	1. ifconfig 查看本机的ip地址
	2. ping 测试两台主机之间能否进行通信
		1. ping + ip 地址 进行信息回馈
		2. ping + ip + -c 4  进行 4次回馈
		3. ping www.baidu.con 可以测试能否上网
		4. ping 域名 都会有回馈
	3. mslookup 可以得到域名对应的ip  nslookup www.baidu.com
##ftp服务器搭建 --vsftpd(ftp服务器)-->自带服务端和客户端
		ftp服务器作用:文件的上传和下载
	1.  服务器端
		1.  修改配置文件
			1.  /etc/vsftpd.config
		2.  重启服务
			1.  sudo service vsftpd restart
	2.  客户端
		1.  实名用户登录
			1.  ftp + ip地址 进入
			2.  文件的上传 put file(登录ftp服务器时在那个目录登的,就选择其中的文件)
			3.  文件的下载 get file
		2.  匿名用户登录
			1.  ftp + serverIp  账号输入:anonymous 密码直接回车
			2.  不允许匿名用户在任意目录切换,只能在一个指定的范围内工作(需要在server端创
			建一个匿名用户登录的目录)创建目录后修改配置文件的anno_root=目录路径 然后重启
             服务
		3. 退出:  bye quit exit
		4.  lftp客户端访问ftp服务器 (这是一种客户端需要额外安装)
			1.  lftp + serverip  然后 login 进入
			2.  lpwd 可以查看登录之前所在的目录
			3.  lcd 可以切换 本地目录
			4.  上传文件 put file  
			5.  上传多个文件 mput *.txt 
			6.  上传目录 mirror 目录名
##nfs服务器搭建( nfs-kernel-server)
	1. 服务端
		1. 简介 : 网络文件系统,允许网络中的计算机之间通过TCP/IP网络共享资源.
		2. 创建一个共享目录
			1. mkdir 目录
		3. 修改配置文件 
			1. /etc/exports
		4. 重启服务
			1. sudo service nfs-kernel-server restart
	2. 客户端:
		1.  连接服务器共享目录
##ssh服务器
##scp命令
##关机重启