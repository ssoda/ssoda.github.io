---
title: "PostgreSQL pg_dump pg_restore"
date: 2024-02-16T00:03:39+08:00
# draft: true
tags: ["note"]
---

## 前情提要

當你需要對不同的遠端 `PostgreSQL` 資料庫進行資料遷移時...

## 實際操作

在此之前，只碰過 MySQL ，馬上能想到的超簡單做法為：  
```
打開 phpmyadmin -> 連線資料庫 -> 匯出 -> 切換資料庫 -> 匯入
```

但是在這邊需要使用 PostgreSQL ...

---

目前 GUI 是使用 `DBeaver` (我覺得比 pgadmin 好用＝＝)，  

以為也是簡單匯出匯入就好...

結果發現它非常的原生，在匯出的時候，需要指定 `local client`，

研究後，可以理解為，你的本地也要有相對應的資料庫 client 端。  
(其實也挺合理的，因為 DBeaver 本來就是要來支援多款資料庫)

---

也就是說，要導出 PostgreSQL 的資料，本地也要裝該資料庫，

有嘗試過只裝 pg_dump 但發現沒辦法單獨使用。

於是我裝好了 PostgreSQL ，結果勒，

要設定 DBeaver 的 local client 時，Add Home 一直無法設定到我要的路徑，

它會一直在我前面串一堆看不懂的路徑(應該要指到`/usr/bin`)，也沒辦法自行編輯，

忘記是在哪篇看到，問題看起來是出在我用 snap 裝 DBeaver，果斷放棄這條路。

---
  
突然想到，欸我有 `docker` 啊，剛好之前測試有裝過 postgres 的 image，

馬上 `docker run` 跑一個容器，直接就有 pg_dump 和 pg_restore 可以用，舒服！

接下來一切都順利多了，

以下範例為：  
在容器內操作，  
從 db_host_1 導出 schema_a ，並直接匯入至 db_host_2 的 schema_a，  
user 皆為 postgres。  


(1)  
`pg_dump -h db_host_1 -U postgres -n schema_a bak.dump`

(2)  
在 db_host_2 建立新的空白 shema_2  -> 後記：這步也許可以再調整甚至省略   

(3)  
`pg_restore -Fc -h db_host_2 -U postgres -n schema_a < bak.dump`


本來是導出 sql 但 pg_restore 讀檔沒成功，  
沒繼續深入研究，改用 dump 檔案操作就順利解決。
