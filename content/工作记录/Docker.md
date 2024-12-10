---
title: "Docker"
date: 2024-12-03
draft: false
---
# 一. Docker APT安装

1. 更新 APT 包索引
首先，确保系统的软件包索引是最新的：

```bash
sudo apt update
```

2. 安装依赖包
Docker 需要一些依赖包来确保能够通过 HTTPS 安全地下载软件包。运行以下命令安装这些依赖：

```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

3. 添加 Docker 的官方 GPG 密钥
Docker 使用 GPG 密钥来确保安装包的安全性。运行以下命令添加 Docker 的官方 GPG 密钥：

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

4. 添加 Docker APT 仓库
将 Docker 的官方 APT 仓库添加到系统中：

```bash
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

这将确保你从 Docker 的官方仓库安装软件包。

5. 更新 APT 包索引
添加完 Docker 仓库后，再次更新包索引以确保 APT 获取到最新的 Docker 包：

```bash
sudo apt update
```

6. 安装 Docker
现在，你可以安装 Docker 社区版（docker-ce）了：

```bash
sudo apt install docker-ce
```

7. 启动 Docker 服务并设置开机自启
安装完成后，启动 Docker 服务并设置它在系统启动时自动启动：

```bash
sudo systemctl start docker
sudo systemctl enable docker
```

8. 验证 Docker 是否安装成功
安装完成后，验证 Docker 是否安装成功，可以查看 Docker 版本：

```bash
docker --version
```

如果安装成功，你会看到类似如下的输出：

```bash
Docker version 20.10.x, build xxxx
```

9. 检查 Docker 服务状态

你还可以检查 Docker 服务的状态，确保它正在运行：

```bash
sudo systemctl status docker
```

如果 Docker 正常运行，输出将类似于：

```yaml
● docker.service - Docker Application Container Engine
     Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
     Active: active (running) since Mon 2024-12-03 10:52:03 UTC; 3h 27min ago
```

10. 运行 Docker 测试容器
验证 Docker 是否能够正常工作，运行一个简单的测试容器：

```bash
sudo docker run hello-world
```

如果 Docker 工作正常，你将看到以下消息：

```bash
Hello from Docker!
This message shows that your installation appears to be working correctly.
```

11. （可选）将当前用户添加到 Docker 组
默认情况下，使用 Docker 命令需要加 sudo。如果你希望不使用 sudo 来运行 Docker，可以将当前用户添加到 Docker 组：

```bash
sudo usermod -aG docker $USER
```

然后，你需要注销并重新登录，或者运行以下命令以立即生效：

```bash
newgrp docker
```

12. 检查 Docker 版本和信息
如果你已经将用户添加到 Docker 组，可以直接运行以下命令来验证 Docker 信息：

```bash
docker info
```

这将显示有关 Docker 系统的详细信息，包括存储驱动、网络设置等。

# 二. 镜像加速

因为墙的原因，在docker pull镜像的时候会很慢，或者说根本pull不下来，我ping的结果是丢包率100%。

![ping](/images/work-record/ping.png "丢包率")

## 方法1. 科学上网

挂梯子+开tun模式。

## 方法2. 使用国内docker的镜像

(1) 创建或修改 /etc/docker/daemon.json：

```bash

sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
    "registry-mirrors": [
        "https://dockerproxy.com",
        "https://docker.mirrors.ustc.edu.cn",
        "https://docker.nju.edu.cn"
    ]
}
EOF
```

----------------
2024-12-03更新
可用镜像源：

```bash
"https://hub.geekery.cn",
"https://hub.littlediary.cn",
"https://docker.rainbond.cc",
"https://docker.unsee.tech",
"https://docker.m.daocloud.io",
"https://hub.crdz.gq",
"https://docker.nastool.de"
```

-----------------

(2) 重启 Docker 服务

```bash
sudo systemctl daemon-reload
sudo systemctl restart docker
```

(3) 重新运行 Docker 测试容器

```bash
sudo docker run hello-world
```

(4) 参考
<https://www.coderjia.cn/archives/dba3f94c-a021-468a-8ac6-e840f85867ea>

# 三. 修改镜像存储路径

(1) 查看当前存储路径以及存储空间

```bash
sudo docker info   # 查看docker数据存储路径，默认为Docker Root Dir:/var/lib/docker
sudo docker system df # 查看docker数据占用的存储空间，-v参数是详细列出
```

(2) 修改/etc/docker/daemon.json 文件

```bash
sudo vim /etc/docker/daemon.json  # 新建配置文件，在其中输入以下信息
 
{
"data-root": "/data/docker",  # 配置docker数据路径
"registry-mirrors": ["http://hub-mirror.c.163.com"]  # 配置国内源[可选]
}
```

(3) 将原文件拷贝到新目录下

```bash
# 将原来docker中存储的数据copy到新的存储目录下
sudo cp -r /var/lib/docker /data/docker
```

(4) 重启docker服务

```bash
sudo systemctl daemon-reload
sudo systemctl restart docker
 
# 查看image信息
docker images
 
# 可以将之前的目录中数据删除
rm -rf /var/lib/docker
```

(5) 参考
<https://blog.csdn.net/weixin_43145427/article/details/123770971>

# 四. Docker镜像和容器构建流程

1. 根据dockerfile构建镜像

   ```bash
   docker build -t 镜像名:版本号 
   ```

2. 构建并运行单个容器

   ```bash
   docker run xxx
   ```

3. 构建并运行多个容器(需要docker compose.yaml)

   ```bash
   docker-compose up -d
   ```

# 五. 镜像操作

1. 删除镜像：

   ```bash
   docker rmi 镜像名/镜像号 # -f强制删除
   ```

2. 查看镜像详细信息

   ```bash
   docker inspect 镜像号
   ```

3. 修改镜像名称

   ```bash
   docker tag 镜像名:镜像版本号 新镜像名:新镜像版本号
   删除原镜像
   docker rmi 镜像名:镜像版本号  # -f强制删除
   ```

# 六. 容器操作

1. 启动容器：

   ```bash
   docker start 容器名/容器号
   ```

   进入容器终端

   ```bash
   docker exec -it 容器名/容器号 bash
   ```

1. 停止容器：

   ```bash
   docker stop 容器名/容器号  # -f强制停止
   ```

2. 删除容器：

   ```bash
   docker rm 容器名/容器号 # -f强制删除
   ```

3. 修改容器名称

```bash
docker rename 旧容器名 新容器名
```

# 七. Nvidia驱动工具

见Nvidia中第二部分nvidia-container-toolkit安装。

# 八. Docker访问X11服务器

主机上显示图形界面，如rviz/rviz2的图形界面。

1. 编辑 ~/.xprofile 文件：

```bash
vim ~/.xprofile
```

如果该文件不存在，系统会自动创建一个新的。

2. 在文件中添加以下内容：

```bash
# 允许本地 Docker 容器访问 X11 服务器
xhost +local:docker
```

保存退出使更改生效。重新登录用户账户，xhost +local:docker 命令将在登录时自动执行。
