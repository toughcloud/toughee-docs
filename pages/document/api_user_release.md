# 用户MAC/Vlan解除绑定

## 接口描述

第三方系统向硬派计费系统发起用户解绑请求，支持清除用户当前MAC和Vlan绑定,硬派计费系统返回成功或失败响应。

## 接口地址

http://服务器地址:端口/api/v1/account/release

## 请求参数

- account_number (string) – 用户账号

CURL 请求示例：

    curl "http://127.0.0.1:1816/api/v1/account/release?sign=0E932AA4F17CFAB2CC604A738930320D&account_number=ua00000004"

## 接口响应

响应示例：

    {
        "msg": "处理成功",
        "nonce": "1490323625",
        "code": 0,
        "sign": "DDBA963FFE0A6CD2455CCFAFDC623243"
    }
