#ARM 路由器 安装NGINX
参考：
https://www.hqt.ro/how-to-install-entware-arm/
https://www.hqt.ro/nginx-web-server-with-php-support-through-entware/

SHELL:

```
cd ~
wget -c -O entware.arm-setup.sh http://files.hqt.ro/entware.arm/entware.arm-setup.sh
chmod +x ./entware.arm-setup.sh
./entware.arm-setup.sh

vi /opt/etc/nginx/nginx.conf
/opt/etc/init.d/S80nginx restart
tail -n 100 -f /opt/var/log/nginx/error.log
```


