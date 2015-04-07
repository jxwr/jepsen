# How to set up nodes via LXC

## Ubuntu 14.04 / trusty

安装必要的包，创建container，名字为n1-n10
```
sudo apt-get install lxc debootstrap lxc-templates css
sudo lxc-create -n n{1..10} -t debian
```

注释掉/etc/default/lxc-net
```
#LXC_DHCP_CONFILE=/etc/lxc/dnsmasq.conf
```

配置/etc/lxc/dnsmasq.conf，让lxc为Container分配固定IP地址
```
dhcp-host=n1,10.0.3.101
dhcp-host=n2,10.0.3.102
dhcp-host=n3,10.0.3.103
dhcp-host=n4,10.0.3.104
dhcp-host=n5,10.0.3.105
dhcp-host=n6,10.0.3.106
dhcp-host=n7,10.0.3.107
dhcp-host=n8,10.0.3.108
dhcp-host=n9,10.0.3.109
dhcp-host=n10,10.0.3.110
```

停止所有container，重启lxc-net
```
sudo service lxc-net restart
```

如果不成，需要重启一下dnsmasq
```
sudo killall -s SIGHUP dnsmasq
```

启动Container
```
sudo lxc-start -n n{1..10}
```
