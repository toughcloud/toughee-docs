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

请使用光盘刻录工具刻录可引导光盘(非数据光盘)。

### 硬盘镜像格式

ToughRADIUS_Enterprise_Edition.x86_64-3.0.0.udev.tar.gz

可直接写入U盘或硬盘

### 虚拟机格式

- VMware Workstation / VirtualBox

ToughRADIUS_Enterprise_Edition.x86_64-3.0.0.vmx.tar.gz

- OVF Virtual Machine / ESX

ToughRADIUS_Enterprise_Edition.x86_64-3.0.0.ovf.tar.gz


- SUSE Cloud / OpenStack / KVM

ToughRADIUS_Enterprise_Edition.x86_64-3.0.0.qcow2.tar.gz

## 镜像安装流程

- 插入光盘（或引导U盘），进入引导界面

![install](http://qnstatic.toughcloud.net/FoGxyRaceovlUaY1mGIt2Hw8LbTI)

请选择第二项 install，

![install](http://qnstatic.toughcloud.net/Fhg5OZR9waR7LIFZx66j9ohkLrBx)

- 选择格式化硬盘，自动写入镜像

![install](http://qnstatic.toughcloud.net/Fomatf4KSeQdxxMTAhuqOytzJPkN)

![untitled5.png](http://qnstatic.toughcloud.net/Fi-jV4FxteZsfK8rTkCbQOBiPQrq)

![install](http://qnstatic.toughcloud.net/FqqnlDxXplfHUVFernGLS9kKaiaW)

- 进入软件许可界面，选中(agree),按 F10 继续

![agree lic](http://qnstatic.toughcloud.net/Fghrt0sEocYsanriMJG5Wppg0Lwy)

- 设置主机名

![hostname](http://qnstatic.toughcloud.net/FnH4RXCGHBJka--3LXowLFZdJyzA)

- 设置网络

![network](http://qnstatic.toughcloud.net/FuujBNz5r6Z6Gd-K7fKO90ZoUvGU)

选择 yes 进入下一步网络配置，选择 no 跳过，安装完成之后可进入系统配置。

![network](http://qnstatic.toughcloud.net/FvXysz_J2d1NgvfXpiX4b-NqVsfd)

按 F4 可配置已有网络接口，F3 新增接口，F5 删除接口

![network](http://qnstatic.toughcloud.net/Fky945Yz9wmYCX57RD4PVssweIVS)

根据实际情况配置使用 DHCP 或 手工配置 IP。 按 F10 继续完成安装。

![network](http://qnstatic.toughcloud.net/FrKYqregCq6PnnCVZwdQALRt7QR0)

![done](http://qnstatic.toughcloud.net/Fl4DIt03Og_VJi45uChcrQyAOJ7l)

![done](http://qnstatic.toughcloud.net/FjuCWV8atR8R6VIxU00NGU1c4oiW)

当出现登录指示时，系统安装完成，服务已运行。

- 登录系统，查看状态

使用 toughee 或 root 用户登录查看状态

使用 ip addr show 查看服务器 IP 地址

![ipaddr](http://qnstatic.toughcloud.net/Fnbmjti_lIUlBUtIGbhA3XM6sSmU)

使用 systemctl status toughee 查看服务状态

![status](http://qnstatic.toughcloud.net/FkOUYZ8abQsDRZS_n9aZRnPcWeEM)

查看管理系统日志

![logger](http://qnstatic.toughcloud.net/FhskHh1nzh8-wzTLd8LR5zCAHbsC)

- 打开浏览器，进入系统管理界面

![login](http://qnstatic.toughcloud.net/FkkNuvdCV9Le1BLViNy92yL6Olv5)


## 系统端口说明

默认端口如下：

- 16370 默认 redis 服务端口，与 radiusd.json 配置相符合
- 1816  默认管理控制台端口，可以通过http://服务器地址:1816 访问 
- 1819  默认自助服务端口，可以通过http://服务器地址:1819 访问 
- 1812  默认 Radius 认证端口，提供路由器接入设备访问
- 1813  默认 Radius 记账端口，提供路由器接入设备访问


