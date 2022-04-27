# 自定义DNS说明

XrayR支持为不同节点设置不同的DNS策略，具体方法如下：

1. 编写dns.json文件，此配置与Xray DNS配置完全相同，请查看：[https://xtls.github.io/config/dns.html](https://xtls.github.io/config/dns.html) 获取帮助。
2. 在`config.yml`中配置`DnsConfigPath`为dns.json的路径。
3. 在所需要启用自定义DNS的节点中，将`EnableDNS`设为true。如设为false或者不填则是使用本机DNS。
4. 如果要启用geoip相关配置，请确保`geoip.dat`和`geosite.dat`处于和`config.yml`同一目录。

## DNS解锁样例配置

```javascript
{
    "servers": [
      "8.8.8.8", 
      {
        "address": "1.1.2.2", // 购买的 DNS 解锁提供的 IP
        "port": 53,
        "domains": [
          "geosite:netflix" 
        ]
      }
    ]
  }
```

## 设置IPV6优先

1. 请先确保主机有ipv6地址，如无，请考虑使用[warp](https://github.com/P3TERX/warp.sh)获取ipv6。
2. 在所需要设置IPV6优先的节点中，将`EnableDNS`设为true。
3. 在所需要设置IPV6优先的节点中，将`SendIP`设为`"::"`。
4. 在所需要设置IPV6优先的节点中，将`DNSType`设为`UseIP`。

至此，XrayR将会优先使用目标网站的ipv6地址进行访问，不会影响默认ipv4站点的访问。~~可以用于解锁Netflix等需求~~

## 设置IPV4优先

1. 在所需要设置IPV4优先的节点中，将`EnableDNS`设为true。
2. 在所需要设置IPV4优先的节点中，将`SendIP`设为`"0.0.0.0"`。
3. 在所需要设置IPV4优先的节点中，将`DNSType`设为`UseIP`。

