---
layout: post
title: iPhone XS Max 與 Xcode 9 相容性分析
---
iPhone XS / XS Max 開賣當天我跟同事 [Toby](https://twitter.com/HsuToby) 有拿到 Max 來做測試。如同他[分享的文章](https://medium.com/@tobyhsu/xcode-9-10-build-出的-app-在-iphone-max-的差異-1-f60062d5a7c2)，iPhone XS Max 在跑 iOS 11 SDK (Xcode 9) build 的 app 會用**放大模式**來顯示。

這個放大模式怎麼來的呢？就是根據 iPhone X 的顯示內容。因為兩個螢幕的長寬比一樣，所以內容是等比例放大的。仔細比較一下還發現更多的細節。先講結論：

iPhone XS Max 在`系統設定 > 螢幕顯示與亮度 > 顯示畫面`設定為**放大模式**時，不管是用哪一版的 SDK build，app 的顯示內容都會跟 iPhone X 一樣，只有**狀態列**會略有不同。而在**一般模式**時，app 必須用 Xcode 10 才能在 XS Max 上顯示原生解析度。

---
以下影片是 [Knil](https://github.com/ethanhuang13/knil) 這個 app\* 分別在五種狀態下的樣貌，可以注意到 1~4 的顯示內容相同，只有狀態列不同。而 5 則是原生解析度。

1. iPhone X
2. iPhone XS Max, Xcode 9 (iOS 11 SDK), 放大模式
3. iPhone XS Max, Xcode 10 (iOS 12 SDK), 放大模式
4. iPhone XS Max, Xcode 9 (iOS 11 SDK), 標準模式
5. iPhone XS Max, Xcode 10 (iOS 12 SDK), 標準模式

![iPhone X & XS Max compare](/assets/img/2018-09-21-iphonex-xsmax-compare-1080p.mov)

---
另外一點，A12 晶片用了一個叫做 **arm64e** 的新 architecture ，用 Xcode 9 要 build & run 到 XS Max 上會顯示以下資訊：

![Xcode 9 run on iPhone XS Max](/assets/img/2018-09-21-arm64e_error.png)

依照錯誤訊息在 build setting 加上 arm64e 也沒用，因為 Xcode 9 就是不支援。

結論就是，如果要支援 iPhone XS Max 的原生解析度或是進行 Max 的實機開發，一定要用 Xcode 10（廢話🤣）。但如果暫時還維持 Xcode 9 的話，使用者會看到 iPhone X 放大版的內容。放大的程度並不明顯，不仔細看是看不出來的。

---
\* [Knil](https://github.com/ethanhuang13/knil) 是我撰寫的開源且免費的 Universal Links 測試工具