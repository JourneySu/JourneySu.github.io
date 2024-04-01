+++
author = "Hailey"
title = "同時安裝EF Core及EF，在VS2022不能Migration!
date = "2024-02-27"
description = "…"
tags = [
    "",
    "",
]
categories = [
    "MSSQL",
    "",
]
series = [""]
aliases = ["migrate-from-jekyl"]
+++




- [嘗試使用Add-Migration指令，修改DB Schema，](#嘗試使用add-migration指令修改db-schema)
        - [參考連結](#參考連結)


## 嘗試使用Add-Migration指令，修改DB Schema，
* 使用Visual Studio 2022，會出現以下奇怪錯誤

![](imgs/VS2022Error.png)


* 同樣的專案，改成使用Visual Studio 2019，進行Add-Migration指令，得到的結果為成功
![](imgs/VS2019Success.png)


###### 參考連結
https://www.itsvse.com/thread-4889-1-1.html