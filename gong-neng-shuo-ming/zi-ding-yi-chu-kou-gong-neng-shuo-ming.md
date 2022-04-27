# 自定义出口功能说明

XrayR完整支持全部的Xray-core所提供的自定义出口功能，具体启用方式如下：

1. 编写 custom\_outbound.json文件，此配置与Xray 出口配置完全相同，请查看：[https://xtls.github.io/config/outbound.html](https://xtls.github.io/config/outbound.html)获取帮助。
2. 在`config.yml`中配置`OutboundConfigPath`为custom\_outbound.json的路径。

### 自定义出口功能示例

```text
[
    {
        "tag": "IPv4_out",
        "protocol": "freedom"
    },
    {
        "tag": "IPv6_out",
        "protocol": "freedom",
        "settings": {
            "domainStrategy": "UseIPv6"
        }
    },
    {
        "protocol": "blackhole",
        "tag": "block"
    }
]
```

