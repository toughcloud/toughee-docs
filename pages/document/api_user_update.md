# 用户计费策略修改

## 接口描述

第三方系统向硬派计费系统发起用户账号修改请求，支持修改用户计费策略，硬派计费系统返回成功或失败响应。

## 接口地址

http://服务器地址:端口/api/v1/account/update

## 请求参数

- account_number (string) – 用户账号
- ip_address (string - x.x.x.x) – 用户IP地址
- install_address (string) – 用户安装地址
- domain (string) – 用户域，对BRAS的特定扩展
- user_concur_number (int) – 用户在线数限制
- bind_mac (int - 0 不绑定 1 绑定) – 用户是否绑定mac
- bind_vlan (int 0 不绑定 1 绑定) – 用户是否绑定vlan
- account_desc (string) – 用户修改描述

CURL 请求示例：

    curl "http://127.0.0.1:1816/api/v1/account/update?sign=5256F72A7BFA2FFE08D6EADAE30CA513&account_number=ua00000004&user_concur_number=1&bind_mac=0&bind_vlan=0"

## 接口响应

响应示例：

    {
        "msg": "处理成功",
        "nonce": "1490322979",
        "code": 0,
        "sign": "B7ED73B9AD0CFD2257E24B3FD035F0DE"
    }
