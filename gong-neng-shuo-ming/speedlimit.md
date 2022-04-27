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

