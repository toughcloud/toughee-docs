# 用户账号查询

## 接口描述

第三方系统向硬派计费系统发起用户账号查询请求，硬派计费返回用户账号信息。支持查询一个或多个账号

用户账号数据结构：

> 上网账号表，每个会员可以同时拥有多个上网账号，account_number 为每个套餐对应的上网账号，每个上网账号全局唯一

> 用户状态：0:"未激活",1:"正常", 2:"停机" , 3:"销户", 4:"到期"

![](http://qnstatic.toughcloud.net/toughee_account_db.png)

## 接口地址

http://服务器地址:端口/api/v1/account/query

## 请求参数

- account_number: 用户账号
- mac_addr: 用户mac地址
- product_id: 用户资费ID

CURL 请求示例：

    curl "http://127.0.0.1:1816/api/v1/account/query?sign=C746B12E9B57BD2EBF0FDF78F7DFFABE"

## 接口响应

处于安全考虑，响应信息不包含明文密码

响应示例：


    {
        "msg": "处理成功",
        "nonce": "1490279685",
        "code": 0,
        "data": [
            {
                "user_concur_number": 1,
                "domain": null,
                "time_length": 0,
                "install_address": "默认小区地址",
                "sync_ver": "1490237809026803",
                "flow_length": 0,
                "account_desc": "",
                "vlan_id2": 0,
                "vlan_id1": 0,
                "expire_date": "2017-04-22",
                "customer_id": "9D9E2AA30F7311E7AAAB542696D1B7F7",
                "last_pause": null,
                "account_number": "ua00000004",
                "status": 0,
                "bind_mac": 0,
                "update_time": "2017-03-23 10:51:29",
                "bind_vlan": 0,
                "ip_address": "",
                "group_id": null,
                "product_id": "buyoutmonth10m",
                "create_time": "2017-03-23 10:51:29",
                "mac_addr": "",
                "balance": 0
            },
            {
                "user_concur_number": 1,
                "domain": null,
                "time_length": 0,
                "install_address": "默认小区地址",
                "sync_ver": "1490240631153023",
                "flow_length": 0,
                "account_desc": "",
                "vlan_id2": 0,
                "vlan_id1": 0,
                "expire_date": "2017-04-22",
                "customer_id": "EDFD41610F7A11E78676542696D1B7F7",
                "last_pause": null,
                "account_number": "ua00000005",
                "status": 1,
                "bind_mac": 0,
                "update_time": "2017-03-23 11:43:51",
                "bind_vlan": 0,
                "ip_address": "",
                "group_id": null,
                "product_id": "buyoutmonth10m",
                "create_time": "2017-03-23 11:43:51",
                "mac_addr": "",
                "balance": 0
            },
            {
                "user_concur_number": 1,
                "domain": null,
                "time_length": 0,
                "install_address": "",
                "sync_ver": "1490276941861730",
                "flow_length": 0,
                "account_desc": "",
                "vlan_id2": 0,
                "vlan_id1": 0,
                "expire_date": "2017-02-10",
                "customer_id": "78DBDC3D0FCF11E794C6542696D1B7F7",
                "last_pause": null,
                "account_number": "userp22",
                "status": 1,
                "bind_mac": 0,
                "update_time": "2017-03-23 21:49:01",
                "bind_vlan": 0,
                "ip_address": "",
                "group_id": null,
                "product_id": "buyoutmonth10m",
                "create_time": "2017-03-23 21:49:01",
                "mac_addr": "",
                "balance": 0
            }
        ],
        "sign": "4DFA973BFE6176D5B992263A64AA2B18"
    }
