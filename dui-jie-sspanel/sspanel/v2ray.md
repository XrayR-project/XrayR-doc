# 对接V2ray (已废弃)

{% hint style="info" %}
在SSPanel-UIM 2022.12.1 版本之后的新订阅系统中，使用节点地址配置的方法已经被弃用，必须使用 [Custom Config 配置方法](sspanel_custom_config.md)。
{% endhint %}

| 协议 | 支持情况 |
| :--- | :--- |
| VMess | tcp, tcp+http, tcp+tls, ws, ws+tls, h2c, h2+tls, grpc, grpc+tls |
| VMessAEAD | tcp, tcp+http, tcp+tls, ws, ws+tls, h2c, h2+tls, grpc, grpc+tls |
| VLess | tcp, tcp+http, tcp+tls/xtls, ws, ws+tls/xtls, h2c, h2+tls/xtls, grpc, grpc+tls/xtls |

## SSpanel-uim 节点地址格式

```text
IP;监听端口;alterId;(tcp或ws);(tls或不填);path=/xxx|host=xxxx.com|server=xxx.com|outside_port=xxx
```

alterId设为0，则自动启用VMessAEAD。

{% hint style="info" %}
注意：VMESS AEAD 将在 2022 年 1 月 1 日强制启用 请注意更新服务端配置，设置alterId = 0
{% endhint %}

## tcp示例

```text
ip;12345;0;tcp;;server=域名
```

```text
示例：1.3.5.7;12345;0;tcp;;server=hk.domain.com
```

## tcp+http示例


```text
ip;12345;0;tcp;;server=域名;headerType=http
```

```text
示例：1.3.5.7;12345;0;tcp;;server=hk.domain.com;headertype=http
```

## tcp + tls 示例

```text
ip;12345;0;tcp;tls;server=域名|host=域名
```

```text
示例：1.3.5.7;12345;0;tcp;tls;server=hk.domain.com|host=hk.domain.com
```

## ws示例

```text
ip;80;0;ws;;path=/xxx|server=域名|host=CDN域名
```

```text
示例：1.3.5.7;80;0;ws;;path=/v2ray|server=hk.domain.com|host=hk.domain.com
```

## ws + tls 示例

```text
ip;443;0;ws;tls;path=/xxx|server=域名|host=CDN域名
```

```text
示例：1.3.5.7;443;0;ws;tls;path=/v2ray|server=hk.domain.com|host=hk.domain.com
```

## ws + tls \(Caddy/Nginx\) 示例

交由Caddy或者Nginx处理TLS 节点配置和 ws+tls一致，在后端配置`CertMode: none`

同时设置outside\_port为Caddy/Nginx监听端口，转发到12345为XrayR监听端口。可以在后端配置`ListenIP: 127.0.0.1`监听本地端口。

```text
ip;12345;0;tls;ws;path=/xxx|server=域名|host=CDN域名|outside_port=443
```

```text
示例：1.3.5.7;12345;0;ws;tls;path=/v2ray|server=hk.domain.com|host=hk.domain.com示例：1.3.5.7;12345;2;ws;tls;path=/v2ray|server=hk.domain.com|host=hk.domain.com
```

## grpc+tls示例

使用grpc建议升级sspanel至[Anankke/SSPanel-Uim@8f68b63](https://github.com/Anankke/SSPanel-Uim/commit/8f68b6360baf9f6624e1158e3cae81d93d1db107)

```text
ip;12345;0;grpc;tls;host=域名|server=域名|servicename=任意字符串
```

```text
示例：1.3.5.7;12345;0;grpc;tls;host=hk.domain.com|server=hk.domain.com|servicename=mygrpc
```

## 中转端口

在任一配置组\|合后增加`|outside_port=xxx`,此项为用户连接端口。

XrayR没有`inside_port=xx`配置选项，如需监听本地端口，请在配置文件中设置监听ip为`127.0.0.1`。

```text
示例：1.3.5.7;80;0;ws;;path=/v2ray|server=hk.domain.com|host=hk.domain.com|outside_port=12345
```

## 启用Vless

此项为实验性功能，请确保您使用的面板已经支持下发vless订阅，否则请手动配置客户端。

sspanel升级到此版本[Anankke/SSPanel-Uim@8f68b63](https://github.com/Anankke/SSPanel-Uim/commit/8f68b6360baf9f6624e1158e3cae81d93d1db107)后支持vless订阅下发

在任意协议配置后增加`enable_vless=true`

```text
示例：hk.domain.com;12345;0;tcp;(tls或xtls);server=hk.domain.com|enable_vless=true
```

同时在本地设置文件将`EnableVless`设为true。 配置文件详见：[配置文件说明](../../xrayr-pei-zhi-wen-jian-shuo-ming/config.md#mian-ban-dui-jie-pei-zhi)

请开启vless同时务必使用tls或者xtls。

## 启用xtls

此项为实验性功能，请确保您使用的面板已经支持下发带有xtls的订阅，否则请手动配置客户端。

sspanel升级到此版本[Anankke/SSPanel-Uim@8f68b63](https://github.com/Anankke/SSPanel-Uim/commit/8f68b6360baf9f6624e1158e3cae81d93d1db107)后支持xtls订阅下发

将任意协议配置中的`tls`替换成`xtls`，如果xtls有流控flow，则在最后增加: `|flow=flow-vlaue`

```text
示例：hk.domain.com;443;0;tcp;xtls;server=hk.domain.com|host=hk.domain.com|enable_vless=true|flow=xtls-rprx-direct
```

同时在本地设置文件将`EnableXTLS`设为true。 配置文件详见：[配置文件说明](../../xrayr-pei-zhi-wen-jian-shuo-ming/config.md#mian-ban-dui-jie-pei-zhi)

