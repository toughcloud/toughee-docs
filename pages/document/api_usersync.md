# 用户开户

## 接口描述

该接口是一个通用用户同步接口，用于第三方系统更自由的控制用户， 该接口主要针对神行者计费专版已经VPN专版，

调用该接口，则计费系统中不会管理费用信息，只是管理用户信息。

## 接口地址

http://服务器地址:端口/api/v1/user/sync

## 请求参数

- realname (string) – 用户姓名
- idcard (string) – 身份证
- address(string) – 地址
- username (string) – 用户账号
- password (string) – 用户密码
- product_code (string) – 产品ID编码
- status= (string) – 用户状态 enabled: 用户新开户或续费时调用，disabled：用户销户时调用
- begin_time (String) - 生效时间 格式为 "%Y-%m-%d %H:%M:%S"(VPN专版) 或 "%Y-%m-%d"(神行者计费专版)
- expire_time (String) -  过期时间 格式为 "%Y-%m-%d %H:%M:%S"(VPN专版) 或 "%Y-%m-%d"(神行者计费专版)

## 扩展参数

扩展参数以 “attr_” 开始， 当前支持的参数

- attr_NODE_ID (string) – 区域节点ID



## 请求示例：

    http://127.0.0.1:1816/api/v1/user/sync?sign=AA0C961396EE14A41A245727526E0CEF
    &realname=张三
    &username=zsan
    &password=123456
    &idcard=0000
    &address=myaddress
    &begin_time=2016-02-10
    &expire_time=2017-02-10
    &product_code=0E77AB90BD1B11E6849640F2E9955DBA
    &status=enabled
    &attr_NODE_ID=1

## 接口响应

响应示例：

    {
        "msg": "处理成功",
        "nonce": "1490276941",
        "code": 0,
        "sign": "67C3F992DDBC08655700655236180AF4"
    }

