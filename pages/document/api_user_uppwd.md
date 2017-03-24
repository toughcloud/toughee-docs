# 用户密码修改

## 接口描述

第三方系统向硬派计费系统发起用户密码修改请求，硬派计费系统返回成功或失败响应。

## 接口地址

http://服务器地址:端口/api/v1/account/password/update

## 请求参数

- account_number (string) – 用户账号
- password (string) – 用户新密码

CURL 请求示例：

    curl "http://127.0.0.1:1816/api/v1/account/password/update?sign=7767FE104A9E9ABC78B2A996A75D62F4&account_number=ua00000004&password=888888"

## 接口响应

响应示例：

    {
        "msg": "处理成功",
        "nonce": "1490323342",
        "code": 0,
        "sign": "F7EC12B132D2BB6DFF8C28D0713A434C"
    }
