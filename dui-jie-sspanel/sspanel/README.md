# 基本对接配置

1. 在`config.yml`中配置`PanelType: "SSpanel"`。

配置文件详见：[配置文件说明](../../xrayr-pei-zhi-wen-jian-shuo-ming/config.md)

1. 对于SSPanel-UIM >= 2021.11的版本中自动启用Custom_config的配置方法，请查看[SSPanel Custom Config](sspanel_custom_config.md)，正确配置节点信息。或者查看SSPanel相关文档：[https://wiki.sspanel.org/#/custom-config](https://wiki.sspanel.org/#/custom-config)。
2. 如果不想使用 Custom Config，请在`ApiConfig`中将`DisableCustomConfig`设为`true`。同时参照[shadowsocks](shadowsocks.md),[v2ray](v2ray.md)和[trojan](trojan.md)的配置方法，在 SSPanel 地址栏中配置节点信息。

{% hint style="info" %}
在SSPanel-UIM 2022.12.1 版本之后的新订阅系统中，使用节点地址配置的方法已经被弃用，必须使用 Custom Config 配置方法。
{% endhint %}