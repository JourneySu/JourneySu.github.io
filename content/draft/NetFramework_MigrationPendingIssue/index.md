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
    "",
    "",
]
series = [""]
aliases = ["migrate-from-jekyl"]
+++



    情境：Entity Framework(非EF Core)下，若遇到Code的Migration紀錄，與DB的Migration紀錄(__MigrationHistory)不一致時…

Step  
1、更改User的Name長度，從40-->100  
2、Add-Migration。會發現有pending訊息  
3、Update-Database。會發現仍然有錯誤  
4、將Migration資料夾下的Migration全部刪除，及將__MigrationHistory的資料全數刪除。  
5、重新進行Add-Migration。會發現有資料表已存在的錯誤訊息。  
6、將資料表全部刪除。  
7、重新Add-Migration，得到結果為成功。




其他指令
EF

1、Update-Database -TargetMigration 201911250232012_20191125_1
將Migration回滾至201911250232012_20191125_1的下一個，
這個動作會將DB MigrationHistory也刪除對應資料



2、重新Update-Database
會將目前為此還沒有做的多個Migration更新至db，並新增MigrationHistory