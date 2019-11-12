# docker与Springboot

> 在Springboot中使用docker

# jdk

1. 安装

   `sudo yum -y install java-1.8.0-openjdk*`

2. 环境变量 `vim /etc/profile`

   ```shell
   export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.201.b09-2.el7_6.x86_64 
   export PATH=$PATH:$JAVA_HOME/bin 
   ```

   1. 修改完，使其生效

   ```
   source /etc/profile
   ```

# consul

1. 安装

   `sudo docker pull consul`

2. 启动

   `sudo docker run -d -p 8500:8500 --name node1 consul agent -server -bootstrap-expect 1 -data-dir=/tmp/consul -client="0.0.0.0" -ui`

# 配置springboot

以网关为例说明：sr-service-gateway

## Dockerfile

1. 创建docker目录

   sr-service-gateway/src/main/docker

2. 创建文件名：Dockerfile，内容：

   ```xml
   FROM java:8
   VOLUME /tmp
   ADD sr-service-gateway-0.0.1-SNAPSHOT.jar gateway.jar
   ENTRYPOINT ["java", "-Djava.security.egd=file:/dev/./urandom", "-jar","gateway.jar"]
   ```

   VOLUME 指定了临时文件目录为/tmp。其效果是在主机 /var/lib/docker 目录下创建了一个临时文件，并链接到容器的/tmp。改步骤是可选的，如果涉及到文件系统的应用就很有必要了。/tmp目录用来持久化到 Docker 数据文件夹，因为 Spring Boot 使用的内嵌 Tomcat 容器默认使用/tmp作为工作目录 
   项目的 jar 文件作为 “app.jar” 添加到容器的 
   ENTRYPOINT 执行项目 app.jar。为了缩短 Tomcat 启动时间，添加一个系统属性指向 “/dev/urandom” 作为 Entropy Source 

3. 如下图

![image-20190412213424729](/Users/sam/Library/Application Support/typora-user-images/image-20190412213424729.png)

## pom.xm配置

```xml
<plugin>
    <groupId>com.spotify</groupId>
    <artifactId>docker-maven-plugin</artifactId>
    <version>1.0.0</version>
    <configuration>
      <imageName>${project.artifactId}</imageName>
      <dockerDirectory>src/main/docker</dockerDirectory>
      <resources>
        <resource>
          <targetPath>/</targetPath>
          <directory>${project.build.directory}</directory>
          <include>${project.build.finalName}.jar</include>
        </resource>
      </resources>
    </configuration>
</plugin>
```

> 可以不要前缀：<docker.image.prefix>springboot</docker.image.prefix>

![image-20190412224704107](/Users/sam/Library/Application Support/typora-user-images/image-20190412224704107.png)

## 注册中心配置

![image-20190412224753641](/Users/sam/Library/Application Support/typora-user-images/image-20190412224753641.png)

这里的host要使用上面consul启动时的容器名：`--name node1`，否则无法访问consul。

## 部署springboot

将jar和Dockerfile放到服务器上

![image-20190412225243996](/Users/sam/Library/Application Support/typora-user-images/image-20190412225243996.png)

## 构建镜像

`sudo docker build -t gateway .`

gateway 是镜像名，可以使用：`docker images`查看。不要忘记后面那个点.

![image-20190412230004566](/Users/sam/Library/Application Support/typora-user-images/image-20190412230004566.png)

## 运行镜像

`docker run -p 10084:10084 -t --link node1 gateway `

容器之间要使用 `--link node1` 关联，否则无法访问。

![image-20190412225434538](/Users/sam/Library/Application Support/typora-user-images/image-20190412225434538.png)

![image-20190412225454795](/Users/sam/Library/Application Support/typora-user-images/image-20190412225454795.png)

![image-20190412225716858](/Users/sam/Library/Application Support/typora-user-images/image-20190412225716858.png)

# 日志

https://blog.csdn.net/u014746226/article/details/89537258

# 问题

还未解决服务打印日志输出到文件问题

还有个别启动参数不甚明白。

Dockerfile配置只限于以上文件配置，复杂些就不清楚了。