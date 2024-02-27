+++
author = "Hailey"
title = "Hugo BundlePage"
date = "2024-02-26"
description = "一些指令或踩過的坑記錄"
tags = [
    "Hugo",
]
categories = [
    "Hugo",
]
series = ["Hugo使用記錄"]
aliases = ["migrate-from-jekyl"]
+++



目錄
- [常用指令](#常用指令)
- [那些我踩的坑](#那些我踩的坑)
  - [我明明刪除了文章，為什麼輸入url還是可以進入該網址閱讀？](#我明明刪除了文章為什麼輸入url還是可以進入該網址閱讀)

---

---
  

常用指令
===

建置

      hugo

建置，並在local host預覽網站(預設網址:http://localhost:1313/)

      hugo server 


那些我踩的坑
===
## 我明明刪除了文章，為什麼輸入url還是可以進入該網址閱讀？

原因：當您使用 hugo server 命令運行 Hugo 伺服器時，Hugo 不會自動清理 public 目錄中的內容。  
解決：
要清理已經生成的內容，您可以在執行 hugo 命令之前手動清空 public 目錄，或者在建置時加入以下參數。  
該參數告訴 Hugo 在生成網站之前清理 public 目錄歐

      hugo --cleanDestinationDir
      hugo server --cleanDestinationDir
