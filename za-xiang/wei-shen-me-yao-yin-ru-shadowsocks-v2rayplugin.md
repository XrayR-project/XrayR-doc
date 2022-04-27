# 为什么要引入Shadowsocks - V2Ray-Plugin

## Update on 2021/07/04

我错怪Trojan了，通过后端禁用TLS，配合Nginx的Stream模块也可以实现，Nginx代理处理Trojan的TLS，达到隐藏TLS握手信息的效果，同时可以fallback到http1.1的站点达到比SS更高的性能水平。

## 原文

很多人觉得有Shadowsocks单端口就够了呀，为啥要引入Shadowsocks - V2Ray-Plugin呢？

首先针对近日来的国际互联网通讯情况，我个人分析认为，在特殊时期，会针对go的TLS握手行为进行匹配，并加以阻断。再加上现有大部分的软件（如V2ray-core,Xray-core）都是以go实现的，并采用go的库进行TLS处理。因此在特殊时期，可以对go的TLS握手行为可以进行识别，从而导致端口精准阻断。所以大部分直接采用go进行tls处理的协议，比如Trojan，在近日遭受了严重阻断。同样，使用Caddy反代进行伪装的行为也遭受了阻断。

虽然针对go的TLS库进行识别的行为有极大的误报率（封杀正常的Caddy反代的网站），但是在特殊时期已经被证实是可能实行的了。因我认为，需要隐藏go的TLS握手行为，从而达到更高的隐蔽性。为此，我认为采用C语言编写的NGINX是目前最好的选择。现有情况也表明：Vmess+ws+tls+nginx在目前存活性最好。

Vmess+ws+tls+nginx虽然已经成功隐藏了go的TLS握手信息，但是Vmess协议由于其本身设计，会产生大量的内存占用。同时其基于时间的验证设计，增加了其使用难度。~~而Trojan暂时又不支持使用其他软件进行TLS处理~~。此时Shadowsocks - V2Ray-Plugin成为了最好的选择。

Shadowsocks - V2Ray-Plugin，首先是基于Shadowsocks的。得益于Shadowsocks协议设计，使得Shadowsocks拥有比Vmess更快的速度和不依赖时间的验证。同时V2Ray-Plugin给予Shadowsocks进行websocket混淆和TLS加密的能力。极大增强了Shadowsocks的安全性，使得流量可以直接在公网传输，不再需要隧道。同时可以把TLS交由NGINX处理，隐藏go的相关特征，防止被阻断端口。

综上所述，为了隐藏特征，我强烈建议采用nginx+ws+tls+everything的做法，在目前情况下，nginx+ws+tls+ss的配置会优于nginx+ws+tls+vmess。同时为了长远考虑，我建议所有的协议实现软件采用C语言提供的TLS库进行TLS相关处理，或者参考Shadowsocks分离出插件层，方便使用第三方软件如nginx进行TLS处理。

