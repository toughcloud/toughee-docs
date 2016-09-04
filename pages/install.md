# 安装配置指导

## 安装环境

centos6/7, ubuntu 14+,其他linux x64系统，推荐使用 centos7

## 下载硬派网络计费系统

    cd /opt
    wget http://download.toughradius.net/toughee-stable-v2-linux-x64.tar.xz -O toughee-v2-linux-x64.tar.xz

## 部署系统

    cd /opt
    tar Jxvf toughee-v2-linux-x64.tar.xz

解压缩得到 /opt/toughrun 目录

>> 注意： /opt/toughrun 是默认目录，如果要修改此目录，必须同时修改 Makefile 和 radiusctl, radiusd.conf 文件中的对应路径。

执行 make all 安装

    cd /opt/toughrun 
    make all

首次使用还需初始化数据库，根据实际情况修改 /opt/toughrun/etc/radiusd.json 的数据库配置，默认采用 sqlite 数据库。

    radiusctl initdb

##  运行系统

启动 Radius 服务

    radiusctl daemon -s startup                     # 启动 Radius 服务进程，

停止服务

    radiusctl daemon -s shutdown                    # 停止 Radius 服务进程

查看状态

    radiusctl daemon -s status                      # 查看 Radius 服务进程运行状态

重载配置

    radiusctl daemon -s reload                      # 修改配置文件后重新加载服务

查看日志

    radiusctl daemon -s "tail -f manage"            # tail 模式查看管理控制台日志
    radiusctl daemon -s "tail -f worker:worker0"    # tail 模式查看 radius 认证记账日志
    radiusctl daemon -s "tail -f ssportal"          # tail 模式查看自助服务系统日志
    radiusctl daemon -s "tail -f task"              # tail 模式查看定时任务日志

> 注意，worker 进程可以配置多个, 进程名为 worker:worker0， worker:worker1 ...

## 使用系统

系统使用的端口可以在 /opt/toughrun/etc/radiusd.json 中修改

默认端口如下：

- 16370 默认 redis 服务端口，与 radiusd.json 配置相符合
- 1816  默认管理控制台端口，可以通过http://服务器地址:1816 访问 
- 1819  默认自助服务端口，可以通过http://服务器地址:1819 访问 
- 1812  默认 Radius 认证端口，提供路由器接入设备访问
- 1813  默认 Radius 记账端口，提供路由器接入设备访问


