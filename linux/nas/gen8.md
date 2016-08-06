# GEN8 nas资料汇总

## 论坛资料
### NAS:资料：
http://www.chiphell.com/forum.php?mod=viewthread&tid=1202503

### HP Gen8 资源百度网盘分享：
链接: http://pan.baidu.com/s/1eQtlrSA 密码: r8we

### HP MicroServer GEN8第二弹，DIY and 方案（ESXi app）
http://www.chiphell.com/thread-857280-1-1.html

http://www.chiphell.com/thread-867588-1-1.html

http://www.hinas.net/portal.php?mod=view&aid=11

### Gen8安装Esxi6.0，pc传数据到黑裙超慢 - NAS / SSD / HDD
http://www.chiphell.com/thread-1311446-1-1.html

### GEN8折腾日记-Windows Server 2012 R2 + Hyper-V安装篇
http://www.nasyun.com/thread-24508-1-1.html

### Gen8不要脸折腾之安装Hyper-V以及群晖
http://www.nasyun.com/thread-25075-1-1.html

### GEN8折腾日记-硬件介绍，配件购买及ILO介绍篇
http://www.nasyun.com/thread-24437-1-1.html

#### 制作HP MicroServer Gen8可用的ESXi 5.x SD/TF卡启动盘
http://blog.ltns.info/linux/esxi_sd_boot_on_microserver_gen8/

## 磁盘挂载
### 挂载nfs磁盘：
mount -t nfs 10.0.0.80:/disk01 /volume1/disk01


### cifs挂载
mount -t cifs -o iocharset=utf8,username=,password="" //Win-manager/disk01 /volume1/disk01
