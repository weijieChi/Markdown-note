使用跟系統有關的指令最好是使用 root 或是 sudo 取得最高權限比較不會有問題。
在早期的 `ifconfig` 是 net-tool 裡面的的工具，但是因為已經沒有人在維護，所以現在新的發行版本多以 iproute2 套件來取代， `ip` 便是其中一個指令。
以下是 `ip` 跟其他網路相關指令對照圖
![ip tool](./image/ip%20tool.jpg)


# ip 指令相關介紹

## 顯示網路基本設定

```sh
# 以下的指令功能基本相同，都是顯示目前網路狀態
ip address
ip a
ip addr
ip addr show
```
因為現在很多 Linux 指令不會要求將參數名稱晚整顯示出來，只要可以辨識即可，但為了清楚表示指令功能，所以以下範例會以晚整參數名稱顯示

顯示 IPv4 或 IPv6 資訊
```sh
ip -4 address # 顯示 IPv4 資訊
ip -5 address # 顯示 IPv6 資訊
```

顯示特定網路介面資訊
```sh
ip address show eth1 # eth1 是網路介面名稱
# OR
ip address show dev eth1
```

顯示目前網路介面狀態
```sh
ip link
```
顯示 ARP 狀態
```sh
ip neighbor
```

顯示目前主機路由
```sh
ip route
```

## 定義網路設定

新增網卡(eth1)的ip位址
```sh
# ip addr add ip位址/CIDR dev eth1   
ip address add 192.168.100.1/24 dev eth1
```

# 其他
總之 iproute2 我目前大多是用來查看網路狀態，如果要設定網路的話我會使用 `nmcli` 來處理
文件參考連結 [nmcli](./Linux%20%E7%B6%B2%E8%B7%AF%20nmcli%20%E8%A8%AD%E5%AE%9A.md)

# 參考
https://www.ltsplus.com/linux/ip-command

https://hackmd.io/@night0915/BJztDJeor

http://www.study-area.org/tips/adv-route/Adv-Routing-HOWTO-3.html