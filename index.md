# 脚本修改网卡

## ip和网关地址需要改为自己的

```bash
#!/bin/bash
cp /etc/sysconfig/network-scripts/ifcfg-ens33 /etc/sysconfig/network-scripts/ifcfg-ens34
sed -i s/dhcp/static/ /etc/sysconfig/network-scripts/ifcfg-ens33
sed -i s/ONBOOT=no/ONBOOT=yes/ /etc/sysconfig/network-scripts/ifcfg-ens33
grep "^IPADDR" /etc/sysconfig/network-scripts/ifcfg-ens33
if [ $? -eq 0 ];then
        echo network is OK!
        echo 网卡IP为`hostname -I`
else
    echo IPADDR=192.168.1.10>>/etc/sysconfig/network-scripts/ifcfg-ens33
    echo MASK=255.255.255.0>>/etc/sysconfig/network-scripts/ifcfg-ens33
    echo GATEWAY=192.168.1.2>>/etc/sysconfig/network-scripts/ifcfg-ens33
    echo DNS1=8.8.8.8>>/etc/sysconfig/network-scripts/ifcfg-ens33
    echo DNS2=114.114.114.114>>/etc/sysconfig/network-scripts/ifcfg-ens33
    nmcli c reload #重启网卡
```
