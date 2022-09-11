# 使用docker安装

镜像地址：https://github.com/XrayR-project/XrayR/pkgs/container/xrayr
## docker image tag

`master`: 与项目最新提交保持一致。

`latest`: 最新release版本。

`v*`: release版本号。

## 安装 Docker

### Centos

```bash
yum install -y yum-utils
yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
yum install docker-ce docker-ce-cli containerd.io -y
systemctl start docker
systemctl enable docker
```

### Debian / Ubuntu

```bash
sudo apt-get update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common -y
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
sudo apt-get install docker-ce docker-ce-cli containerd.io -y
systemctl start docker
systemctl enable docker
```

## 安装Docker-compose

```bash
curl -fsSL https://get.docker.com | bash -s docker
curl -L "https://github.com/docker/compose/releases/download/1.26.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```

## Docker-compose 安装XrayR \(推荐\)

1. `git clone https://github.com/XrayR-project/XrayR-release`
2. `cd XrayR-release`
3. 编辑配置文件：`config.yml`，详见：[配置文件说明](../../xrayr-pei-zhi-wen-jian-shuo-ming/config.md)
4. 启动docker：`docker-compose up -d`

## Docker run 安装XrayR

请注意指定`config.yml`目录。

```bash
docker pull ghcr.io/xrayr-project/xrayr:latest && docker run --restart=always --name xrayr -d -v ${PATH_TO_CONFIG}/config.yml:/etc/XrayR/config.yml --network=host ghcr.io/xrayr-project/xrayr:latest
```

## 更新XrayR

docker-compose仅需两条简单通用的命令即可实现更新、删除容器并重启。更新软件后`config.yml`不会被更新覆盖。

注意在 docker-compose.yml 所在的目录下执行：

```bash
docker-compose pull
docker-compose up -d
```

