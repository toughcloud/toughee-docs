# 硬派计费API接口

## 协议约定

- 消息发起方：第三方系统。
- 消息接受方：硬派计费系统。
- 接口请求方法：HTTP GET 或 POST 支持标准http1.1协议
- 响应消息格式：JSON：{“code”:0,"msg":"success","name1":"value1"}
- 消息报文编码：UTF-8 注意对参数进行 urlencode 编码
- 接口鉴权：MD5签名，md5(共享密钥+排序的参数值组合字符串)
- 当前接口版本：v1

## 消息签名

将所有参数的值进行排序相加得到排序的参数值字符串，为了安全，可以增加一个随机参数值，比如nonce=123131414,保证nonce每次都不同，nonce的值参与签名计算。

除了直接GET提交，也可以通过Form表单提交

代码参考：

    def make_sign(api_secret, params=[]):
        """
            >>> make_sign("123456",[1,'2',u'中文'])
            '33C9065427EECA3490C5642C99165145'
        """
        _params = [p for p in params if p is not None]
        _params.sort()
        _params.insert(0, api_secret)
        strs = ''.join(_params)
        mds = md5(strs.encode('utf-8')).hexdigest()
        return mds.upper()

    def check_sign(api_secret, msg):
        """
            >>>  check_sign("123456",dict(code=1,s='2',msg=u'中文',sign='33C9065427EECA3490C5642C99165145'))
            True
        """
        if "sign" not in msg:
            return False
        sign = msg['sign']
        params = [msg[k].encode('utf-8') for k in msg if k != 'sign']
        local_sign = make_sign(api_secret, params)
        result = (sign == local_sign)
        if not result:
            logging.error("check_sign failure, sign:%s != local_sign:%s" %(sign,local_sign))

        return result