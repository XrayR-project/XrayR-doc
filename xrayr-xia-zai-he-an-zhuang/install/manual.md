# 手动安装

## 下载并使用

1. 在此处，根据自身系统选择合适的版本：[Release](https://github.com/XrayR-project/XrayR/releases)
2. 解压压缩包，之后运行：`./XrayR -config config.yml`

## 编译并使用

1. 大于 go 1.19
2. 依次运行

   ```bash
   git clone https://github.com/XrayR-project/XrayR
   cd XrayR/main
   go mod tidy
   go build -o XrayR -ldflags "-s -w"
   ./XrayR -config config.yml
   ```

配置文件详见：[配置文件说明](../../xrayr-pei-zhi-wen-jian-shuo-ming/config.md)

