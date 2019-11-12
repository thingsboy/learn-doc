# 磁盘分区

**列出磁盘基本信息**

> sudo fdisk -l

找到未分区的disk磁盘 `/dev/xvdb`

**进入磁盘**

> fdisk /dev/xvdb

**查看磁盘情况**

> p

**创建新的分区**

> n

**分区号、分区大小**

回车即可

**写入分区表**

> w

**格式化分区**

> mkfs -t ext4 /dev/xvdb

**挂载分区**

> mkdir -p /data
> mount /dev/xvdb /data

**设置开机挂载分区**

> vim /etc/fstab
> /dev/xvdb       /data       ext4    defaults    0 0