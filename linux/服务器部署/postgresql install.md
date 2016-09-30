# 编译安装postgresql

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

## 解压并移动目录
```
tar xvzf postgresql-9.4.8.tar.gz
cp -r postgresql-9.4.8 /usr/local/postgresql-9.4.8
cd /usr/local/postgresql-9.4.8
```


## 编译安装
```bash
./configure --prefix=/usr/local/postgres --with-pgport=5432 --with-perl --with-python --with-tcl --with-openssl --with-pam  --without-ldap --with-libxml  --with-libxslt  --enable-thread-safety  --with-wal-blocksize=16 --with-blocksize=16 --enable-dtrace --enable-debug

make && make install
```

## 增加用户并赋予权限
```bash
groupadd postgres
useradd -g postgres postgres

chown -R postgres:postgres /usr/local/postgres
mkdir -p /var/postgres/data
mkdir -p /var/postgres/logfile
chown postgres:postgres /var/postgres/
chown postgres:postgres /var/postgres/*
chown postgres:postgres /usr/local/postgres/*
chmod -R 700 /var/postgres/*
```

## 切换用户
```bash
su postgres

echo "export PGHOME=/usr/local/postgres" >> ~/.bash_profile
echo "export PGDATA=/var/postgres/data" >> ~/.bash_profile
echo "export PATH=\$PGHOME/bin:\$PATH" >> ~/.bash_profile
echo "export MANPATH=\$PGHOME/share/man:\$MANPATH" >> ~/.bash_profile
echo "export LANG=en_US.utf8" >> ~/.bash_profile
echo "export DATE=\`date +\"%Y-%m-%d %H:%M:%S\"\`" >> ~/.bash_profile
echo "export LD_LIBRARY_PATH=\$PGHOME/lib:\$LD_LIBRARY_PATH" >> ~/.bash_profile

source ~/.bash_profile
```

```sql
initdb -D /var/postgres/data --locale=zh_CN.UTF8
pg_ctl -D /var/postgres/data -l /var/postgres/logfile/log start
```

```bash
vim /var/postgres/data/pg_hba.conf

host    all             all             0.0.0.0/0               md5

vim /var/postgres/data/postgresql.conf

listen_addresses='*'
port = 5432

pg_ctl -D /var/postgres/data -l /var/postgres/logfile/log restart

psql
```

```sql
alter user postgres with password 'password';
```


# 修改防火墙
```
systemctl disable firewalld.service
systemctl stop firewalld.service
yum install -y iptables-services
iptables -I INPUT -p tcp --dport 5432 -j ACCEPT
service iptables save
service iptables restart
```

## 初始化SCHEMA
```sql
-- 赋予权限
CREATE ROLE schema_name login nocreatedb nocreaterole noinherit encrypted password 'schema_password';
CREATE SCHEMA schema_name;
grant connect on database postgres to schema_name;
grant ALL PRIVILEGES on schema schema_name to schema_name;
grant ALL PRIVILEGES on all tables in schema schema_name to schema_name;

--创建只读用户
./createuser --interactive readonly;    -- 三个问题都是n

alter user postgres with password 'password';

grant usage on schema schema_name to readonly;
grant select  on all tables in schema schema_name to readonly;
```
