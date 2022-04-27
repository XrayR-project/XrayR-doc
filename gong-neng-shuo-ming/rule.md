# 审计功能说明

1. 请在前端审计规则处填写任意正则表达式，如 `baidu.com`将屏蔽所有baidu的域名，`(.+\.|^)(360|so)\.(cn|com)`将屏蔽360相关网站。
2. 支持输入ip地址屏蔽ip，如`127.0.0.1`。
3. BT协议屏蔽请查看：[自定义路由功能说明](zi-ding-yi-lu-you-gong-neng-shuo-ming.md)

## 本地审计规则设置

针对不支持远程设置审计规则的面板：如V2board，可以在本地配置文件`RuleListPath`设置本地规则文件路径。规则文件不需要定义文件类型，每条**正则规则**一行，默认本地规则ID标号为-1。

配置文件详见：[配置文件说明](../xrayr-pei-zhi-wen-jian-shuo-ming/config.md#mian-ban-dui-jie-pei-zhi)

**本地规则文件示例**

请保证每行只是一个单纯的正则规则，不要包含任何其无关他字符串。

```text
(.+\.|^)(360|so)\.(cn|com)
baidu.com
google.com
127.0.0.1
```

