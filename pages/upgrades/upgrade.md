# 版本升级指南

### V3.x 版本升级办法

该升级方法适用于V3.x - V4.0.0.1 之前的版本。注意该升级办法为在线升级，请保持服务器可以连接互联网。

此方法主要通过完整重建数据恢复数据来实现（只有在数据库结构变动的情况下）

重新初始化数据库会清除上网日志，上网日志不在备份任务列表，因此会丢失上网日志，如果需要保存上网日志，请另外执行额外的备份。

#### 升级流程

1. 备份数据库：登录管理系统，进入系统管理菜单下的数据备份管理，执行备份。

    > 注意：如果新版本并没有数据库结构变化（参考版本说明），无需执行这一步 

2. 在服务器 linux 终端，初始化数据库。

    cd /opt/toughee && make initdb

    > 注意：如果新版本并没有数据库结构变化（参考版本说明），无需执行这一步 

3. 在服务器 linux 终端，执行升级指令：

    /opt/toughee/upgrade stable   #企业版正式版升级
    /opt/toughee/upgrade dev   #企业版开发版升级
    /opt/toughee/upgrade free_stable   #社区免费版正式版升级
    /opt/toughee/upgrade free_dev   #社区免费版开发版升级

4. 重启服务

    systemctl restart toughee

5. 恢复数据库：登录系统，进入系统管理菜单下的数据备份管理，执行恢复。

    > 注意：如果新版本并没有数据库结构变化（参考版本说明），无需执行这一步 


### V4.x 版本的升级

该升级方法适用于V4.0.0.4 以后的版本。注意该升级办法为在线升级，请保持服务器可以连接互联网。

相比老版本，该方法对数据库采取部分重建升级的方式，避免未备份的日志数据丢失。

#### 升级流程

1. 在服务器 linux 终端，执行数据库备份指令：

    cd /opt/toughee && make backup

    > 注意：如果新版本并没有数据库结构变化（参考版本说明），无需执行这一步

2. 在服务器 linux 终端，执行升级指令：

    /opt/toughee/upgrade stable   #企业版正式版升级
    /opt/toughee/upgrade dev   #企业版开发版升级
    /opt/toughee/upgrade free_stable   #社区免费版正式版升级
    /opt/toughee/upgrade free_dev   #社区免费版开发版升级

3. 在服务器 linux 终端，执行数据库升级指令：

    cd /opt/toughee && make updb

    > 注意：如果新版本并没有数据库结构变化（参考版本说明），无需执行这一步


4. 重启服务

    systemctl restart toughee












