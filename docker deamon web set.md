# step 0: 确认不使用docker desktop
```wsl
which docker
```
输出: `/usr/bin/docker`

# step 1: 检查 WSL 网络是否正常
```wsl
cat /etc/resolv.conf

curl -I https://www.google.com

curl -I https://registry-1.docker.io
```

# step 2: 查看 WSL 代理端口

检查代理端口：
```wsl
env | grep -i proxy

linux system:
需要去v2rayA：localhost检查端口
```
输出：`HTTPS_PROXY=http://...`

测试：
```wsl
curl -x http://127.0.0.1:PORT -I https://registry-1.docker.io
```

# step 3: 确认 Docker daemon 当前没有代理

```wsl
docker info | grep -i proxy
```
如果没有输出,说明无代理
# step 4: 配置 Docker daemon 代理

```wsl
sudo mkdir -p /etc/systemd/system/docker.service.d
sudo nano /etc/systemd/system/docker.service.d/http-proxy.conf
```
写入：
```nano
[Service]
Environment="HTTP_PROXY=http://127.0.0.1:10808"
Environment="HTTPS_PROXY=http://127.0.0.1:10808"
Environment="NO_PROXY=localhost,127.0.0.1"
```
保存： 

Ctrl + O\
Enter\
Ctrl + X

# step 5： 重新加载 Docker 服务

```wsl
ps -p 1 -o comm=
```
输出：`systemd`

```wsl
sudo systemctl daemon-reload
sudo systemctl restart docker
```


