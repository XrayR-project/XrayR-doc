# 自动申请证书说明

XrayR 支持多种自动申请证书配置。申请到的证书将会放在**配置文件\(config.yml\)目录的`cert`文件夹下**。

以下是自动申请证书的相关配置文件说明。

```yaml
CertConfig:
    CertMode: dns # Option about how to get certificate: none, file, http, dns. Choose "none" will forcedly disable the tls config.
    CertDomain: "node2.test.com" # Domain to cert
    CertFile: /etc/XrayR/cert/node2.test.com.cert # Provided if the CertMode is file
    KeyFile: /etc/XrayR/cert/node2.test.com.key
    Provider: alidns # DNS cert provider, Get the full support list here: https://go-acme.github.io/lego/dns/
    Email: test@me.com
    DNSEnv: # DNS ENV option used by DNS provider
        ALICLOUD_ACCESS_KEY: aaa
        ALICLOUD_SECRET_KEY: bbb
```

| 参数 | 选项 | 说明 |
| :--- | :--- | :--- |
| `CertMode` | `none`,`file`,`http`,`dns` | 获取证书的方式。`file`:手动提供，并制定路径。`http`：通过http申请，需要80端口。`dns`：使用dns模式申请，需要制定相关dns服务商配置。`none`：强制关闭tls设置，交由nginx或者caddy处理。 |
| `CertDomain` | 无 | 申请证书域名 |
| `CertFile` | 无 | 手动指定的证书路径 |
| `KeyFile` | 无 | 手动指定的私钥路径 |
| `Provider` | 无 | dns提供商，所有支持的dns提供商请在此获取：[https://go-acme.github.io/lego/dns/](https://go-acme.github.io/lego/dns/) |
| `DNSEnv` | 无 | 采用DNS申请证书需要的环境变量，请参考上文链接内，自己的dns提供商所需要的参数，填写于此。请注意一行一个，填写时需符合yaml文件格式。 |

