# 对接Shadowsocks - V2Ray-Plugin

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x534F;&#x8BAE;</th>
      <th style="text-align:left">&#x52A0;&#x5BC6;&#x65B9;&#x6CD5;</th>
      <th style="text-align:left">&#x6DF7;&#x6DC6;&#x65B9;&#x6CD5;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Shadowsocks - V2Ray-Plugin</td>
      <td style="text-align:left">aes-128-gcm, aes-256-gcm, chacha20-ietf-poly1305</td>
      <td style="text-align:left">
        <p>simple_obfs_http,simple_obfs_tls,</p>
        <p>ws,ws+tls</p>
      </td>
    </tr>
  </tbody>
</table>

## SSpanel-uim 节点地址格式

```text
IP;监听端口;;(ws或obfs);(tls或不填);path=/xxx|host=xxxx.com|server=xxx.com|outside_port=xxx
```

注意监听端口后面有两个分号

## SSpanel-uim 代码修改

SSpanel-uim关于Shadowsocks - V2Ray-Plugin的代码存在部分问题，需要加以修改才能正确下发订阅。

此方法写于 [SSPanel-Uim@822d3c](https://github.com/Anankke/SSPanel-Uim/commit/822d3cbcb3ad8f7e11874a96f05d73e5b016c164)，不保证后续仍然生效。

### 修改方法

打开src\Models\Node.php文件，找到第420行，将其注释。

修改前：

```text
$return_array['path'] = ($return_array['path'] . '?redirect=' . $user->getMuMd5());
```

修改后：

```text
// $return_array['path'] = ($return_array['path'] . '?redirect=' . $user->getMuMd5());
```

## SSpanel-uim 订阅

SSpanel-uim建议安卓，WIN和Mac使用Clash，IOS使用Shadowrocket获取含有Shadowsocks - V2Ray-Plugin的订阅。

## ws + tls \(Nginx\) 示例（**推荐**）

交由Caddy或者Nginx处理TLS 节点配置和 ws+tls一致，在后端配置`CertMode: none`

同时设置outside\_port为Nginx监听端口，转发到12345为XrayR监听端口。可以在后端配置`ListenIP: 127.0.0.1`监听本地端口。

```text
ip;12345;;ws;tls;path=/xxx|server=域名|host=CDN域名|outside_port=443
```

```text
示例：1.3.5.7;12345;;ws;tls;path=/ss|server=hk.domain.com|host=hk.domain.com|outside_port=443
```

## ws+tls示例

```text
ip;12345;;ws;tls;path=/xxx|host=xxxx.com|server=xxx.com
```

```text
示例：1.3.5.7;12345;;ws;tls;path=/ss|host=hk.domain.com|server=hk.domain.com
```

## ws示例

```text
ip;12345;;ws;;path=/xxx|host=xxxx.com|server=xxx.com
```

```text
示例：1.3.5.7;12345;;ws;;path=/ss|host=hk.domain.com|server=hk.domain.com
```

## simple\_obfs\_http示例

```text
ip;12345;;obfs;http;server=xxx.com
```

```text
示例：1.3.5.7;12345;;obfs;http;server=hk.domain.com
```

## simple\_obfs\_tls示例

```text
ip;12345;;obfs;tls;server=xxx.com
```

```text
示例：1.3.5.7;12345;;obfs;tls;server=hk.domain.com
```

## 中转端口

在任一配置组合后增加`|outside_port=xxx`,此项为用户连接端口。

XrayR没有`inside_port=xx`配置选项，如需监听本地端口，请在配置文件中设置监听ip为`127.0.0.1`。

```text
示例：1.3.5.7;12345;;ws;tls;path=/ss|server=hk.domain.com|host=hk.domain.com|outside_port=8888
```

