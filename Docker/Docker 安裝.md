# Docker 安裝方式
這裡主要是介紹以 Linux 為主的安裝方式

在 Windows 跟 Mac OSX 因為 kenrnel 並沒有 Docker 執行環境所需要的 Namespaces 與 cgroup 等功能做邏輯隔離的功能，所以這兩個系統的 Docker 安裝實際上是安裝一個迷你 Linux VM ，再由套件提供所需的介面來提供操作，這裡就不介紹安裝方式，有興趣的人請自行搜尋安裝方式自行安裝八 :p

## 官方提供的 Linux 安裝腳本

```sh
sudo curl -fsSL https://get.docker.com/ | sh
```

許多較新的 Linux 發行版本多已經將 Docker Engine 軟套件整合進自身的套件庫，需要使用時可以直接透過線上套件庫安裝 Docker
## debian 流派發行版本，包含 Ubuntu
```sh
sudo apt install docker.io
```

## Red Hat 流派發行版本，包含 fedora 、 Rock Linux 等
```sh
sudo dnt intall docker
```

## 關於 Docker 安裝後未啟用問題
在 debian 流派發行版本 Docker 安裝完後預設就會自動啟動為系統服務，開機後會自行啟動
```sh
sudo systemctl status docker
```
會顯示 active (running)

但是在 Red Hat 流派發行版本，包含 fedora 、 Rock Linux 等並不會自行啟動，剛安裝完後並不會啟動 Docker
```sh
sudo systemctl status docker
```
會顯示 inactive (dead)
所以當使用 Red Hat 流派發行版本希望每次系統開機時後會自動啟動 Docker 為系統服務要下以下指令
```sh
sudo systemctl start docker  # 啟動 Docker 
sudo systemctl enable docker # 將 Docker 設定為系統服務，每次開機會自動啟動
```