
# 硬派计费系统安装配置指南

## 安装环境

linux/BSD 64位系统， 推荐使用 centos7, opsuse 14
systemd支持：操作系统最好支持systemd管理服务

## 上传软件至服务器

将你获取的软件安装包toughee-linux-x64.tar.xz 上传至服务器 /opt 目录, 正确的路径应该是：

    /opt/toughee-linux-x64.tar.xz

## 部署系统

    cd /opt
    tar xvf toughee-linux-x64.tar.xz

解压缩得到 /opt/toughee 目录

> ☞ 注意： /opt/toughee 是默认目录，建议不要修改目录

执行 make all 安装

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

    systemctl start toughee  #启动服务，注意系统开机时会自动启动服务，无需人工启动
    systemctl stop toughee  #停止服务
    systemctl status toughee #查看服务状态


## 使用系统

系统使用的端口可以在 /opt/toughee/etc/toughee.json 中修改

默认端口如下：

- 1816  默认管理控制台端口，可以通过http://服务器地址:1816 访问 
- 1819  默认自助服务端口，可以通过http://服务器地址:1819 访问 
- 1812  默认 Radius 认证端口，提供路由器接入设备访问
- 1813  默认 Radius 记账端口，提供路由器接入设备访问

> ☞ 硬派网络计费系统提供了基于WEB浏览器的管理界面，为了更好地操作体验，建议您使用IE9以上浏览器，推荐使用Chrome内核浏览器，以及火狐浏览器获得更好的效果。在较老的 IE 版本上会有一些兼容性问题。

## 其他说明
 
- 服务使用toughee用户运行，为保证安全尽量不要修改为root用户，toughee用户必须有 /opt/toughee,/var/toughee的读写权限
- 注意初次运行，可能因防火墙启动而无法访问，请开放1816/tcp,1819/tcp,1812/udp,1813/udp端口。
- 请合理分配计费系统操作权限，保证系统安全。
- 每个进程都会占用一定的mysql连接数，请注意合理优化mysql性能。
- linux新系统一定要优化内核，加大连接数，不然不能应对高并发。
- 计费系统默认又一个自动备份功能，但不太适合大数据量的备份恢复，建议使用mysql本身的备份功能来进一步保证数据安全，并且将数据文件远程备份。

### mysql备份脚本

系统内置了一个mysql备份脚本，在/opt/toughee/bin/mysql_backup,修改下配置，可以加入系统定时任务执行每日备份

上网日志表不备份，默认保留14天的备份

    !/bin/bash
    # toughee database backup script
    # 01 1 * * *  sh /opt/toughee/bin/mysql_backup  # crontab任务定义
    
    USER="root" 
    PASSWORD=  #根据实际修改
    OUTPUT="/backup" #备份目录,自动创建
    DATABASES=("mysql" "toughee") # 需要备份的数据库表
    
    test -d $OUTPUT || mkdir -p $OUTPUT #自动创建备份目录
    
    # 自动删除14天以前的备份文件，请根据实际调整
    find $OUTPUT -name "*.sql.xz" -type f -mtime +14 -exec rm -f {} \; > /dev/null 2>&1
    
    for db in ${DATABASES[@]}; do
        echo "backup database: $db"
        mysqldump --force --opt --user=$USER \
            --password=$PASSWORD --databases $db \
            --ignore-table=toughee.tr_ticket > $OUTPUT/date +%Y%m%d.$db.sql
    xz -f $OUTPUT/date +%Y%m%d.$db.sql
    done
    


## linux 内核优化

默认情况下，linux系统有一些限制，并不能直接支持高并发性能，需要做一些内核优化。

### 把以下内容加入 /etc/sysctl.conf

    net.ipv4.ip_forward=1
    net.ipv4.tcp_syncookies = 1
    net.ipv4.tcp_tw_reuse = 1
    net.ipv4.tcp_tw_recycle = 1
    net.ipv4.tcp_fin_timeout = 30
    net.ipv4.tcp_keepalive_time = 1200
    net.ipv4.ip_local_port_range = 10000 65000
    net.ipv4.tcp_max_syn_backlog = 8192
    net.ipv4.tcp_max_tw_buckets = 5000
    net.ipv4.tcp_max_syn_backlog = 65536
    net.core.netdev_max_backlog = 32768
    net.core.somaxconn = 32768
    net.core.wmem_default = 8388608
    net.core.rmem_default = 8388608
    net.core.rmem_max = 16777216
    net.core.wmem_max = 16777216
    net.ipv4.tcp_synack_retries = 2
    net.ipv4.tcp_syn_retries = 2
    net.ipv4.tcp_tw_reuse = 1
    net.ipv4.tcp_wmem = 8192 436600 873200
    net.ipv4.tcp_rmem  = 32768 436600 873200
    net.ipv4.tcp_mem = 94500000 91500000 92700000
    net.ipv4.tcp_max_orphans = 3276800
    net.ipv4.tcp_fin_timeout = 30
    vm.overcommit_memory = 1

执行 sysctl -p

### 修改 /etc/security/limits.conf

加入以下内容至末尾

    *  soft nproc 40000
    *  hard nproc 40000
    *  soft nofile 40000
    *  hard nofile 40000

### 修改 /etc/pam.d/login

加入以下内容至末尾

    session required /lib64/security/pam_limits.so
    session required pam_limits.so


### 修改 /etc/profile

加入以下指令到末尾

    ulimit -n 65535

重启一下系统，执行 ulimit -a 可以看到优化结果，执行 ulimit -n 可以看到最大连接数限制，默认是1024

