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

添加Host信息到每个Container
```
127.0.0.1       localhost n10 n10.local
::1             localhost ip6-localhost ip6-loopback
fe00::0         ip6-localnet
ff00::0         ip6-mcastprefix
ff02::1         ip6-allnodes
ff02::2         ip6-allrouters

10.0.3.101 n1 n1.local
10.0.3.102 n2 n2.local
10.0.3.103 n3 n3.local
10.0.3.104 n4 n4.local
10.0.3.105 n5 n5.local
10.0.3.106 n6 n6.local
10.0.3.107 n7 n7.local
10.0.3.108 n8 n8.local
10.0.3.109 n9 n9.local
10.0.3.110 n10 n10.local
```
