# 基本对接配置

1. 在`config.yml`中配置`PanelType: "SSpanel"`。

配置文件详见：[配置文件说明](../../xrayr-pei-zhi-wen-jian-shuo-ming/config.md)

1. 对于sspanel >= 2021.11的版本中自动启用Custom_config的配置方法，请查看[SSPanel Custom Config](sspanel_custom_config.md)，正确配置结点信息。关于订阅相关信息，请查看SSPanel相关文档：https://wiki.sspanel.org/#/universal-subscription。
2. 如果不想使用custom config，请在`ApiConfig`中将`DisableCustomConfig`设为`true`。同时参照[shadowsocks](shadowsocks.md),[v2ray](v2ray.md)和[trojan](trojan.md)的配置方法，在sspanel地址栏中配置结点信息。
