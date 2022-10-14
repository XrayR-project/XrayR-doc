# 限速功能说明

1. 节点限速：请在SSpanel的节点限速处填写，单位Mbps。
2. 用户限速：请在SSpanel的用户设置处填写，单位Mbps。
3. 限速值设为0，则为不限速。

## 本地节点限速设置

针对不支持远程设置限速的面板：如V2board，可以在本地配置文件`SpeedLimit`设置限速。注意此设置会覆盖远程获取的节点级别限速。

{% hint style="info" %}
节点限速：所有连接到该节点的用户限速值都会采用`SpeedLimit`中的设置值**（不是端口限速）**
{% endhint %}

配置文件详见：[配置文件说明](../xrayr-pei-zhi-wen-jian-shuo-ming/config.md#mian-ban-dui-jie-pei-zhi)

## 动态限速功能

XrayR支持动态限速功能，可以根据用户的使用流量调整限速值。在`ControllerConfig` 中配置如下项。

{% hint style="info" %}
为保证能及时调整长连接的限速（如长时间下载），请确保默认限速值大于0。可在用户、节点、本地任意位置配置默认大于0的限速值，优先级为本地>节点>用户。如果默认限速值为0，则用户的动态限速只有在下次建立连接时才会生效。
{% endhint %}


```yaml
AutoSpeedLimitConfig:
    Limit: 0 # Warned speed. Set to 0 to disable AutoSpeedLimit (mbps)
    WarnTimes: 0 # After (WarnTimes) consecutive warnings, the user will be limited. Set to 0 to punish overspeed user immediately.
    LimitSpeed: 0 # The speedlimit of a limited user (unit: mbps)
    LimitDuration: 0 # How many minutes will the limiting last (unit: minute)
```
| 参数          | 说明                                                                        |
| ------------- | --------------------------------------------------------------------------- |
| Limit         | 警告速度。设置为0以禁用自动限速功能。单位：Mbps。                           |
| WarnTimes     | 警告次数。连续警告次数达到该值后，用户将被限速。设置为0以立即惩罚超速用户。 |
| LimitSpeed    | 限速值。单位：Mbps。                                                        |
| LimitDuration | 限速时长。单位：分钟。                                                      |