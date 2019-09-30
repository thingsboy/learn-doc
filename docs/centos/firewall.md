# 防火墙

> 介绍centos有关防火墙的操作。

# 开放指定端口

```shell
# 80是要开放的端口
firewall-cmd --permanent --zone=public --add-port=80/tcp
# 重载防火墙使端口生效
firewall-cmd --reload
```

# 检查端口是否生效

```shell
firewall-cmd --zone=public --query-port=80/tcp
```

- 如果打印出`yes`说明端口开放成功。

# 检查防火墙状态

```shell
firewall-cmd --state
```

# 检查防火墙规则

```shell
firewall-cmd --list-all
```

# 开关防火墙

```shell
# 打开防火墙
systemctl start firewalld
# 关闭防火墙
systemctl stop firewalld
# 防火墙状态
systemctl status firewalld
```

# 防火墙出错：Failed to start...

> 报错信息：Failed to start firewalld.service: Unit firewalld.service is masked.

```shell
# 执行
systemctl unmask firewalld
```