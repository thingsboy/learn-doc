# 安装

> 介绍docker的安装。

## 二进制文件安装

- 选择版本：https://download.docker.com/linux/static/stable/x86_64/

- 下载tgz
- 解压：tar xzvf docker.xx.tgz
- 复制二进制文件到 /usr/bin/ : `cp docker/* /usr/bin/ `

- 检查是否安装：`docker version`

- 配置docker.service文件

  vi /usr/lib/systemd/system/docker.service

  ```
  [Unit]
  Description=Docker Application Container Engine
  Documentation=https://docs.docker.com
  After=network-online.target firewalld.service
  Wants=network-online.target
   
  [Service]
  Type=notify
  ExecStart=/usr/bin/dockerd
  ExecReload=/bin/kill -s HUP $MAINPID
  LimitNOFILE=infinity
  LimitNPROC=infinity
  TimeoutStartSec=0
  Delegate=yes
  KillMode=process
  Restart=on-failure
  StartLimitBurst=3
  StartLimitInterval=60s
   
  [Install]
  WantedBy=multi-user.target
  ```

- vi /etc/docker/daemon.json

  ```json
  {
  "registry-mirrors": ["https://registry.docker-cn.com"]
  }
  ```

- 启动dockerd服务进程

  ```
  systemctl daemon-reload
  systemctl start docker.service
  ```

- 检验

  ```
  ps aux|grep docker
  ```

  