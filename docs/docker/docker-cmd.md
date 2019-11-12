# 常用指令

https://mp.weixin.qq.com/s/d_CuljDTJq680NTndAay8g

# 指令

1. 删除运行的容器

```
sudo docker rm 容器id
```

2. 查看当前容器

```
sudo docker ps
```

 `sudo docker ps -a`

3. 删除镜像

```
sudo docker rmi 镜像名
```

4. 当前已有镜像

```
sudo docker images
```

5. 清除none的images

```
docker rmi $(docker images -f "dangling=true" -q)
```

6. 删除已经exit容器

```
sudo docker rm $(sudo docker ps -qf status=exited)
```

7. 端口

- -p 指定端口号 第一个8080 为 容器内部的端口号 第二个8080位外界访问的端口号,将容器内的8080端口号映射到外部的8080端口号

8. 启动、停止、重启容器命令

```
docker start container_name/container_id
docker stop container_name/container_id
docker restart container_name/container_id
```

9. 进入到容器

```
docker attach container_name/container_id
```

# Dockerfile

```yml
##  Dockerfile文件格式

# This dockerfile uses the ubuntu image
# VERSION 2 - EDITION 1
# Author: docker_user
# Command format: Instruction [arguments / command] ..
 
# 1、第一行必须指定 基础镜像信息
FROM ubuntu
 
# 2、维护者信息
MAINTAINER docker_user docker_user@email.com
 
# 3、镜像操作指令
RUN echo "deb http://archive.ubuntu.com/ubuntu/ raring main universe" >> /etc/apt/sources.list
RUN apt-get update && apt-get install -y nginx
RUN echo "\ndaemon off;" >> /etc/nginx/nginx.conf
 
# 4、容器启动执行指令
CMD /usr/sbin/nginx
```

# 构建镜像

当前目录作为构建上下文

`$ docker build .`

1. 大多数情况，应该将一个空目录作为构建上下文环境。
2. 通过`.dockerignore`文件排除上下文目录中的文件和目录。
3. 可通过`-f`指定文件位置：`$ docker build -f /path/Dockerfile .`
4. 通过`-t`参数指定构建成镜像的仓库名、标签名。可同时使用多个`-t`参数。