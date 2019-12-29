# Linux

## 目录管理命令行
- **目录查看、切换、显示当前目录**
  	

  ```shell
  ls [-al] [文件或者目录]		
  cd [目录名称]“~”//家目录 “-”//上次的目录 “.”//本地目录 “..”//上级目录
  pwd
  ```

- **目录创建与删除**
  	

  ```shell
  mkdir [-p//递归建立所需] 目录名称
  rmdir [-p//递归删除所需] 目录名称
  ```
## 文件操作命令
- **快捷方式创建**
  ​	 

  ```shell
  ln  [-s//建立软链接（类似于快捷方式），否则硬链接（硬链接就是相当于复制，但是二者内容永远一样）] 源文件 目标文件。
  ```

- **文件创建与查看**

  ```shell
  touch #文件名 
  stat #[文件//查看文件状态]
  ```

- **文件查看**
  
  ```shell
  cat/more/less/head/tail/...
  ```

## 目录及文件管理命令
- **复制、移动、删除**

```shell
cp [-r] 源文件 目标文件
mv 源文件 目标文件
rm [-rf] 文件或目录
```
- **查找**

```shell
which 命令名 #查找命令
whereis 文件或目录 
find 目录 [-name/user/size] 参数
```

## 用户管理命令
- **用户管理**
```shell
who  # 查看用户命令
useradd [-g 群组] 用户名  #添加用户命令
passwd 用户名  # 添加用户密码
userdel [-r] 用户名  # 删除用户	
```
- **群组管理**
```shell
groups [用户名]  # 查看用户群组
groupadd 群组名  # 创建群组
groupdel 群组名  # 删除群组
usermod [-g 群组] 用户名  #用户群组修改
```

## 权限管理命令

- **权限、角色的设置**

```shell
chown [-R] 用户名 文件或目录  # 修改所有者
chown [-R] 用户名：组名 文件或目录  # 修改所有者和组
chgrp组名 文件或目录  # 修改说是组
chmod [-R] xyz 文件或目  # x：4ugoa；y：2+-=；z1rwx 修改权限
```

## 压缩命令、解压缩命令
```shell
zip [-r//压缩目录] 压缩名 源文件
unzip [-d //指定压缩位置][文件位置] 源文件

gzip [-r//压缩目录] 源文件
gunzip 要解压的文件

bzip2 [-k//保留源文件 v显示压缩信息] 源文件
bunzip2 要解压文件

tar [-cvf //打包 -xvf //解包 -tf 
//查看压缩 -zcvf //gz格式压缩 -jcvf //bz2格式压缩] [指定压缩名] 源文件
```

## 软件的安装与卸载

- 源码包安装
  > 下载源码包(curl 、wget)
  > 解压（tar）
  > 进入到该目录
  > 编译前配置
  > 编译
  > 编译安装
  > 删除make clean 然后直接删除目录
  > rpm包安装
  
- 下载rpm安装包
  > rpm -ivh软件包
  >  -i安装 -v显示详细信息 -h显示进度
  >  查询包信息 rpm -q 安装包
  >  查询包信息 rpm -qi 安装包
  >  查询安装位置 rpm -ql 安装包
  >  卸载 rpm -e 安装包
  
- yum安装管理rpm包
  > 查询可以安装的软件包yum
  > 安装 yum [-y] install 软件包
  > -y 自动回答 yes

# vim编辑器
			vi编辑器：命令模式（可以向其它模式转换）、编辑模式()、最后行模式
			vi 文件名称
	
			命令模式
	
			h  j  k  l
			左 下 上 右
	
			dd 剪切当前行
			yy 复制
			p 下一行黏贴  P 上一行黏贴ps 
	
			a在光标后插入   A在当行末插入
			i在光标前插入	I在当行首插入
			o在当前行之下插入 O在上一行插入
	
			编辑模式
	
			:
			最末行模式
			:set nu 显示行号
			:w 保存
			:wq 保存并退出

# JDK环境的部署与项目发布
```
<应用的上传>
	rz命令（没有的话使用yum -y install lrzsz）
<应用的上传>

<JDK环境的配置>
	下载文件后给予777权限
	拷贝到/opt目录下
	解压jdk
	解压后进入jdk目录
	拷贝jdk目录
	vi进入/etc/profile
	JAVA_HOME=
	CLASSPATH=.:$JAVA_HOME/lib
	PATH=$PATH:&JAVA_HOME/bin

​	export JAVA_HOME CLASSPATH PATH
​	source profile //使文件生效 
​	java -version javac//检查是否正常
<JDK环境的配置>

<tomcat的部署>
	解压就可使用，进入apache的bin目录
	./startup.sh完成启动
	ps -ef|grep tomcat 检查运行状态
	将war包放入webapps目录下，赋予权限
	访问项目路径即可
<tomcat的部署>
<firewall-cmd --state><systemctl stop firewalld.service>
```

# node安装

```shell
# wget https://nodejs.org/dist/v10.9.0/node-v10.9.0-linux-x64.tar.xz    // 下载
# tar xf  node-v10.9.0-linux-x64.tar.xz       // 解压
# cd node-v10.9.0-linux-x64/                  // 进入解压目录
# ./bin/node -v                               // 执行node命令 查看版本
# v10.9.0                                     // 结果
# ln -s /usr/software/nodejs/bin/npm   /usr/local/bin/                  // 设置命令软链接
# ln -s /usr/software/nodejs/bin/node   /usr/local/bin/
```

# 防火墙的配置

## iptables防火墙

```shell
一、iptables防火墙
1、基本操作

# 查看防火墙状态

service iptables status  

# 停止防火墙

service iptables stop  

# 启动防火墙

service iptables start  

# 重启防火墙

service iptables restart  

# 永久关闭防火墙

chkconfig iptables off  

# 永久关闭后重启

chkconfig iptables on　　

2、开启80端口

vim /etc/sysconfig/iptables
# 加入如下代码
-A INPUT -m state --state NEW -m tcp -p tcp --dport 80 -j ACCEPT
保存退出后重启防火墙

service iptables restart

```

## firewall防火墙

```shell
二、firewall防火墙
1、查看firewall服务状态

systemctl status firewalld

出现Active: active (running)切高亮显示则表示是启动状态。

出现 Active: inactive (dead)灰色表示停止，看单词也行。
2、查看firewall的状态

firewall-cmd --state
3、开启、重启、关闭、firewalld.service服务

# 开启
service firewalld start
# 重启
service firewalld restart
# 关闭
service firewalld stop
4、查看防火墙规则

firewall-cmd --list-all
5、查询、开放、关闭端口

# 查询端口是否开放
firewall-cmd --query-port=8080/tcp
# 开放80端口
firewall-cmd --permanent --add-port=80/tcp
# 移除端口
firewall-cmd --permanent --remove-port=8080/tcp
#重启防火墙(修改配置后要重启防火墙)
firewall-cmd --reload

# 参数解释
1、firewall-cmd：是Linux提供的操作firewall的一个工具；
2、--permanent：表示设置为持久；
3、--add-port：标识添加的端口；
```
