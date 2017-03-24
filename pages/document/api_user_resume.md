# 用户复机

## 接口描述

第三方系统向硬派计费系统发起用户复机请求,硬派计费系统返回成功或失败响应。

> 注意，只有处于停机状态的用户才需要停机，用户复机后，账号恢复认证功能，根据停机时间自动计算顺延到期日期。

## 接口地址

http://服务器地址:端口/api/v1/account/resume

## 请求参数

- account_number (string) – 用户账号

CURL 请求示例：

    curl "http://127.0.0.1:1816/api/v1/account/resume?sign=0E932AA4F17CFAB2CC604A738930320D&account_number=ua00000004"

## 接口响应

响应示例：

    {
        "msg": "处理成功",
        "nonce": "1490324605",
        "code": 0,
        "sign": "6C40BF8C15764D07FD3D2CC6771C5601"
    }
