+++
author = "Hailey"
title = "談談C#-兩個變數指向相同記憶體位址"
date = "2024-02-27"
description = "那些開發時踩到的坑…"
tags = [
    "CSharp",

]
categories = [

]

aliases = ["migrate-from-jekyl"]
+++



目錄
- [Chatgpt說明](#chatgpt說明)

---

## Chatgpt說明
先上我與Chatgpt的學習過程吧！


我：

    我可以理解成，當兩個同type的變數指向同一個記憶體位置時，如
    ListNode a= new ListNode(3);
    var b = a;
    ，此時更改a或b變數底下的「屬性」，改的會是指向記憶體的值，

    但若更改a或b，如
    b=b.next，則代表將原有的指向記憶體引用斷開，改成指向另一記憶體，
    所以a和b此時指向的記憶體空間便會是不一樣的，對嗎？

ChatGPT

    是的，你的理解是正確的。

    當兩個同類型的變數指向同一個記憶體位置時，它們實際上是引用相同的物件。因此，如果你更改其中一個變數底下的屬性，例如變更 a.val 或 b.val，這將影響到同一個物件，因為它們指向同一個記憶體位置。

    然而，如果你更改其中一個變數本身，例如 b = b.next;，這將會斷開這兩個變數之間的連接，使得它們指向不同的記憶體位置。在這種情況下，a 和 b 將指向不同的物件，因此它們指向的記憶體空間將不同。

我：

    可以分別為我撰寫程式碼範例，使我更能理解嗎

ChatGPT

    當然可以，以下是一個範例程式碼：
```c#
Copy code
using System;

public class ListNode {
    public int val;
    public ListNode next;
    public ListNode(int val=0, ListNode next=null) {
        this.val = val;
        this.next = next;
    }
}

class Program {
    static void Main(string[] args) {
        // 創建一個新的 ListNode 物件 a
        ListNode a = new ListNode(3);

        // 將 b 設置為 a
        ListNode b = a;

        // 印出 a 和 b 的 val
        Console.WriteLine("a.val = " + a.val); // 3
        Console.WriteLine("b.val = " + b.val); // 3

        // 更改 a 的 val
        a.val = 5;

        // 印出 a 和 b 的 val，因為 a 和 b 都指向同一個物件，所以它們的 val 都會改變
        Console.WriteLine("After changing a.val:");
        Console.WriteLine("a.val = " + a.val); // 5
        Console.WriteLine("b.val = " + b.val); // 5

        // 創建一個新的 ListNode 物件 c
        ListNode c = new ListNode(10);

        // 將 b 設置為 c，這將斷開 a 和 b 之間的連接
        b = c;

        // 印出 a 和 b 的 val，它們現在指向不同的物件，所以它們的 val 不同
        Console.WriteLine("After changing b:");
        Console.WriteLine("a.val = " + a.val); // 5
        Console.WriteLine("b.val = " + b.val); // 10

        // 這裡再次更改 a 的 val
        a.val = 15;

        // 印出 a 和 b 的 val，即使 a 的 val 已經改變，但 b 不受影響，因為它們現在指向不同的物件
        Console.WriteLine("After changing a.val again:");
        Console.WriteLine("a.val = " + a.val); // 15
        Console.WriteLine("b.val = " + b.val); // 10
    }
}
```

    在這個範例中，我們創建了兩個 ListNode 物件 a 和 c，並將 b 設置為 a。然後，我們更改 a 的 val，這也會影響到 b，因為它們都指向同一個物件。接著，我們將 b 設置為 c，這將斷開 a 和 b 之間的連接，使得它們指向不同的物件。最後，我們再次更改 a 的 val，但這次不會影響到 b，因為它們現在指向不同的物件。

我

    上面同樣的例子，記憶體指向可以用圖示的方式做解釋嗎？


ChatGPT

    當然可以！讓我用圖示來解釋：

    首先，我們先來看一下一開始的情況，a 和 b 都指向同一個物件：

```yaml
ListNode: a, b
   |
   v
[ 3 | ] --> null
```
    在這個情況下，a 和 b 都指向 [ 3 | ] 這個節點。

    接著，當我們將 b 設置為 c 時，b 將指向一個新的物件，而不是 a 所指向的物件：

```yaml
ListNode: a            ListNode: b
   |                          |
   v                          v
[ 3 | ] --> null          [ 10 | ] --> null
```


    現在，a 和 b 指向不同的物件，分別是 [ 3 | ] 和 [ 10 | ]。

    即使我們修改了 a 所指向的物件的值，b 不會受到影響，因為它們指向不同的物件。這就是為什麼在最後一部分中，a.val 和 b.val 的值分別是 15 和 10。

我

    是否可以你將程式碼寫出來，考我的理解程度

ChatGPT

    當然，以下是一些程式碼示例，您可以試著理解它們的執行結果：

```csharp
public class ListNode {
    public int val;
    public ListNode next;
    public ListNode(int val=0, ListNode next=null) {
        this.val = val;
        this.next = next;
    }
}

class Program {
    static void Main(string[] args) {
        // 示例 1: 值類型和參考類型的存儲方式不同
        int value1 = 10;
        int value2 = value1;
        value1 = 20;
        Console.WriteLine("value1 = " + value1); // 20
        Console.WriteLine("value2 = " + value2); // 10

        ListNode node1 = new ListNode(3);
        ListNode node2 = node1;
        node1.val = 5;
        Console.WriteLine("node1.val = " + node1.val); // 5
        Console.WriteLine("node2.val = " + node2.val); // 5

        // 示例 2: 物件之間的指向關係
        ListNode head = new ListNode(1);
        head.next = new ListNode(2);
        head.next.next = new ListNode(3);
        ListNode current = head;
        while (current != null) {
            Console.WriteLine("Node value: " + current.val); 
            current = current.next;
        }
        // Node value: 1
        // Node value: 2
        // Node value: 3

        // 示例 3: 物件引用的影響
        Person person1 = new Person("Alice");
        Person person2 = person1;
        person1.Name = "Bob";
        Console.WriteLine("person1.Name = " + person1.Name); // Bob
        Console.WriteLine("person2.Name = " + person2.Name); // Bob

        // 示例 4: 陣列中的物件引用
        int[] array1 = {1, 2, 3};
        int[] array2 = array1;
        array1[0] = 10;
        Console.WriteLine("array1[0] = " + array1[0]); // 10
        Console.WriteLine("array2[0] = " + array2[0]); // 10
    }
}

public class Person {
    public string Name { get; set; }
    public Person(string name) {
        Name = name;
    }
}
```
    這些示例包含了值類型和參考類型的存儲方式、物件之間的指向關係以及物件引用的影響。請試著運行這些程式碼片段，觀察它們的輸出，並試著理解每個示例中變數之間的關係。


## Value Type 與 Reference Type
ex：int為 Value Type
ex:array、object為Reference Type

圖示說明：

    待補


## call by Value / call by Reference



[Day24-C#-參數的傳遞方式-Call By Value/Call By Reference/Output parameter](<https://ithelp.ithome.com.tw/articles/10213241> "")

