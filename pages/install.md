# Linux 安装配置指导

本文将指引您在通用的 linux 环境下完成硬派网络计费系统的安装配置。

## 安装环境

linux/BSD 64位系统， 推荐使用 centos7, opsuse 14
systemd支持：操作系统最好支持systemd管理服务

## 上传软件至服务器

将你获取的软件安装包toughee-linux-x64.tar.xz 上传至服务器 /opt 目录, 正确的路径应该是：

    /opt/toughee-linux-x64.tar.xz


## 安装部署系统

    cd /opt
    tar xvf toughee-linux-x64.tar.xz

 解压缩得到 /opt/toughee 目录，执行 make all 安装

☞ 注意： /opt/toughee 是默认目录，建议不要修改目录

    cd /opt/toughee 
    make all

 首次使用还需初始化数据库，根据实际情况修改 /opt/toughee/etc/toughee.json 的数据库配置，默认采用 sqlite 数据库。

### mysql 配置说明

进入 mysql 终端管理:

    mysql >  create database toughee DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
    mysql >  GRANT ALL ON toughee.* TO raduser@'127.0.0.1' IDENTIFIED BY 'radpwd' WITH GRANT OPTION;
    mysql >  FLUSH PRIVILEGES;

 修改数据库配置部分,具体参数请根据实际填写。

     "database": {
        "backup_path": "/var/toughee/data",
        "dbtype": "mysql",
        "dburl": "mysql://raduser:radpwd@127.0.0.1:3306/toughee?charset=utf8",
        "echo": 0,
        "pool_recycle": 300,
        "pool_size": 60
    }

## 执行初始化

    cd /opt/toughee 
    make initdb

## 运行系统

使用systemd来管理服务

> systemctl start toughee  #启动服务，注意系统开机时会自动启动服务，无需人工启动
> systemctl stop toughee  #停止服务
> systemctl status toughee #查看服务状态


## 如何使用系统

系统使用的端口可以在 /opt/toughee/etc/toughee.json 中修改, 默认端口如下：

- 1816  默认管理控制台端口，可以通过http://服务器地址:1816 访问 
- 1817  默认微信公众号接口服务端口，可以通过http://服务器地址:1817 访问
- 1819  默认自助服务端口，可以通过http://服务器地址:1819 访问 
- 1820  默认无线认证端口，可以通过http://服务器地址:1820 访问
- 1812  默认 Radius 认证端口，提供路由器接入设备访问
- 1813  默认 Radius 记账端口，提供路由器接入设备访问

系统采用了模块化的设计，每个服务模块可以启动为一个独立的服务进程互不影响，可以把不需要的服务停用。

> 硬派网络计费系统提供了基于WEB浏览器的管理界面，为了更好地操作体验，建议您使用IE9以上浏览器，推荐使用Chrome内核浏览器，以及火狐浏览器获得更好的效果。在较老的 IE 版本上会有一些兼容性问题。

## 其他说明

- 服务使用toughee用户运行，为保证安全尽量不要修改为root用户，toughee用户必须有 /opt/toughee,/var/toughee的读写权限
- 注意初次运行，可能因防火墙启动而无法访问，请开放1816/tcp,1819/tcp,1812/udp,1813/udp端口
- 请合理分配计费系统操作权限，保证系统安全。
- 每个进程都会占用一定的mysql连接数，请注意合理优化mysql性能。
- linux新系统一定要优化内核，加大连接数，不然不能应对高并发。
- 计费系统默认提供一个自动备份功能，但不太适合大数据量的备份恢复，建议使用mysql本身的备份功能来进一步保证数据安全，并且将数据文件远程备份。










