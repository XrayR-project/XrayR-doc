# 对接Trojan (已废弃)

{% hint style="info" %}
在SSPanel-UIM 2022.12.1 版本之后的新订阅系统中，使用节点地址配置的方法已经被弃用，必须使用 [Custom Config 配置方法](sspanel_custom_config.md)。
{% endhint %}

| 协议 | 支持情况 | 支持协议 |
| :--- | :--- | :--- |
| Trojan | √ | tcp, grpc |

## SSpanel-uim 节点地址格式

```text
域名或IP;port=用户连接端口#监听端口|host=xx
```

## tcp示例

```text
示例：gz.aaa.com;port=443|host=gz.aaa.com
```

## grpc示例

使用trojan+grpc请升级sspanel至[Anankke/SSPanel-Uim@8f68b63](https://github.com/Anankke/SSPanel-Uim/commit/8f68b6360baf9f6624e1158e3cae81d93d1db107)

```text
示例：gz.aaa.com;port=443|host=gz.aaa.com|grpc=1|servicename=mygrpc
```

## 中转示例

用户连接443，XrayR监听12345

```text
示例：gz.aaa.com;port=443#12345|host=hk.aaa.com
```

## 启用xtls **\(此项为实验性功能\)**

sspanel升级到此版本[Anankke/SSPanel-Uim@8f68b63](https://github.com/Anankke/SSPanel-Uim/commit/8f68b6360baf9f6624e1158e3cae81d93d1db107)后支持xtls订阅下发

将任意协议配置中添加`enable_xtls=true`，如果xtls有流控flow，则在最后增加: `flow=flow-vlaue`

```text
示例：gz.aaa.com;port=443|host=gz.aaa.com|enable_xtls=true|flow=xtls-rprx-direct
```

同时在本地设置文件将`EnableXTLS`设为true。 配置文件详见：[配置文件说明](https://github.com/XrayR-project/XrayR-doc/tree/af55d4cc45735ca8d00491aa97f8cbbd97c8faf4/sspanel/config/README.md)

