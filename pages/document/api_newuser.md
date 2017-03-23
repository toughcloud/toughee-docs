# 用户开户

## 接口描述

第三方系统向硬派计费系统发起开户请求，实现新账号的注册，硬派计费系统返回成功或失败响应。

## 接口地址

http://服务器地址:端口/api/v1/customer/add

## 请求参数

- account_number (string) – 用户账号
- billing_type (int) – 计费模式，0 首次上线计费 1 立即计费
- customer_id (string) – 客户ID，16-32位字符串（可选）
- order_id (string) – 交易ID，16-32位字符串（可选）
- product_id (string) – 订购资费ID
- node_id (string) – 用户区域ID
- area_id (string) – 用户社区ID（可选）
- agency_id (string) – 代理商ID（可选）
- realname (string) – 用户姓名
- password (string) – 用户账号密码
- ip_address (string) – 用户IP地址
- idcard (string) – 用户身份证号码（可选）
- email (string) – 用户电子邮箱（可选）
- mobile (string) – 用户手机号码（可选）
- address (string) – 用户地址（可选）
- customer_desc (string) – 用户描述备注（可选）
- expire_date (string) – 用户到期时间 yyyy-mm-dd
- months (int) – 用户订购月数，预付费包月有效
- days (int) – 用户订购天数，预付费包日有效
- fee_value (string) – 交易费用 x.xx (元)

CURL 请求示例：

    curl -X "POST" "http://127.0.0.1:1816/api/v1/customer/add?sign=AA0C961396EE14A41A245727526E0CEF&account_number=userp22&customer_name=userp2&node_id=1&realname=userp2&begin_date=2016-02-10&expire_date=2017-02-10&product_id=0E77AB90BD1B11E6849640F2E9955DBA&time_length=0&flow_length=0&balance=0&password=888888&fee_value=360.00"

## 接口响应

响应示例：

    {
        "msg": "处理成功",
        "nonce": "1490276941",
        "code": 0,
        "sign": "67C3F992DDBC08655700655236180AF4"
    }

