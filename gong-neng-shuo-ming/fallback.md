# Fallback 功能说明

> fallback 为 Xray 提供了高强度的防主动探测性, 并且具有独创的首包回落机制.
>
> fallback 也可以将不同类型的流量根据 path 进行分流, 从而实现一个端口, 多种服务共享.
>
> 目前您可以在使用 VLESS 或者 trojan 协议时, 通过配置 fallbacks 来使用回落这一特性, 并且创造出非常丰富的组合玩法.
>
> ---[https://xtls.github.io/config/features/fallback.html](https://xtls.github.io/config/features/fallback.html)

## 启用Fallback功能

设置`EnableFallback`为`true`，并配置`FallBackConfigs`

```yaml
ControllerConfig:
  EnableFallback: true # Only support for Trojan and Vless
  FallBackConfigs:  # Support multiple fallbacks
    -
      SNI: # TLS SNI(Server Name Indication), Empty for any
      Alpn: # Alpn, Empty for any
      Path: # HTTP PATH, Empty for any
      Dest: 80 # Required, Destination of fallback, check https://xtls.github.io/config/fallback/ for details.
      ProxyProtocolVer: 0 # Send PROXY protocol version, 0 for dsable
```

## 配置Fallback

XrayR遵循Xray设计思路，支持一个节点多个Fallback设置，因此`FallBackConfigs`为一个数组，每个子元素示例如下：

```yaml
-
  SNI: # TLS SNI(Server Name Indication), Empty for any
  Alpn: # Alpn, Empty for any
  Path: # HTTP PATH, Empty for any
  Dest: 80 # Required, Destination of fallback, check https://xtls.github.io/config/fallback/ for details.
  ProxyProtocolVer: 0 # Send PROXY protocol version, 0 for dsable
```

### SNI: string

尝试匹配 TLS SNI\(Server Name Indication\)，空为任意，默认为 ""

### Alpn: string
尝试匹配 TLS ALPN 协商结果，空为任意，默认为 ""

有需要时，VLESS 才会尝试读取 TLS ALPN 协商结果，若成功，输出 info `realAlpn =` 到日志。
用途：解决了 Nginx 的 h2c 服务不能同时兼容 http/1.1 的问题，Nginx 需要写两行 listen，分别用于 1.1 和 h2c。
注意：fallbacks alpn 存在 `"h2"` 时，[Inbound TLS](../transport.md#tlsobject) 需设置 `"alpn":["h2","http/1.1"]`，以支持 h2 访问。

{% hint style="info" %}
Fallback 内设置的 `alpn` 是匹配实际协商出的 ALPN，而 Inbound TLS 设置的 `alpn` 是握手时可选的 ALPN 列表，两者含义不同。
{% endhint %}

### Path: string

尝试匹配首包 HTTP PATH，空为任意，默认为空，非空则必须以 "/" 开头，不支持 h2c。

智能：有需要时，VLESS 才会尝试看一眼 PATH（不超过 55 个字节；最快算法，并不完整解析 HTTP），若成功，输出 info realPath = 到日志。 用途：分流其它 inbound 的 WebSocket 流量或 HTTP 伪装流量，没有多余处理、纯粹转发流量，实测比 Nginx 反代更强。

注意：fallbacks 所在入站本身必须是 TCP+TLS，这是分流至其它 WS 入站用的，被分流的入站则无需配置 TLS。

### Dest: string\|number

决定 TLS 解密后 TCP 流量的去向，目前支持两类地址：（该项必填，否则无法启动）

1. TCP，格式为 "addr:port"，其中 addr 支持 IPv4、域名、IPv6，若填写域名，也将直接发起 TCP 连接（而不走内置的 DNS）。
2. Unix domain socket，格式为绝对路径，形如 "/dev/shm/domain.socket"，可在开头加 "@" 代表 abstract，"@@" 则代表带 padding 的 abstract。

   若只填 port，数字或字符串均可，形如 80、"80"，通常指向一个明文 http 服务（addr 会被补为 "127.0.0.1"）。

### ProxyProtocolVer: number

发送 PROXY protocol，专用于传递请求的真实来源 IP 和端口，填版本 1 或 2，默认为 0，即不发送。若有需要建议填 1。

目前填 1 或 2，功能完全相同，只是结构不同，且前者可打印，后者为二进制。Xray 的 TCP 和 WS 入站均已支持接收 PROXY protocol。

> TIP
>
> 若你正在 配置 Nginx 接收 PROXY protocol，除了设置 proxy\_protocol 外，还需设置 set\_real\_ip\_from，否则可能会出问题。

## Fallback 示例

XrayR设置

```text
EnableFallback: true
FallBackConfigs:  # Support multiple fallbacks
  -
    SNI:
    Alpn:
    Path:
    Dest: 8080
    ProxyProtocolVer: 0
```

Nginx设置

```text
server {  
    listen 8080 http2;
  root /var/www/public; # 改成你自己的路径
  index index.php index.html;
  server_name www.test.com; # 改成你自己的域名

  location / {
    try_files $uri /index.php$is_args$args;
  }

  location ~ \.php$ {
    include snippets/fastcgi-php.conf;
    fastcgi_pass 127.0.0.1:9000; # unix:/run/php/php-fpm.sock;
  }
}
```

## 参考

[Xray Fallback](https://xtls.github.io/config/features/fallback.html)

