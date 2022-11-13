# 内存优化相关

## 链接控制优化

通过自定义`ConnectionConfig`连接释放的[相关配置](../xrayr-pei-zhi-wen-jian-shuo-ming/config.md#lian-jie-kong-zhi)，可以一定程度优化内存占用

1. 减少`ConnIdle`有可能可以优化高连接数量时的内存占用，但是会导致用户连接延时变高。
2. 在 HTTP 浏览的场景中，可以将 `UplinkOnly` 和 `DownlinkOnly` 设为 0，以提高连接关闭的效率，减少内存占用。
3. 减少`BufferSize`可以优化内存占用，但是可能会导致CPU占用上升。

