---
description: A Xray backend framework that can easily support many panels.
---

# 关于XrayR

## XrayR

A Xray backend framework that can easily support many panels.

一个基于Xray的后端框架，支持V2ay,Trojan,Shadowsocks协议，极易扩展，支持多面板对接。

项目地址: [https://github.com/XrayR-project](https://github.com/XrayR-project)

## 项目目录

* [XrayR](https://github.com/XrayR-project/XrayR)：XrayR源码以及软件发布。
* [XrayR-release](https://github.com/XrayR-project/XrayR-release)：XrayR一键安装脚本以及Docker。
* [XrayR-doc](https://github.com/XrayR-project/XrayR-doc)：XrayR文档源码。

## 特点

* 永久开源且免费。
* 支持V2ray，Trojan， Shadowsocks多种协议。
* 支持Vless和XTLS等新特性。
* 支持单实例对接多面板、多节点，无需重复启动。
* 支持限制在线IP
* 支持节点端口级别、用户级别限速。
* 配置简单明了。
* 修改配置自动重启实例。
* 方便编译和升级，可以快速更新核心版本， 支持Xray-core新特性。

## 功能介绍

| 功能            | v2ray | trojan | shadowsocks |
| :-------------- | :---- | :----- | :---------- |
| 获取节点信息    | √     | √      | √           |
| 获取用户信息    | √     | √      | √           |
| 用户流量统计    | √     | √      | √           |
| 服务器信息上报  | √     | √      | √           |
| 自动申请tls证书 | √     | √      | √           |
| 自动续签tls证书 | √     | √      | √           |
| 在线人数统计    | √     | √      | √           |
| 在线用户限制    | √     | √      | √           |
| 审计规则        | √     | √      | √           |
| 节点端口限速    | √     | √      | √           |
| 按照用户限速    | √     | √      | √           |
| 自定义DNS       | √     | √      | √           |

## 支持前端

| 前端                                                   | v2ray | trojan | shadowsocks                      |
| :----------------------------------------------------- | :---- | :----- | :------------------------------- |
| sspanel-uim                                            | √     | √      | √ \(单端口多用户和V2ray-Plugin\) |
| v2board                                                | √     | √      | √                                |
| [PMPanel](https://github.com/ByteInternetHK/PMPanel)   | √     | √      | √                                |
| [ProxyPanel](https://github.com/ProxyPanel/ProxyPanel) | √     | √      | √                                |
| [WHMCS (V2RaySocks)](https://v2raysocks.doxtex.com/)   | √     | √      | √                                |

## V2ray支持协议

| 协议      | 支持情况                                                                            |
| :-------- | :---------------------------------------------------------------------------------- |
| VMess     | tcp, tcp+http, tcp+tls, ws, ws+tls, h2c, h2+tls, grpc, grpc+tls                     |
| VMessAEAD | tcp, tcp+http, tcp+tls, ws, ws+tls, h2c, h2+tls, grpc, grpc+tls                     |
| VLess     | tcp, tcp+http, tcp+tls/xtls, ws, ws+tls/xtls, h2c, h2+tls/xtls, grpc, grpc+tls/xtls |

## Trojan支持协议

| 协议      | 支持情况 |
| :-------- | :------- |
| Trojan    | √        |
| Trojan-go | ws, grpc |

## Shadowsocks支持协议

| 协议            | 支持情况 | 加密方法                                                                        |
| :-------------- | :------- | :------------------------------------------------------------------------------ |
| ShadowsocksAEAD | √        | aes-128-gcm, aes-256-gcm, chacha20-ietf-poly1305                                |
| Shadowsocks2022 | √        | 2022-blake3-aes-128-gcm, 2022-blake3-aes-256-gcm, 2022-blake3-chacha20-poly1305 |
