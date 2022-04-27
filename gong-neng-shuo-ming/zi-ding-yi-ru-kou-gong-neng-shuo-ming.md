# 自定义入口功能说明

XrayR完整支持全部的Xray-core所提供的自定义入口功能，具体启用方式如下：

1. 编写 custom\_inbound.json文件，此配置与Xray 出口配置完全相同，请查看：[https://xtls.github.io/config/inbound.html](https://xtls.github.io/config/inbound.html)获取帮助。
2. 在`config.yml`中配置`InboundConfigPath`为custom\_inbound.json的路径。

### 自定义入口功能示例

```text
[
    {
        "listen": "0.0.0.0",
        "port": 1234,
        "protocol": "socks",
        "settings": {
            "auth": "noauth",
            "accounts": [
                {
                    "user": "my-username",
                    "pass": "my-password"
                }
            ],
            "udp": false,
            "ip": "127.0.0.1",
            "userLevel": 0
        }
    }
]
```

