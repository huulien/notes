# CENTOS 编译准备需要安装功能

## 修改源
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
yum makecache

## SYSTEM
yum update

## BUILD
yum install -y subversion
yum install -y flex bison
yum install -y git
yum install -y gcc gcc-c++ autoconf automake
yum install -y zlib zlib-devel openssl openssl-devel pcre-devel
yum install -y libxml*
yum install -y openssl
yum install -y openssl-devel
yum install -y gcc zlib-devel xz openssl-devel bzip2 bzip2-devel lrzsz 
yum install -y libjpeg-turbo-devel
yum install -y zlib-devel
yum install -y libjpeg-turbo-devel
yum install -y unzip
yum install -y net-tools
yum install -y psmisc
yum install -y vim
yum install -y wget

## PYTHON
wget https://bootstrap.pypa.io/ez_setup.py -O - | python
easy_install pip
easy_install virtualenv
easy_install virtualenvwrapper

## FIREWALL
* 关闭firewalld防火墙
systemctl disable firewalld.service
systemctl stop firewalld.service

* 安装并使用iptables防火墙
yum install iptables-services
service iptables save
service iptables restart

* 开放80 8090端口并将80请求转发给8090
iptables -I INPUT -p tcp --dport 80 -j ACCEPT
iptables -I INPUT -p tcp --dport 8090 -j ACCEPT
iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 8090

* firewalld防火墙开放端口
firewall-cmd --permanent --add-port=9988/tcp
firewall-cmd --reload
