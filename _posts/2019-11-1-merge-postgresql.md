---
keywords:
  - Postgresql
  - Devops
  - Database
comments: true
title: 將 Postgresql 資料庫備份結合
cover_image: https://raw.githubusercontent.com/theblackcat102/theblackcat102.github.io/master/images/database_diagram.png
---

最近自己的資料庫即將吃滿我伺服器全部容量，但因為有些資料已經太舊，基本上不會被實時讀取。但是為了日後分析的完整性卻又不能直接刪除，因此我購置了硬碟打算在我自己的主機將所有遠端伺服器上太舊的資料轉移到我自己的本地主機。

由於我自己有定期備份到 blackblaze 的機制，因此我希望能在每次備份資料中將新筆數與本地端資料庫結合（舊筆資料依然保留在本地資料庫內），這樣隨著我遠端的舊資料刪除，我的本地端資料依然可以逐漸累積。

本來想法是寫一個自動備份的 script 將每月的 table dump 同步，後將舊資料刪除。然而這樣太慢，且我需要同時同步多個 table 。

最後在網路上找到一個[超簡單的方法](https://dba.stackexchange.com/questions/54986/merging-two-backups-form-a-postgresql-database)讓 pg_dump 的資料可以完美 restore 到本地端資料庫內。由於原來的網頁已經消失，需要透過 [web archive](https://web.archive.org/web/20141020052239/http://blog.fespinozacast.com/2014/01/04/merge-two-backups-of-a-postgresql-database/) 才能讀取
因此這裡我重新講解一次操作過程。

![](https://raw.githubusercontent.com/theblackcat102/theblackcat102.github.io/master/images/database_diagram.png#center)


1. 首先你需要一個含有完整 schema 的備份，T0 這個將會是用來初始化本地端資料庫的備份

```
(local)$ psql dbname < T0.dump
```

2. 從 Production 資料庫生成只有資料且唯輸入的的備份

```
(production)$   pg_dump -U postgres -a --inserts dbname | gzip -9 > backups.bak.gz 
```

3. 將 backups.bak.gz 再丟回本地端的資料庫即可

```bash
(local)$ gunzip -c backups.bak.gz | psql dbname
```


