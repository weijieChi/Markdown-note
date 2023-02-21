# MBR 工具


. fdisk
    只能格式化 MBR 格式硬碟
. mkfs.*
    格式掛特定檔案格式工具

# GPT 工具

. parted

 1. `parted dev/sdc`
   指定磁碟裝置
 2. `print`
   先觀察目前的磁碟狀態
 3. `mktable gpt`
   指定使用 gpt 格式
   > 使用 mklable 可以選擇 MBR 格式或是 GPT，如果使用 MBR 的格式輸入 msdos ， GPT 則輸入 gpt
   https://jeffwen0105.com/linux-storage-partition/
 4. `mkpart`
   ```
   Partition name?  []? my_part
   File system type?  [ext2]?
   Start? 1
   End? 10000
   ```

  > 單位可以選擇以下:
    s : sector 硬碟儲存的最小容量單位
    B : byte
    MiB 、 GiB、 TiB ( 可以整除 2 )
    MB 、 GB 、 TB ( 可以整除 10 )
    起始點以 2048s 開始是一個安全界限的開始，如未能配置好開始的分區導致無法有效對齊，會出現警告，一般都建議從 2048s 為基本起點。
    https://jeffwen0105.com/linux-storage-partition/

# 在 ubuntu 安裝 xfs 工具
因為 xfs 檔案格式為 [red hat 的維護的檔案系統](https://www.cyberciti.biz/faq/how-to-install-xfs-and-create-xfs-file-system-on-debianubuntu-linux/)，在 red hat 系列的 Linux 版本會預設安裝，但是 ubuntu 等 Debian 等系列的 Linux版本並不會預設安裝
以下為 ubuntu 安裝 xfs 的步驟

1. 安裝 xfs 套件
```
sudo apt-get install xfsprogs
```

2. 之後再用 `mkfs.xfs` 格式化
```
mkfs.xfs -f /dev/sdc1
```
3. 掛載時候要指定使用 xfs 系統才會成功掛載
```
mount -t xfs /dev/sdc1 /gptDisk/
```

# fstabe
## 位置： `/etc/fstab`
它的作用是設定硬碟分割區或其化儲存裝置，在開機時掛載點及如何掛載等選項。

# 其他
`df` 顯示硬碟空間使用狀況
`du`
`blkid`
`lsblk`
`mount`