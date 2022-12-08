# 设备连接限制功能说明

由于大量面板不再支持远程设备限制指定，现增加本地设备限制参数。

如需启用，可在配置文件中将`DeviceLimit`设为非0值，注意此设置会覆盖远程获取的用户设备限制数目。

配置文件详见：[配置文件说明](../xrayr-pei-zhi-wen-jian-shuo-ming/config.md#mian-ban-dui-jie-pei-zhi)

{% hint style="info" %}
每一个独立IP地址视为一个设备。
{% endhint %}

## SSPanel 全局设备限制

当XrayR版本&gt;=v0.7.1，SSpanel版本&gt;=[2021.9](https://github.com/Anankke/SSPanel-Uim/releases/tag/2021.9)，XrayR将会针对SSPanel启用全局设备限制功能。此时，不同后端结点将会全局限制独立IP连接数量，而非各后端本地限制。

当设备限制为1时，不同结点之间的切换会受到限制，建议至少设置设备数为2。并且由于SSPanel面板限制，IP连接信息可能需要至少2分钟才能传递到全部的后端结点，因此在2分钟内的同时连接将不能被限制。

## 全局设备限制

当XrayR版本>=v0.8.7，可以启用基于redis的全局设备限制功能，可以跨节点支持基于IP的设备限制，兼容所有面板。可在`ControllerConfig` 中配置如下项。

```yaml
GlobalDeviceLimitConfig:
    Enable: false # Enable the global device limit of a user
    RedisAddr: 127.0.0.1:6379 # The redis server address
    RedisPassword: YOUR PASSWORD # Redis password
    RedisDB: 0 # Redis DB
    Timeout: 5 # Timeout for redis request
    Expiry: 60 # Expiry time (second)
```

| 参数          | 说明                                                                            |
| ------------- | ------------------------------------------------------------------------------- |
| Enable        | 是否启用全局设备限制，设备限制数量由面板下发、或由配置文件中的`DeviceLimit`指定 |
| RedisAddr     | redis连接地址，不同节点需要连接到同一redis数据库，来实现全局设备限制            |
| RedisPassword | redis密码                                                                       |
| RedisDB       | redis数据库编号                                                                 |
| Timeout       | 连接redis超时时间，单位：秒                                                     |
| Expiry        | redis中存储的在线用户过期时间，单位：秒                                         |

{% hint style="info" %}
如果同一redis下对接了多个面板结点，建议同一面板下的结点使用同一redis数据库编号，以保证不同面板之间独立限制。
{% endhint %}

{% hint style="info" %}
XrayR全局设备限制需要访问Redis服务器，用户第一次连接时会引入额外的延迟。我们实现了缓存机制，只会在用户第一次访问结点时和redis通讯，后续访问会直接从缓存中读取，因此不会引入额外的延迟。
{% endhint %}