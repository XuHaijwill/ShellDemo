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
> tcp    LISTEN     0      128    [::]:3306               [::]:*  
>
> 

