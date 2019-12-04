---
layout: post
title: 重拾程式解題的樂趣 - Advent of Code
---

你有做過線上解題嗎？像是高中生軟體比賽會寫的 ACM Online Judge，或是有些軟體工作面試要求考演算法，而要刷的 [LeetCode](https://leetcode.com)。

我不喜歡寫這些，雖然富有挑戰性，說實在並不有趣。如果想要**享受純粹的解題樂趣，我不會去寫 LeetCode**。

直到最近我發現一個只在每年 12 月才會有的解題活動：[Advent of Code](https://adventofcode.com)。

它是一人專案，作者是 [Eric Wastl](http://was.tl/) ([@ericwastl](https://twitter.com/ericwastl))。這個活動從 2015 年以來已經是第 5 年了。

## 什麼是 Advent of Code

Advent 是天主教專有名詞，你可以簡單理解成「耶誕節倒數」（[維基百科](https://zh.wikipedia.org/wiki/將臨期)）。所以 [Advent of Code](https://adventofcode.com)（以下簡稱 AoC） 的活動是在每年的 12/1 到 12/25。

在這 25 天中，每天都會公布兩題（通常）要寫程式才能解決的題目。時間是台灣的下午一點。

第一題通常不會太難，而你要解開第一題以後才會看到第二題的題目，是第一題的變化。很有可能顛覆你前面的思路跟設定。我喜歡這種變化題的設計方式，可以打破**[慣性思維](https://zh.wikipedia.org/wiki/慣性思維)**。

實際解了幾題，我發現就解題樂趣而言，AoC 比 LeetCode 好玩很多。

LeetCode 的解題過程大致上是：

* 挑題目（有些要付錢）
* 理解題目（同時心裡想著，不會吧，這題是 Easy？）
* 在網頁介面上寫程式來：
	* 處理輸入的測試資料
	* 解題完回傳答案
* 送出程式碼讓 LeetCode 後台執行
* 要考慮到 edge cases
* 要考慮到執行時間，解完以後還會跟別人比較

而 Advent of Code 的解題過程則是：

* 有一個簡單的背景故事（例如聖誕老人被困在太陽系某處，你要幫助他 blah blah）
* 每天準時公布題目
* 一組資料
* 一個答案輸入框
* 解題方式隨意
* 第一題解完會有第二題
* 答錯的話要過一分鐘才能重試

以下說明 AoC 的幾個特色。

### 解題方式隨意

2019 Day 1-1 這題，其實我是在手機上複製貼上到 Numbers app 解的😆

因為它的題目非常簡單，大意是：

> 聖誕老人的太空船上的各種模組要消耗燃油。它列給你所有模組的重量，然後你用簡單的四則運算求出對應的燃料重量，再加總。

所以用試算表秒解。而且[不是只有我有這種想法](https://twitter.com/ohyes1h/status/1202048971616616448?s=20)。

### 變化題

當你把 1-1 解完以後，「故事」才會往下展開。看到 1-2 這題就有趣了：

> 原來你剛才忘記計算燃料本身的重量了。每次增加燃料的同時，你要再增加一定的燃料，如此反覆直到某個條件為止。

這就不能用原本的方式計算，所以我才打開電腦寫程式，順便重寫第一題。

邏輯變了，但資料沒有變。我只要調整計算方式。

### 比較少在處理資料，比較多在解題本身

在寫 LeetCode 時，有好一部分時間是在處理資料的輸入格式，這個部份特別無趣。

AoC 你可以隨意。因為資料只會有一組而且是公開的，不需要像 LeetCode 反覆嘗試來處理各種「規則有寫但看不到範例」的 edge cases。

每天的兩題共用同一份資料，所以即使第二題的邏輯不同，你初始處理資料的程式碼通常也可以沿用第一題。

這些條件與設計，就**讓人更專注在解題而不是處理資料格式**。

### 題目難度

2019 前面四天每天有越來越難的趨勢。

### 活動玩法

既然是玩法很自由的解題遊戲，你要怎麼做都可以。你可以跟高手比賽解題速度，每天下午一點公布題目後就開始寫。如果[前 100 名](https://adventofcode.com/2019/leaderboard)的話，會得到 (100 - N + 1) 點積分，可以累積積分來排名。但是排行榜上都是在幾分鐘內解完，我可能題目都還沒理解完呢😂

所以我的玩法是志在參加，有把題目都解出來就好。我是用 Swift + Playground。每解完一題就 commit 起來。

解完之後再去看討論。以後學了其他語言也可以回來解一次。

AoC 也支援私底下的排行榜，可以跟朋友同事切磋。

### 救命，解不下去

不確定題目意思可以跟我在 [Twitter](https://twitter.com/ethanhuang13) 討論。

凡是公開題目就會有公開解答。[GitHub](https://github.com/Bogdanp/awesome-advent-of-code) 有一些可以參考，[Reddit](https://www.reddit.com/r/adventofcode/) 也有很多討論。甚至還有人[靠 Siri 解題](https://www.reddit.com/r/adventofcode/comments/e5q63j/2019_day_1_did_someone_say_siri/)！？（1-1 還沒解完的不要看）

不過我覺得前幾天的第一題的難度真的沒有太高，可以多試幾次再去看討論。

### 費用

AoC 完全免費！甚至不用登入就可以看[題目](https://adventofcode.com)。

只要用 GitHub、Twitter 等註冊帳號就可以開始填答。

若你覺得這個活動很有趣，可以考慮[捐助](https://adventofcode.com/2019/support)，金額隨意。

### 歷史題目

我是從今年才開始玩的。但是 [2015-2018](https://adventofcode.com/2019/events) 也各有 25 * 2 題可以回去解。

## 結語

對你來說，線上程式解題是好玩、痛苦，或是苦樂參半的經驗？

前陣子在 Twitter 上有看到一陣在討論 LeetCode 怎麼刷、怎麼買（中文版比英文還便宜）。看到討論時，我比較有興趣的卻是，這種線上測驗的專案是怎麼做起來的啊？

等到我看到 [@ericwastl](https://twitter.com/ericwastl) 創造的 AoC 發現，這個專案是他一個人從頭搭建的，題目也都是自己想的。[他甚至說](https://adventofcode.com/2019/about)，為了避免法律爭議，即使寄給他題目的建議他也不會讀，免得不小心用上了這些點子。我覺得這位工程師以及 AoC 這個專案，甚至比解題本身甚至更有意思。

也許我們應該思考怎麼創造出題目，而不是只會解題而已？

總之，AoC 是一個很有趣的程式解題活動，有空的話一起來玩吧。

**可以來[我開好的 Leaderboard](https://adventofcode.com/2019/leaderboard/private)，輸入`747723-067e3e4b`加入**，已經有一些推友在上面了。我會把 anonymous user 移除，所以請記得到[設定](https://adventofcode.com/2019/settings)把自己的名稱顯示出來。

或者是只跟自己比也完全沒問題。

AoC 刷起來！

## 相關連結

* [About Advent of Code](https://adventofcode.com/2019/about)