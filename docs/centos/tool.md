# centos工具安装

# 离线安装zip

- 检查是否已经安装zip

`$ rpm -qa | grep unzip`

- 下载unzip安装包 [unzip-6.0-19.el7.x86_64.rpm](http://mirror.centos.org/centos/7/os/x86_64/Packages/unzip-6.0-19.el7.x86_64.rpm)

https://centos.pkgs.org/7/centos-x86_64/unzip-6.0-19.el7.x86_64.rpm.html

- 执行指令安装unzip包

`$ rpm -ivh unzip-6.0-19.el7.x86_64.rpm`

看到输出 `You have new mail in ....`

说明安装成功

# centos 7 安装 Oracle 

https://www.cnblogs.com/yejingcn/p/10278473.html



中文乱码，要设置编码：

文件：**/home/oracle/.bashrc**

```
export LANG=zh_CN.UTF-8
export NLS_LANG=AMERICAN_AMERICA.ZHS16GBK
```

