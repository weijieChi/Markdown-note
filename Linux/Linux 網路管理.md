# 識別與取得網路介面資訊
## 使用 `ip` 這個指令來查看網路卡，IP位址之設定等相關的資訊，相關指令執行如下：
```
[rockylinux@workstation ~]$ ip link show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000
    link/ether 08:00:27:ce:5e:d6 brd ff:ff:ff:ff:ff:ff
3: virbr0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN mode DEFAULT group default qlen 1000
    link/ether 52:54:00:94:4c:d5 brd ff:ff:ff:ff:ff:ff
4: virbr0-nic: <BROADCAST,MULTICAST> mtu 1500 qdisc fq_codel master virbr0 state DOWN mode DEFAULT group default qlen 1000
    link/ether 52:54:00:94:4c:d5 brd ff:ff:ff:ff:ff:ff
[rockylinux@workstation ~]$
```

## 若要顯示每一個網路介面卡資訊上面所設定的IP位址的話，則將 `link` 換成 `address` 即可：
```
[root@fedora ~]# ip address show 
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:22:6a:32 brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic noprefixroute enp0s3
       valid_lft 85639sec preferred_lft 85639sec
    inet6 fe80::b924:d629:199e:1e5b/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:e9:ca:ea brd ff:ff:ff:ff:ff:ff
    inet 192.168.56.101/24 brd 192.168.56.255 scope global dynamic noprefixroute enp0s8
       valid_lft 439sec preferred_lft 439sec
    inet6 fe80::26ea:7343:c884:7cb1/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
[root@fedora ~]# 
```
## 若要指定網路介面，則是在show後面再加上網路介面卡的名稱即可
ex: `ip address show enp0s8`

# 要觀察特定網路介面的效能
若要顯示某個網路介面卡之網路流量，則可以加上 `-s` 參數，則執行之後，會顯示有多少 bytes 位元封包接收到，有多少 bytes 位元封包傳送出去，以及封包錯誤以及封包有多少被丟棄。相關的執行指令輸出的訊息如下：
```
[rockylinux@workstation ~]$ ip -s link show enp0s3
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000
    link/ether 08:00:27:ce:5e:d6 brd ff:ff:ff:ff:ff:ff
    RX: bytes  packets  errors  dropped overrun mcast
    80167      822      0       0       0       136
    TX: bytes  packets  errors  dropped carrier collsns
    78114      506      0       0       0       0
[rockylinux@workstation ~]$
```

# 顯示本地路由表
使用 `ip route` 顯示本地路由表
ex:
```
[root@fedora ~]# ip route
default via 10.0.2.2 dev enp0s3 proto dhcp src 10.0.2.15 metric 100 //預設路由表，當封包目的位置不在路由表上時候就會往預設路由表送
10.0.2.0/24 dev enp0s3 proto kernel scope link src 10.0.2.15 metric 100 
192.168.56.0/24 dev enp0s8 proto kernel scope link src 192.168.56.101 metric 101 
[root@fedora ~]# 
```
## 顯示 IPv6 路由表
顯示 IPv6 路由表要加上 `-6` 參數
```
[root@fedora ~]# ip -6 route
::1 dev lo proto kernel metric 256 pref medium
fe80::/64 dev enp0s3 proto kernel metric 1024 pref medium
fe80::/64 dev enp0s8 proto kernel metric 1024 pref medium
[root@fedora ~]# 
```

# 到某目的 IP 的路由追蹤
指令 `traceroute`
ex: `teaceroute 8.8.8.8`
PS: windows 指令為 `tracert`

---

# 參考
https://ithelp.ithome.com.tw/articles/10278651