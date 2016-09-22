# 编译安装kafka

## 下载源码
wget http://mirrors.tuna.tsinghua.edu.cn/apache/kafka/0.10.0.0/kafka_2.11-0.10.0.0.tgz

tar xzvf kafka_2.11-0.10.0.0.tgz
cd kafka_2.11-0.10.0.0

bin/kafka-server-start.sh config/server.properties
bin/kafka-server-start.sh -daemon ./config/server.properties

# 修改防火墙
```
systemctl disable firewalld.service
systemctl stop firewalld.service
yum install -y iptables-services
iptables -I INPUT -p tcp --dport 9092 -j ACCEPT
service iptables save
service iptables restart
```


bin/kafka-list-topic.sh --zookeeper 127.0.0.1:2181