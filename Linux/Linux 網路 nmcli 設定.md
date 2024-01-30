nmcli 有個圖形化介面的兄弟就是 nmtui ，不過在這邊只介紹 nmcli 指令

# nmcli 指令

## 狀態觀察

總之先從觀察網路介面狀態開始
以下的指令會顯示網路介面狀態
```sh
nmcli device status
```
若要查看目前正在連到哪個網路卡可以搭配 `connection` 加上 `show`
```sh
nmcli connection show
```

查看 ip ，不過還是使用 `ip` 指令查看會比較清楚
```sh
nmcli
```

## 使用 nmcli 修改網路設定
啟用或是停用網路介面
```sh
nmcli connection down enp0s3 # 停用介面， enp0s3 是網路介面名稱
nmcli connection up enp0s3 # 啟用介面， enp0s3 是網路介面名稱
```

設定固定 ip
```sh
nmcli connection modify enp0s4 ipv4.address 192.168.0.100/24 ipv4.gateway 192.168.0.1 # enp0s4 為網路介面名稱
```

設定動態 DHCP ip
```sh
nmcli device modify eth0 ipv4.method auto # IPv4
nmcli device modify eth0 ipv6.method auto # IPv6
```

設定 DNS
```sh
nmcli connection modify ens3 ipv4.dns 8.8.8.8
```


https://www.redhat.com/en/blog/rhel-9-networking-say-goodbye-ifcfg-files-and-hello-keyfiles

中文
https://min.news/technique/9d0f54403a6333b8051e9a4614b8c5fa.html

重要
http://n.sfs.tw/content/index/14379

有點過時的資料
https://dywang.csie.cyut.edu.tw/dywang/rhel7/node22.html