---
layout: post
title: NFS + Autofs + Netgroup
category: other
intro: "Using NFS, Autofs, Netgroup together"
---

We can use NFS, Autofs, Netgroup together.

首先我们考虑一下问题:
1. 可不可以讓用戶端在有使用到 NFS 檔案系統的需求時才讓系統自動掛載？
2. 當 NFS 檔案系統使用完畢後，可不可以讓 NFS 自動卸載，以避免可能的 RPC 錯誤？

Autofs可以避免以上的问题, 自動掛載的 autofs 服務可以在用戶端需要 NFS 伺服器提供的資源時才掛載。


Review:
1 Network FileSystem (NFS) 可以讓主機之間透過網路分享彼此的檔案與目錄；
2 NFS 主要是透過 RPC 來進行 file share 的目的，所以 Server 與 Client 的 RPC 一定要啟動才行！
3 NFS 的設定檔就是 /etc/exports 這個檔案；
4 NFS 的權限可以觀察 /var/lib/nfs/etab，至於的重要登錄檔可以參考 /var/lib/nfs/xtab
5 這個檔案，還包含相當多有用的資訊在其中！
6 NFS 伺服器與用戶端的使用者帳號名稱、UID 最好要一致，可以避免權限錯亂：
7 NFS 伺服器預設對用戶端的 root 進行權限壓縮，通常壓縮其成為 nfsnobody 或 nobody。
8 NFS 伺服器在更動 /etc/exports 這個檔案之後，可以透過 exportfs 這個指令來重新掛載分享的目錄！
10 可以使用 rpcinfo 來觀察 RPC program 之間的關係！！！
11 NFS 伺服器在設定之初，就必須要考慮到 client 12端登入的權限問題，很多時候無法寫入或者無法進行分享，主要是 Linux 13實體檔案的權限設定問題所致！
14 NFS 用戶端可以透過使用 showmount, mount 與 umount 來使用 NFS 主機提供的分享的目錄！
15 NFS 亦可以使用掛載參數，如 bg, soft, rsize, wsize, nosuid, noexec, nodev 等參數， 來達到保護自己檔案系統的目標！
16 自動掛載的 autofs 服務可以在用戶端需要 NFS 伺服器提供的資源時才掛載。


Links:
http://linux.vbird.org/linux_server/0330nfs.php#nfsclient_autofs
Google.....
