---
layout: post
title: FoundationDB
---
蘋果今天將一套 noSQL 資料庫軟體 [FoundationDB](https://www.foundationdb.org/) 給[開源](https://github.com/apple/foundationdb)出來。這個名字很蘋果。釋出的版本是 5.1.5，看來有點歷史了，但之前沒聽過。出於好奇查了一下它的背景。

FoundationDB 本是一間 startup，以及同名開源資料庫軟體。蘋果在 2015 年把這間公司買下後把軟體閉源，作為內部使用。現在又重新開源起來。

（根據當年 Business Insider 的[報導](http://www.businessinsider.com/why-apple-bought-foundationdb-2015-3)，蘋果收購與閉源 FoundationDB，造成不少公司的麻煩啊...）

至於 FoundationDB 軟體本身是幹嘛呢？資料庫我實在不是很懂，不過看了一些[介紹](https://2014.nosql-matters.org/cgn/wp-content/uploads/2014/05/Jennifer-Rullmann-NoSQL-and-ACID.pdf)，它擅長做大型分散式服務，不僅高效、有彈性，而且還具有硬體成本優勢。

據說蘋果是把它用在 iMessage 等大型服務的設施上（品質應該比什麼 UIKit、Swift、Xcode 之類的好得多吧 😂）。既然重新開源了，可以觀察一下。
