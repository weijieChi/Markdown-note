# 修改 proxmox Host IP 為 DHCP

    首先我的環境是 HDCP 設定 IP ，但是 Host 是 static IP ，所以當重新開機後 Host 就沒有網路了  

## 步驟

1. 到 `/etc/network/interfaces` 宿改這個檔案
      . 當初用 `vi` 但有些不懂操作，後來改用 `nano` 編輯
2. DHCP 參考檔案
      ``
      iface eth0 inet manual

       auto vmbr0
       iface vmbr0 inet dhcp
       bridge_ports eth0
       bridge_stp off
       bridge_fd 0
      ```



### 參考資料

https://www.servethehome.com/how-to-change-primary-proxmox-ve-ip-address/

https://forum.proxmox.com/threads/ve_host-web-interface-setup-for-dhcp.27481/