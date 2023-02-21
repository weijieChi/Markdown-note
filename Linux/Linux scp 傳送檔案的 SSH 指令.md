# 前言

在純 terminal 介面的 Linux 當檔案要傳送到其他網路上非本地端得主機時就無法單純使用 cp 等指令，這時候就可以使用 `scp` 指令複製遠端主機的檔案，或是將本地端的檔案傳送到遠端主機。
還有當環境是沒有 GUI 的 Linux 主機 VM 時候，就沒辦法單純使用 Hypervisor 提供的右鍵複製貼上在 Host 跟 VM 之間互將傳送檔案
在使用時候要先確定遠端主機的 SSH-Server 服務有啟動，且防火牆沒有擋住 poet:22 。
在 windows powershell 有支援此指令。

註： 如果檔案位置是需要 root 權限才能讀取複製的話可能無法直接用 root 帳號複製遠端黨(我還沒查資料)，可以先把檔案移動或複製到一般使用者可以讀取的位置，並用 `chown` 改變檔案擁有者跟群組為一般使用者


# 指令基本範例
```
scp [參數] [使用者@主機IP]:來源檔案 [使用者@主機IP]:目的檔案
```

## 使用參數說明

### 常用參數：
* -p: 保留原本檔案資訊和權限
* -C: 壓縮
* -r: 遞迴複製整個資料夾的所有資料 // 當要複製資料夾(目錄)時候使用
* -P: 後面接連接埠號碼，使用指定連接埠 // 當 SSH 連線使用非標準連接埠號時候使用
* -v: 顯示詳細資訊
* -4: 強制使用 IPv4
* -6: 強制使用 IPv6

# 使用範例

## 連線前先確認要連線的遠端 Limux 主機 SSH- server 有啟動

1. 在準備連線的遠端 Linux 主機確認 SSH-Server 是否已經啟動
   先使用 `systemctl status sshd` SSH-Server 服務狀態，如果為狀態顯示 `Active: inactive (dead)`
   請使用 `systemctl start sshd` 指令啟動 SSH-Server 服務，之後如果相要每次開機就自動啟動 SSH-Server 服務就再加上 `systemctl enable sshd` 指令讓 SSH-Server 在每次開機就自動啟動

2. 檢查 Linux 防火牆是否允許 SSH-Server 服務通過
   這裡使用 red hat 的環境防火牆為 firewalld ，以下為 firewalld 的使用情境
   先下 `firewall-cmd --list-all` 檢查 firewalld 是否允許 SSH-Server 通過
   如果顯示 `services: dhcpv6-client mdns samba-client ssh` 裡面不包含 `ssh` (這個範例已經允許，所以有 `ssh`) 使用下列指令讓 firewalld 允許 SSH-Server 通過防火牆
   `firewall-cmd --permanent --add-service=ssh`
   `--permanent` 這個參數是要讓 firewalld 在下次開機時就自動允許 SSH-Server 通過防火牆

## 從 windows 下載 Linux 遠端檔案 (使用 powershell)

```
PS C:\Users\weijie\Documents\SSH_Download_practice> scp weijie@192.168.56.101:/home/weijie/test.txt .
weijie@192.168.56.101's password:
test.txt                                                                              100%    5     1.3KB/s   00:00
PS C:\Users\weijie\Documents\SSH_Download_practice>
```
一開始沒注意到範例最後的 `.` ，當要把遠端檔案改檔名時候可以把 `.` 改成 `你要的檔名`

## 把本地端檔案上傳到遠端 Linux 主機 (使用 powershell)

```
PS C:\Users\weijie\Documents\SSH_Download_practice> scp .\FromWindowsFile.txt weijie@192.168.56.101:/home/weijie/
weijie@192.168.56.101's password:
FromWindowFile.txt                                                                    100%   25     8.3KB/s   00:00
PS C:\Users\weijie\Documents\SSH_Download_practice>
```

# 參考

### scp
https://www.ruyut.com/2022/04/scp-copy-file.html
http://note.drx.tw/2008/03/ubuntuscp-part1.html

### firewalld
https://hoohoo.top/blog/firewalld-firewall-installation-allow-disable-ip-port-usage-introduction/