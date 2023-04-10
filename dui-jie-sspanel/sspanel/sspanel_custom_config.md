# 对接SSPanel Custom Config

对于SSPanel-UIM >= 2021.11的版本中自动启用Custom_config的配置方法，请查看以下配置，正确配置节点信息。或者查看SSPanel相关文档：[https://wiki.sspanel.org/#/custom-config](https://wiki.sspanel.org/#/custom-config)。

# Shadowsocks
```json
{
    "offset_port_user": "12345", //前端/订阅中下发的端口
    "offset_port_node": "12345", //节点服务器下发的端口
    "server_user": "hk.domain.com", //前端/订阅中下发的服务器地址
    "mu_encryption": "chacha20-ietf-poly1305" // `aes-128-gcm`, `aes-256-gcm`, `chacha20-ietf-poly1305`三者之一
}

```

# V2ray

alterId设为0，则自动启用VMessAEAD。

{% hint style="info" %} 注意：VMESS AEAD 将在 2022 年 1 月 1 日强制启用 请注意更新服务端配置，设置alterId = 0 {% endhint %}

## tcp示例

``` json
{
	"offset_port_node": "12345",
	"server_sub": "hk.domain.com",
	"alter_id": "0",
	"network": "tcp",
	"security": "none"
}
```

## tcp+http示例

```json
{
	"offset_port_node": "12345",
	"server_sub": "hk.domain.com",
	"alter_id": "0",
	"network": "tcp",
	"security": "none",
	"header": {
        "type": "http",
        "request": {
            "path": ["/"],
  			"headers": {
    			"Host": ["www.baidu.com"]
            }
        },
        "response": {}
    }
}
```

## tcp+tls示例

```json
{
	"offset_port_node": "443",
	"server_sub": "hk.domain.com",
	"host": "hk.domain.com",
	"alter_id": "0",
	"network": "tcp",
	"security": "tls"
}
```

## ws示例

```json
{
	"offset_port_node": "80",
	"server_sub": "hk.domain.com",
	"host": "hk.domain.com",
	"alter_id": "0",
	"network": "ws",
	"security": "none",
	"path": "/v2ray"
}
```

## ws+tls示例

```json
{
	"offset_port_node": "443",
	"server_sub": "hk.domain.com",
	"host": "hk.domain.com",
	"alter_id": "0",
	"network": "ws",
	"security": "tls",
	"path": "/v2ray"
}
```

## grpc+tls示例

```json
{
	"offset_port_node": "443",
	"server_sub": "hk.domain.com",
	"host": "hk.domain.com",
	"alter_id": "0",
	"network": "grpc",
	"security": "tls",
	"servicename": "some_name"
}
```

## 中转端口示例
在任一配置中设置`offset_port_user`为用户连接端口

``` json
{
	"offset_port_user": "8888",
	"offset_port_node": "12345",
	"server_sub": "hk.domain.com",
	"alter_id": "0",
	"network": "tcp",
	"security": "none"
}
```

此时用户连接端口为8888，节点监听端口为12345

## 启用vless
在任一配置中设置 `enable_vless: "1"` 为用户连接端口

``` json
{
	"offset_port_node": "443",
	"server_sub": "hk.domain.com",
	"host": "hk.domain.com",
	"alter_id": "0",
	"network": "tcp",
	"security": "tls",
	"enable_vless": "1"
}
```
请开启vless同时务必使用tls或者xtls。

## 启用xtls
在任一配置中设置`security: xtls`。

``` json
{
	"offset_port_node": "443",
	"server_sub": "hk.domain.com",
	"host": "hk.domain.com",
	"alter_id": "0",
	"network": "tcp",
	"security": "xtls",
	"enable_vless": "1"
}
```

# Trojan

## tcp示例

``` json
{
	"offset_port_node": "443",
	"server_sub": "hk.domain.com",
	"host": "hk.domain.com"
}
```

## grpc示例

``` json
{
	"offset_port_node": "443",
	"server_sub": "hk.domain.com",
	"host": "hk.domain.com",
	"grpc": "1",
	"servicename": "some_name"
}
```

## Trojan-go ws示例

``` json
{
	"offset_port_node": "443",
	"server_sub": "hk.domain.com",
	"host": "hk.domain.com",
	"network": "ws",
	"path": "/path"
}
```

## 中转示例
在任一配置中设置`offset_port_user`为用户连接端口
``` json
{
	"offset_port_user": "443",
	"offset_port_node": "12345",
	"server_sub": "hk.domain.com",
	"host": "hk.domain.com"
}
```
此时用户连接443，节点监听12345

## 启用xtls

在任一配置中设置`enable_xtls: 1`。

``` json
{
	"offset_port_node": "443",
	"server_sub": "hk.domain.com",
	"host": "hk.domain.com",
	"enable_xtls": "1"
}
```
