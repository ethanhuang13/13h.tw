---
layout: post
title: iOS 也有深色模式—智慧型反相
---
2016 年，Apple 給 tvOS 10 增加了深色主題設定（[`UIUserInterfaceStyle`](https://developer.apple.com/documentation/uikit/uiuserinterfacestyle)*）、2018 年 macOS 在 Mojave 也新增了深色模式，甚至連 Safari/WebKit 都可以告訴網站去支援深色模式（[`prefers-color-scheme`](https://webkit.org/blog/8475/release-notes-for-safari-technology-preview-68/)）。但是 iOS 一直沒有全系統的深色主題或設定。

由於 iOS 的 UI 預設都是白底黑字或亮色系，大部分 app 如果不特別設計深色主題的話也就會是淺色，所以**把螢幕顏色反過來**就是一個建立深色模式的思路💡。

但是傳統的螢幕反相，就是單純地把輸出到螢幕的顏色反過來、黑白互換，類似於傳統底片的效果。遇到圖片就會慘不忍睹😂。直接拿來當深色模式是不堪用的。

> 螢幕顏色反相的設定在輔助使用裡面存在已久，但是我唯一聽過的使用情境，就是還在用傳統底片的攝影師，用相機 app 搭配反相模式來看她沖洗好的負片。

---
不過 iOS 11 新增了**智慧型反相**輔助功能。智慧型反相把 iOS 主畫面與 app icon 保留原本的配色，只是稍微降低飽和度。同時，**app 可以指定忽略哪些 UI 元件**。例如用來顯示圖片的 `UIImageView` 就不需要反相。對於大部分使用者來說，可以當作一個不錯的深色模式替代品。

把智慧型反相當作深色模式來思考的話，除了圖片以外，底色是深色的畫面就可以忽略反相。如果 app 本來就是以暗色為主的介面，那就可以全部忽略。以我公司 CATCHPLAY 的 app 為例，我們的主題一向是深色為主，因此可以把所有的元件都忽略掉智慧型反相。

要支援智慧型反相滿簡單的，就是把不要反相的 `UIView` 元件的 [`accessibilityIgnoresInvertColors`](https://developer.apple.com/documentation/uikit/uiview/2865843-accessibilityignoresinvertcolors) 設為 `true` 即可。

如果整個 app 都不要反相，在 `UIApplicationDelegate` 的 `didFinishLaunchingWithOptions` 方法設定 `UIView.appearance().accessibilityIgnoresInvertColors = true` 即可。

---
正常的顏色：

![Normal](/assets/img/2018-10-30-cp-normal.png)

智慧型反相的預設結果，效果跟經典反相一樣：

![Enable Smart Invert](/assets/img/2018-10-30-enable-smart-invert.png)

整個 app 的 UIView 都忽略經典反相，看起來大致相同。狀態列的顏色仍然是反過來的：

![Ignore Invert](/assets/img/2018-10-30-ignore-invert.png)

如果在意狀態列顏色的話，可以監聽系統通知 [`invertColorsStatusDidChangeNotification`](https://developer.apple.com/documentation/uikit/uiaccessibility/1615196-invertcolorsstatusdidchangenotif)，並用 [`UIAccessibility.isInvertColorsEnabled`](https://developer.apple.com/documentation/uikit/uiaccessibility/1615167-isinvertcolorsenabled) 來判斷使用者是否啟用反相，然後再指定狀態列的 style。這個判斷名稱雖然沒有寫 smart，但是我實測它只會在智慧型反相時回傳 true，在經典反相時則回傳 false。

---
雖然說叫做智慧型反相，其實也沒有多智慧🤣，就是可以指定部分 UI 元件不要反相而已。也許你還會想，既然照片的顏色顛倒不堪用，為什麼智慧型反相時，系統沒有預設把 `UIImageView` 忽略掉呢？大概是因為 `UIImageView` 可以用來顯示照片，也可以用來顯示圖形按鈕。即使 `UIImage` 有 [`renderingMode`](https://developer.apple.com/documentation/uikit/uiimage/1624122-renderingmode) 也不容易判斷，乾脆讓開發者自己決定。就像其他 accessibility 功能一樣，系統可以猜到大概，最後細節還是要留給開發者。

但這也導致絕大多數 app 的圖片在智慧型反相預設情況下很可怕，就連 iOS 11 初期版本的 WebView 與郵件也沒[支援正確的照片顏色](https://support.apple.com/en-us/HT208067#113)。開發者應該檢查一下自家的 app 在智慧型反相下的效果。

最後提供一個開發或測試的時候的小技巧，可以在`系統設定`➡️`一般`➡️`輔助使用`➡️最下面的`輔助使用快速鍵`勾選`智慧型反相`，這樣按三下裝置的實體按鈕，就可以快速切換。控制中心也可以放入`輔助使用快速鍵`項目。

---
補充資料：

> *iOS 12 也新增了跟 tvOS 10 一樣的[`UIUserInterfaceStyle`](https://developer.apple.com/documentation/uikit/uiuserinterfacestyle)，但是沒有作用。

> 開啟智慧型反相時，在裝置上螢幕截圖還是會截出正常的圖片。如果要截圖的話要接上電腦用 Quick Time 來抓。

> `accessibilityIgnoresInvertColors` 也可以在 Interface Builder 設定，在 User Defined Runtime Attributes 新增 keyPath 並設為 `true` 即可。細節可參考[這篇文章](https://duan.ca/2017/12/20/smart-invert-support-for-you-app/)。