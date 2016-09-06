＃ 系统配置管理

系统配置主要是对一些系统相关的数据配置，包括数据库，日志配置。
> 注意，系统配置影响系统的运行状态，所有操作必须由超级管理员完成。

#### 基本配置

![untitled6.png](http://qnstatic.toughcloud.net/FkYzr3v-btcDaVtjmbmVUhdWjeaz)

- DEBUG 选项，设置系统的调试开关，用于诊断系统故障
- 时区：目前仅支持中国时区
- 安全密钥：系统用于数据加密的安全密钥，系统安装时修改后一般不需要再修改，若发生系统被攻击，密钥泄露，数据被盗的情况，请重新生成安全密钥，生成安全密钥时会对所有用户密码重新加密。

#### 数据库配置

![untitled7.png](http://qnstatic.toughcloud.net/FnX8cvlf9CJARfpKPcj-IGMTmh7I)

数据库连接池性能调整，一般无需改动。

#### 日志配置

![untitled8.png](http://qnstatic.toughcloud.net/FoeAYhz7AyE7ReQQsCFJSNT_Dz1F)

可支持外部 syslog 服务。
