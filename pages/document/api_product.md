# 资费套餐查询

## 接口描述

第三方系统向硬派计费系统发起资费套餐请求，硬派计费返回资费套餐列表。支持可选的参数资费ID参数。

资费数据结构：

> 资费类型 product_policy 0 预付费包月 1 预付费时长 2 买断包月 3 买断时长 4 预付费流量 5 买断流量 6 自由资费
> 销售状态 product_status 0 正常 1 停用 资费停用后不允许再订购

![](http://qnstatic.toughcloud.net/toughee-product-db.png)

## 接口地址

http://服务器地址:端口/api/v1/product/query

## 请求参数

- product_id：资费ID，可选，最大32位

CURL 请求示例：

    curl -X "GET" “http://127.0.0.1:1816/api/v1/product/query?sign=1B8F4F7F9DC9B423B5BA5A428B5CEE81&product_id=0E77AB90BD1B11E6849640F2E9955DBA”

## 接口响应

响应示例：

    {
        "msg": "处理成功",
        "nonce": "1483509278",
        "code": 0,
        "data": [
            {
                "product_policy": 0,
                "bind_mac": 0,
                "update_time": "2016-12-10 01:52:51",
                "free_auth": 0,
                "fee_times": 0,
                "fee_flows": 0,
                "create_time": "2016-12-08 15:50:58",
                "free_auth_uprate": 0,
                "output_max_limit": 10485760,
                "bind_vlan": 0,
                "product_name": "预付费包月10M20元",
                "ispub": 1,
                "concur_number": 0,
                "fee_months": 0,
                "input_max_limit": 10485760,
                "product_status": 0,
                "free_auth_downrate": 0,
                "fee_price": 2000,
                "id": "0E77AB90BD1B11E6849640F2E9955DBA",
            }
        ],
        "sign": "EBB32AD74D767924AF172711E243E052"
    }

