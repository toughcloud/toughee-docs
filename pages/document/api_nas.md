# NAS 查询

## 接口描述

第三方系统向硬派计费系统发起NAS查询请求，硬派计费返回NAS信息列表。支持可选的NAS IP地址参数。

NAS 数据结构：

![](http://qnstatic.toughcloud.net/toughee_nas_db.png)

## 接口地址

http://服务器地址:端口/api/v1/nas/query

## 请求参数

- ip_addr：nas ip地址

CURL 请求示例：

    curl "http://127.0.0.1:1816/api/v1/nas/query?sign=C746B12E9B57BD2EBF0FDF78F7DFFABE"

## 接口响应

响应示例：

    {
        "msg": "处理成功",
        "nonce": "1490278914",
        "code": 0,
        "data": [
            {
                "id": "1",
                "ip_addr": "127.0.0.1",
                "coa_port": 3799,
                "dns_name": null,
                "vendor_id": "0",
                "ac_port": 2000,
                "portal_vendor": null,
                "bas_secret": "secret",
                "nas_id": null,
                "bas_name": "local bras",
                "time_type": 0,
                "sync_ver": "1487134899056216"
            }
        ],
        "sign": "1D2A3D4B47BDEAC31DCBC98134BBDC9F"
    }

