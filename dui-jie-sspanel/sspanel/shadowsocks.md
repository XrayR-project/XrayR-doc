# 对接Shadowsocks (已废弃)

{% hint style="info" %}
在SSPanel-UIM 2022.12.1 版本之后的新订阅系统中，使用节点地址配置的方法已经被弃用，必须使用 [Custom Config 配置方法](sspanel_custom_config.md)。
{% endhint %}

| 协议 | 支持情况 | 加密方法 |
| :--- | :--- | :--- |
| ShadowsocksAEAD | √ | aes-128-gcm, aes-256-gcm, chacha20-ietf-poly1305 |

## SSpanel-uim 节点地址格式

* 请注意，节点类型请选择：`Shadowsocks`
* 单端口多用户承载用户加密方式请选择：`aes-128-gcm`, `aes-256-gcm`, `chacha20-ietf-poly1305`三者之一。
* XrayR目前只支持一个单端口多用户承载用户，有多个承载用户时只使用第一个。

  ```text
  域名或IP;port=监听端口#连接端口;server=xx
  ```

## Shadowsocks 示例

```text
示例：gz.aaa.com;port=80#1234;server=gz.aaa.com
```

