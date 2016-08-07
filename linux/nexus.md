# nexus备注

```bash
groupadd nexus
useradd -g nexus nexus_admin
chown -R nexus_admin /opt/nexus
chmod +wr /opt/nexus
passwd nexus_admin

ln -s /opt/nexus/nexus-2.11.2-06/bin/nexus /usr/bin/nexus
```