# 用户停机

## 接口描述

第三方系统向硬派计费系统发起用户停机请求，用户停机后，暂时处于无法认证状态,硬派计费系统返回成功或失败响应。

用户停机后，状态变为停用，无法认证，同时记录停机时间

> 注意，只有处于正常状态的用户才能停机

## 接口地址

http://服务器地址:端口/api/v1/account/pause

## 请求参数

- account_number (string) – 用户账号

CURL 请求示例：

    curl "http://127.0.0.1:1816/api/v1/account/pause?sign=0E932AA4F17CFAB2CC604A738930320D&account_number=ua00000004"

## 接口响应

响应示例：

    {
        "msg": "处理成功",
        "nonce": "1490324042",
        "code": 0,
        "sign": "31551BF3CDFD2D5D5424EC0BA5EAAFE2"
    }
