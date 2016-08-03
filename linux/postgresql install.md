# 编译安装postgresql

## 安装编译环境
```bash
yum install -y subversion
yum install -y flex bison
yum install -y git
yum install -y gcc gcc-c++ autoconf automake
yum install -y zlib zlib-devel openssl openssl-devel pcre-devel
yum install -y libxml*
yum install -y openssl
yum install -y openssl-devel
yum install gcc zlib-devel xz openssl-devel bzip2 bzip2-devel lrzsz -y
yum install libjpeg-turbo-devel -y
yum install zlib-devel -y
yum install libjpeg-turbo-devel -y
yum install -y make gcc-c++ cmake bison-devel ncurses-devel
```

## 编译安装
```bash
cd postgresql-9.4.8
./configure --prefix=/usr/local/postgresql --without-readline
make && make install
```

## 增加用户并赋予权限
```bash
groupadd postgres
useradd -g postgres postgres

chown -R postgres:postgres /usr/local/postgresql
mkdir -p /var/postgresql/data
chmod -R 775 /var/postgresql/*
chown -R postgres:postgres /var/postgresql
```

## 增加配置
```bash
export PATH=/usr/local/postgresql/bin:$PATH
export PGDATA=/var/postgresql/data
export PGHOME=/usr/local/postgresql
export LANG=zh_CN.UTF-8
export PGPORT=5432
```

## 切换用户
```bash
su postgres
```

```sql
initdb -D /var/postgresql/data --locale=zh_CN.UTF8
pg_ctl -D /var/postgresql/data -l logfile start
```

```bash
vim /var/postgresql/data/pg_hba.conf
host    all             all             0.0.0.0/0               md5
vim /var/postgresql/data/postgresql.conf
listen_addresses='*'

psql
```

```sql
alter user postgres with password 'xxxxxx';
```

## 初始化SCHEMA
```sql
create schema tradecore;

-- 赋予权限
CREATE ROLE tradecore login nocreatedb nocreaterole noinherit encrypted password 'tradecore_dev';
grant connect on database postgres to tradecore;
grant ALL PRIVILEGES on schema tradecore to tradecore;
grant ALL PRIVILEGES on all tables in schema tradecore to tradecore;
```
