+++
author = "Hailey"
title = "ReSharperNote"
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


## 指令

`Ctrl+R, Ctrl+P` 提取參數變成由Method傳入  
`Ctrl+R, Ctrl+I` inline，簡化不必要的變數將2行縮減成一行  
`Ctrl+R, Ctrl+F` 將變數宣告提取至field(全域)…等  
`Ctrl+R, Ctrl+M` 將圈選起來的區塊提取至一新Method  
`Ctrl+R, A` 執行測試  
`Alt Enter` 產生class、Method




#### 使用範例  
Step1.  
`new Customer` + `Alt Enter` ==>
```c#
var customer = new Customer();
```

Step2.在Customer上面按 `Alt Enter`產生class  
```c#
    public class Calculator
    {
    }
```