# 区域查询

## 接口描述

第三方系统向硬派计费系统发起区域查询请求，硬派计费返回区域信息列表。支持可选的区域ID参数。

区域数据结构：

![](http://qnstatic.toughcloud.net/toughee_node_db.png)

## 接口地址

http://服务器地址:端口/api/v1/node/query

## 请求参数

- node_id：区域ID，可选，最大32位

CURL 请求示例：

    curl "http://127.0.0.1:1816/api/v1/node/query?sign=C746B12E9B57BD2EBF0FDF78F7DFFABE"

## 接口响应

响应示例：

    {
        "msg": "处理成功",
        "nonce": "1490277739",
        "code": 0,
        "data": [
            {
                "id": "1",
                "node_name": "默认区域",
                "node_desc": "默认区域",
                "rule_id": "1"
                "sync_ver": "1490236888333415",
            }
        ],
        "sign": "A5BC90D072172A4CC57A7D670A5E1D18"
    }

