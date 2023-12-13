# Shell

## Shell概览

> 1. 自动化批量系统初始化程序 （update，软件安装，时区设置，安全策略...）
> 2. 自动化批量软件部署程序 （LAMP，LNMP，Tomcat，LVS，Nginx）
> 3. 应用管理程序 (KVM，集群管理扩容，MySQL，DELLR720 批量 RAID）
> 4. 日志分析处理程序（PV, UV, 200, !200, top 100, grep/awk）
> 5. 自动化备份恢复程序（MySQL 完全备份/增量 + Crond）
> 6. 自动化管理程序（批量远程修改密码，软件升级，配置更新）
> 7. 自动化信息采集及监控程序（收集系统/应用状态信 CPU,Mem,Disk,Net,TCP Status,Apache,MySQL）
> 8. 配合 Zabbix 信息采集（收集系统/应用状态信息 CPU,Mem,Disk,Net,TCP Status,Apache,MySQL）
> 9. 自动化扩容（增加云主机——>业务上线）zabbix 监控 CPU 80%+|-50% Python API AWS/EC2（增加/删除云主机） + Shell Script（业务上线）
> 10. 俄罗斯方块，打印三角形，打印圣诞树，打印五角星，运行小火车，坦克大战，排序算法实现
> 11. Shell 可以做任何事（一切取决于业务需求）

## 程序语言执行：

> 程序语言执行：
>
> C —— 编译 —— 二进制机器码 （CPU X86 复杂指令集, Power 精简指令集，
>
> APM）
>
> Java —— 编译 —— 字节码（Java 虚拟机 JDK） Tomcat/Hadoop 
>
> shell —— 解释 （/usr/bin/bash）
>
> perl —— 解释 （/usr/bin/perl）
>
> expect —— 解释 （/usr/bin/expect）
>
> Python —— 解释 ( /usr/bin/python)
>
> —— 编译 —— 字节码（Python 虚拟机

## 基本使用

> 过滤端口状态 
>
> [root@192 ~]# ss -an | grep 3306
> tcp    LISTEN     0      128       *:3306                  *:*                  
> tcp    LISTEN     0      128    [::]:3306               [::]:*  ping命令
>
> [root@192 ~]# ping -c1 www.baidu.com &> /dev/null && echo "www.baidu.com is up" || echo "www.baidu.com is down" 
> www.baidu.com is up
> [root@192 ~]# ping -c1 www.baidu.com  && echo "www.baidu.com is up" || echo "www.baidu.com is down" 
> PING www.baidu.com (120.232.145.144) 56(84) bytes of data.
> 64 bytes from 120.232.145.144 (120.232.145.144): icmp_seq=1 ttl=128 time=11.7 ms
>
> --- www.baidu.com ping statistics ---
> 1 packets transmitted, 1 received, 0% packet loss, time 0ms
> rtt min/avg/max/mdev = 11.742/11.742/11.742/0.000 ms
> www.baidu.com is up
>
> [root@192 ~]# /usr/bin/python <<-EOF
> > print "hello world!"
> > print "2222"
> > print "3333"
> > EOF
> > hello world!
> > 2222
> > 3333

### shell中调用python

![image-20231210212014164](docs\imgs\image-20231210212014164.png)

> rpm -qc bash

![image-20231210214022971](docs\imgs\image-20231210213351715.png)

> 查询作业
>
> jobs

> 1. 命令和文件自动补齐
>
> 2. 命令历史记忆功能 上下键、!number、!string、!$、!!、^R
>
> 3. 别名功能 alias、unalias cp、~username/.bashrc、\cp -rf /etc/hosts .
>
> 4. 快捷键 ^R、^D、^A、^E、^L、^U、^K、^Y、^S、^Q
>
> 5. 前后台作业控制 &、nohup、^C、^Z、bg %1、fg %1、kill %3、screen
>
> 6. 输入输出重定向 0,1,2 > >> 2>（错误输出） 2>>（错误输出追加） 2>&1（2到1） &> cat < /etc/hosts cat <<EOF cat >file1 <<EOF



> ## 管道 | tee
>
> ip addr |grep 'inet ' |grep eth0
>
> ip addr |grep 'inet ' |tee test |grep eth0 覆盖
>
> ip addr |grep 'inet ' |tee -a test |grep eth0 -a 追加
>
> df |grep '/$'
>
> df |tee df.txt |grep '/$'
>
> [root@test~]# date > date.txt
>
> [root@test~]# date |tee date.txt
>
> Fri Aug 25 15:30:20 CST 2017
>
> ## 命令排序
>
> ; 不具备逻辑判断
>
> cd; eject 
>
> && || 具备逻辑判断
>
> ./configure && make && make install （命令返回值 echo $?）
>
> mkdir /var/111/222/333 && echo ok
>
> mkdir -p /var/111/222/333 && echo ok
>
> ls /home/111/222/333/444 || mkdir -p /home/111/222/333/444
>
> [ -d /home/111/222/333/444 ] || mkdir -p /home/111/222/333/444
>
> ping -c1 10.18.42.1 &>/dev/null && echo up || echo down
>
> ============================================================
>
> 注意：
>
> command & 后台执行
>
> command &>/dev/null 混合重定向（标准输出 1，错误输出 2）
>
> command1 && command2 命令排序，逻辑判断
>
> ============================================================

> ## shell 通配符（元字符）表示的不是本意
>
> \* 匹配任意多个字符 ls in* rm -rf * rm -rf *.pdf find / -iname "*-eth0"
>
> ? 匹配任意一个字符 touch love loove live l7ve; ll l?ve
>
> [] 匹配括号中任意一个字符 [abc] [a-z] [0-9] [a-zA-Z0-9] [ ^a-zA-Z0-9] ll l[io]ve ll l[ ^a-z]ve ll /dev/sd[a-z]
>
> () 在子 shell 中执行(cd /boot;ls) (umask 077; touch file1000)
>
> {} 集合 touch file{1..9} 
>
> \# mkdir /home/{111,222} mkdir -pv /home/{333/{aaa,bbb},444}
>
> \# cp -rv /etc/sysconfig/network-scripts/ifcfg-eth0 /etc/sysconfig/network-scripts/ifcfg-eth0.old
>
> \# cp -rv /etc/sysconfig/network-scripts/{ifcfg-eth0,ifcfg-eth0.old}
>
> \# cp -rv /etc/sysconfig/network-scripts/ifcfg-eth0{,.old}\ 转义符，让元字符回归本意
>
> \# echo * 
>
> \# echo \*
>
> \# touch yang\sheng
>
> mkdir \\
>
> echo -e "atb"
>
> echo -e "a\tb"
>
> echo -e "anb" 
>
> echo -e "a\nb" 
>
> ## echo 输出带颜色文本
>
> echo --help
>
> ![image-20231211093753379](docs\imgs\image-20231211093753379.png)
>
> ## printf 格式化输出文本

## shell 变量

### 变量的类型

> 1. 自定义变量
>
> 定义变量： 变量名=变量值 变量名必须以字母或下划线开头，区分大小写
>
> ip1=192.168.2.115 
>
> 引用变量： $变量名 或 ${变量名}
>
> 查看变量： echo $变量名 set(所有变量：包括自定义变量和环境变量)
>
> 取消变量： unset 变量名
>
> 作用范围： 仅在当前 shell 中有效



> 2. 环境变量
>
> 定义环境变量： 方法一 export back_dir2=/home/backup 
>
> 方法二 export back_dir1 将自定义变量转换成环境变量
>
> 引用环境变量： $变量名 或 ${变量名}
>
> 查看环境变量： echo $变量名 env 例如 env |grep back_dir2
>
> 取消环境变量： unset 变量名
>
> 变量作用范围： 在当前 shell 和子 shell 有效
>
> =======================================================
>
> C 语言 局部变量 vs 全局变量
>
> SHELL 自定义变量 vs 环境变量
>
> =======================================================



> 3. 位置变量
>
> $1 $2 $3 $4 $5 $6 $7 $8 $9 ${10}



> 4. 预定义变量
>
> $0 脚本名
>
> $* 所有的参数
>
> $@ 所有的参数
>
> $# 参数的个数
>
> $$ 当前进程的 PID
>
> $! 上一个后台进程的 PID
>
> $? 上一个命令的返回值 0 表示成功
>
> > 示例 1：
> >
> > \# vim test.sh
> >
> > echo "第 2 个位置参数是$2"
> >
> > echo "第 1 个位置参数是$1"
> >
> > echo "第 4 个位置参数是$4"
> >
> > echo "所有参数是: $*"
> >
> > echo "所有参数是: $@"
> >
> > echo "参数的个数是: $#"
> >
> > echo "当前进程的 PID 是: $$"
> >
> > echo '$1='$1
> >
> > echo '$2='$2
> >
> > echo '$3='$3
> >
> > echo '$*='$*
> >
> > echo '$@='$@
> >
> > echo '$#='$#
> >
> > echo '$$='$$
>
> **了解$\*和$@区别** 
>
> > 示例 2：
> >
> > \# vim ping.sh
> >
> > \#!/bin/bash 
> >
> > ping -c2 $1 &>/dev/null 
> >
> > if [ $? = 0 ];then 
> >
> > echo "host $1 is ok" 
> >
> > else 
> >
> > echo "host $1 is fail" 
> >
> > fi 
> >
> > \# chmod a+x ping.sh
> >
> > \# ./ping.sh 192.168.2.25
>
> basename /etc/sysconfig/network... 输出文件名
>
> dirname ...
>
> ![image-20231213084943096](docs\imgs\image-20231213084648626.png)
>
> ![image-20231213085122637](docs\imgs\image-20231213085122637.png)

### 变量的赋值方式：

> 1. 显式赋值
>
> 变量名=变量值
>
> 示例：
>
> ip1=192.168.1.251
>
> school="BeiJing 1000phone"today1=`date +%F`
>
> today2=$(date +%F)

> 2. read 从键盘读入变量值
>
> read 变量名
>
> read -p "提示信息: " 变量名
>
> read -t 5 -p "提示信息: " 变量名
>
> read -n 2 变量名

> 示例 3：
>
> \# vim first.sh
>
> back_dir1=/var/backup
>
> read -p "请输入你的备份目录: " back_dir2
>
> echo $back_dir1
>
> echo $back_dir2
>
> \# sh first.sh
>
> 示例 4：
>
> \# vim ping2.sh
>
> \#!/bin/bash 
>
> read -p "Input IP: " ip 
>
> ping -c2 $ip &>/dev/null 
>
> if [ $? = 0 ];then 
>
> echo "host $ip is ok" 
>
> else 
>
> echo "host $ip is fail" 
>
> fi 
>
> \# chmod a+x ping2.sh
>
> \# ./ping.sh
>
> 定义或引用变量时注意事项：
>
> " " 弱引用
>
> ' ' 强引用
>
> [root@test~]# school=1000phone
>
> [root@test~]# echo "${school} is good"
>
> 1000phone is good
>
> [root@test~]# echo '${school} is good'
>
> ${school} is good
>
> ` ` 命令替换 等价于 $() 反引号中的 shell 命令会被先执行
>
> [root@test~]# touch `date +%F`_file1.txt 
>
> [root@test~]# touch $(date +%F)_file2.txt 
>
> [root@test~]# disk_free3="df -Ph |grep '/$' |awk '{print $4}'" 错误
>
> [root@test~]# disk_free4=$(df -Ph |grep '/$' |awk '{print $4}')
>
> [root@test~]# disk_free5=`df -Ph |grep '/$' |awk '{print $4}'`

> ![image-20231213090211531](docs\imgs\image-20231213090211531.png)

### 变量的运算

> 1. 整数运算
>
> 方法一：expr
>
> expr 1 + 2
>
> expr $num1 + $num2 + - \* / %

> 方法二：$(())
>
> echo $(($num1+$num2)) + - * / %
>
> echo $((num1+num2))
>
> echo $((5-3*2)) 
>
> echo $(((5-3)*2))
>
> echo $((2**3))
>
> sum=$((1+2)); echo $sum

> 方法三：$[]
>
> echo $[5+2] + - * / %
>
> echo $[5**2]

> 方法四：let
>
> let sum=2+3; echo $sum
>
> let i++; echo $

### 变量"内容"的删除和替换







## Refrence

> - linux shell 脚本 入门到实战详解 https://blog.csdn.net/weixin_42313749/article/details/120524768
> - 【千锋教育Linux高级程序设计】笔记+视频+源码，全部免费！ https://zhuanlan.zhihu.com/p/638482652
> - https://www.bilibili.com/video/BV1Zb411N74b/
> - 微信打开小程序：http://navo.top/3emE3i