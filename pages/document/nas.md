# 接入设备管理

接入设备主要是指充当PPPoE，PPTP，L2TP 接入服务器的路由器等设备，系统支持多设备接入管理，接入设备信息必须在系统中登记才能和计费系统进行通信。

系统支持标准的Radius协议接入，通常大多数路由器接入设备可以以标准类型配置。但是对于很多厂家的接入设备，在标准协议下并不能工作的很完美，比如MAC地址，VLAN往往以各自的私有协议封装，计费系统为了准确的处理这些信息，必须对这些接入设备进行类型标识，并在消息处理时进行适配处理。

接入设备需要绑定区域，每个接入设备可以绑定一个或多个区域，只有绑定区域，该区域下的用户才能通过这个接入设备认证上网。

![](http://qnstatic.toughcloud.net/toughee-nas.png)

## 属性说明

- 接入设备地址：接入设备的网络 IP 地址，这个地址在系统中是唯一的。
- 接入设备标识：对于没有固定 IP 的路由器接入设备，可以通过 接入设备标识 实现动态鉴权。
- 接入设备名称：接入设备名称描述。
- 共享密钥：接入设备与 Radius 系统采用的消息签名秘钥，两边配置必须一致，否则会造成用户密码不匹配的错误，或者消息被丢弃。
- 接入设备的类型：设置接入设备的厂家标识，设置后，系统会根据厂商标识对该设备的消息进行消息适配处理，解析私有协议属性，下发私有协议属性。
- 授权端口：接入设备提供的一个授权服务监听端口（默认3799），通过这个端口，计费系统可以主动下发授权消息，比如强制用户下线，动态下发限速。
- 无线控制器端口：如果接入设备具备无线控制器功能，并同时充当无线控制器，则需要填写无线控制器端口，通常为2000
- 时区类型：默认采用北京时间，在某些国外厂商提供的路由器设备中可能需要设置。（该属性目前为保留属性）
- 绑定区域：绑定允许接入认证的区域，可多选。