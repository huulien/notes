# 编译安装zookepper

## 下载zookepper


## 修改配置文件
mv /usr/local/zookeeper/conf/zoo_sample.cfg /usr/local/zookeeper/conf/zoo.cfg

/usr/local/zookeeper/bin/zkServer.sh start

## 开放端口
systemctl disable firewalld.service
systemctl stop firewalld.service
yum install -y iptables-services
iptables -I INPUT -p tcp --dport 2181 -j ACCEPT
service iptables save
service iptables restart
