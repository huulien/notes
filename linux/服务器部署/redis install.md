# 编译安装redis

## 安装编译环境
```bash
yum install -y flex bison
yum install -y git
yum install -y gcc gcc-c++ autoconf automake
yum install -y zlib zlib-devel openssl openssl-devel pcre-devel
yum install -y libxml*
yum install -y openssl
yum install -y openssl-devel
yum install -y gcc zlib-devel xz openssl-devel bzip2 bzip2-devel lrzsz 
yum install -y libjpeg-turbo-devel 
yum install -y make gcc-c++ cmake bison-devel  ncurses-devel
yum install -y systemtap systemtap-sdt-devel
yum install -y perl-ExtUtils-Embed
yum install -y readline readline-devel
yum install -y pam pam-devel
yum install -y perl-ExtUtils-Embed readline-devel zlib-devel pam-devel libxml2-devel libxslt-devel openldap-devel python-devel gcc-c++   openssl-devel cmake
yum install -y tcl tcl-devel
```

# 下载
wget http://download.redis.io/releases/redis-3.2.0.tar.gz 
tar xzf redis-3.2.0.tar.gz
cp redis-3.2.0 /usr/local/ -r
cd /usr/local/redis-3.2.0
make MALLOC=libc

vim redis.conf
# requirepass foobared去掉注释，foobared改为自己的密码，我在这里改为redis
bind 127.0.0.1 修改成0.0.0.0

src/redis-server redis.conf &

# 修改防火墙
```
systemctl disable firewalld.service
systemctl stop firewalld.service
yum install -y iptables-services
iptables -I INPUT -p tcp --dport 6379 -j ACCEPT
service iptables save
service iptables restart
```

# 数据管理
## 安装工具
gem install redis-dump -V

## 导出数据
redis-dump -u :password@ip > redis.json

## 导入数据
cat redis.json | redis-load -u :password@ip:prot


