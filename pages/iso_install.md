# Linux 安装配置指导

## 安装准备

最低服务器配置：CPU 1核心，内存1G，硬盘20G，百兆/千兆网卡

## 下载硬派网络计费系统镜像

镜像下载地址： https://pan.baidu.com/s/1bpgKC5h

镜像基于 openSUSE Leap 42.1 发行版，内置硬派网络计费系统服务，数据库支持Sqlite,Mariadb。

- 系统用户名密码

toughee/toughee 计费系统使用该用户运行

root/toughradius 系统 root 用户

### 光盘 ISO 镜像

内置 Sqlite 数据库，如果你的系统配置较低，可使用该镜像

ToughRADIUS_Enterprise_Edition.x86_64-3.0.0.iso

内置 Mysql(Mariadb) 数据库

ToughRADIUS_Enterprise_Edition_Mysql.x86_64-3.0.0.iso

请使用光盘刻录工具刻录可引导光盘(非数据光盘)

### 虚拟机格式

1. 支持 VMware Workstation / VirtualBox

ToughRADIUS_Enterprise_Edition.x86_64-3.0.0.vmx.tar.gz


2. 支持 OVF Virtual Machine / ESX

ToughRADIUS_Enterprise_Edition.x86_64-3.0.0.ovf.tar.gz


3. 支持 SUSE Cloud / OpenStack / KVM

ToughRADIUS_Enterprise_Edition.x86_64-3.0.0.qcow2.tar.gz

## 镜像安装流程





## 系统端口说明

默认端口如下：

- 16370 默认 redis 服务端口，与 radiusd.json 配置相符合
- 1816  默认管理控制台端口，可以通过http://服务器地址:1816 访问 
- 1819  默认自助服务端口，可以通过http://服务器地址:1819 访问 
- 1812  默认 Radius 认证端口，提供路由器接入设备访问
- 1813  默认 Radius 记账端口，提供路由器接入设备访问


