---
title: "Virtual Box 安裝的一些麻煩事"
date: 2024-06-26T23:01:27+08:00
draft: true
tags: ["note"]
---

## 前情提要
久久處理一次新開虛擬機，記錄一下遇到的一些麻煩及注意事項。  

## 安裝前的配置建議
略過無人安裝。  
用 2 核以上安裝真的比較快，也不容易遇到卡住問題。  

## 設定共用資料夾 & Guest Additions
裝置 > 共用資料夾 > 共用資料夾設定  
1. 選擇 host 端 資料夾路徑
2. 掛載點輸入要掛到客體的資料夾路徑 (如：`/home/ssoda/Documents/share`)
3. 勾選 自動掛載、設為永久

裝 Guest Additions:
裝置 > 插入 Guest Additions CD 映像...  
我這邊是遇到沒自動執行 ，所以直接到 Files 進到掛載的映像檔，然後點 `Run software`

### 遇到狀況 & 應對：  

狀況 1：
```
bzip not found
```
應對：
```
sudo apt install bzip2
```
---

狀況 2：
```
This system is currently not set up to build kernel modules.
```
應對：
```
sudo apt install virtualbox-guest-utils dkms
```
---

狀況 3：
```
遇到無權限存取掛載之資料夾
```
應對：
```
sudo usermod -a -G vboxsf $USER

然後重新登入，應該就可以看到掛載目錄了。(注意路徑有沒有打錯字)
```
---

狀況 4：
```
隔天打開遇到又遇到上述狀況 3...
就算輸入密碼進去，也是顯示空資料夾。
```
應對：
```
1. 先在 command line 移出該資料夾。
2. 裝置 > 共用資料夾 > 共用資料夾設定 ---> 移除原本配置的資料夾
3. 關機
4. 裝置 > 共用資料夾 > 共用資料夾設定 ---> 新增跟原本一樣的配置資料夾
5. 開機，就好了...
```

## 心得
怎感覺每次新的安裝遇到的狀況都不太一樣，真的有小精靈？
