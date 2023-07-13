---
title: "每次遠端我都懶得打密碼"
# title: "Connect to Remote Server Without Entering Password"
date: 2023-07-12T23:56:17+08:00
# draft: true
---

## 總要先弄把鑰匙吧
建立公鑰私鑰  


## 把公鑰放到遠端
ssh 進入遠端 Server

```
mkdir -p ~/.ssh
```

```
vim ~/.ssh/authorized_keys
```

複製你的公鑰內容進去這隻檔案

當然你也可以用 scp 或其他方式傳檔上遠端再把內容讀進去


## 回到本機

建立檔案 `~/.ssh/config`

添加

```
Host dev
    HostName 1.2.3.4
    User username
    IdentityFile ~/.ssh/id_ed25519
```

## 測試

```
ssh dev
```

## REF

https://kb.iu.edu/d/aews

