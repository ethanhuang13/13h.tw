---
layout: post
title: 如何管理 Xcode 版本才不會害到自己跟團隊
---

身為一個 iOS 工程師，我們應該對自己的開發工具有完整的掌握。最常使用的就是 Xcode。

我注意到開發者很常踩到 Xcode 在安裝、版本選擇方面的坑，所以決定來分享一下自己是怎麼管理 Xcode 版本。

## 安裝與下載

### 不要透過 Mac App Store

開發者最常犯的錯誤大概就是用 Mac App Store 下載 Xcode 了。使用 MAS 看似方便，但是後面會有各種無法掌握的因素。比如說：

#### 下載不了...

類似的抱怨在 Twitter 上隨便找都一堆。

<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

<blockquote class="twitter-tweet" data-partner="tweetdeck"><p lang="zh" dir="ltr">更新了一个星期的 xcode还没成功……</p>&mdash; Jia (@deepjia) <a href="https://twitter.com/deepjia/status/1183388230734897154?ref_src=twsrc%5Etfw">October 13, 2019</a></blockquote>

<blockquote class="twitter-tweet" data-partner="tweetdeck"><p lang="zh" dir="ltr">连续两个星期没法从 MAS 里安装 Xcode 之后，我选择： <a href="https://t.co/Ha1za3fTBO">pic.twitter.com/Ha1za3fTBO</a></p>&mdash; 迟先生的星星球 (@iskyzh) <a href="https://twitter.com/iskyzh/status/1184471967736291330?ref_src=twsrc%5Etfw">October 16, 2019</a></blockquote>

#### 低能安裝過程...

<blockquote class="twitter-tweet"><p lang="zh" dir="ltr">幹你娘低能 Apple Store，Xcode 下載完跟我說要關閉 Xcode 才可以安裝，但我沒開 Xcode 所以想說先按取消再試一次，結果他給我重新下載...</p>&mdash; Haruka (@hirakujira) <a href="https://twitter.com/hirakujira/status/1175404511252250624?ref_src=twsrc%5Etfw">September 21, 2019</a></blockquote>

#### 下載失敗浪費空間...

<blockquote class="twitter-tweet" data-partner="tweetdeck"><p lang="zh" dir="ltr">Xcode 升級下載失敗就算了，每次安裝失敗還留一堆垃圾檔案在系統裡。<br><br>全部反安裝再試一次。</p>&mdash; OOBE (@OOBE) <a href="https://twitter.com/OOBE/status/1189181800242765825?ref_src=twsrc%5Etfw">October 29, 2019</a></blockquote>

#### 正要用的時候，自己手賤或是系統犯賤幫你更新...

我覺得這個超慘的耶🤦‍♂️

<blockquote class="twitter-tweet"><p lang="zh" dir="ltr">我說那個 Xcode 可以不要挑正要驗收時更新嗎⋯⋯<br>🤦‍♂️🤦‍♂️🤦‍♂️</p>&mdash; 餿腐味粗工 (@joe_trash_talk) <a href="https://twitter.com/joe_trash_talk/status/1176769452320251904?ref_src=twsrc%5Etfw">September 25, 2019</a></blockquote>

#### 而且強迫症的你還糾結著那該死的紅點...

<blockquote class="twitter-tweet" data-partner="tweetdeck"><p lang="zh" dir="ltr">升上10.15.1终于把xcode的更新安装完了，终于不用见到那个该死的红点了。</p>&mdash; 工藤龍一郎 (@BakeCom) <a href="https://twitter.com/BakeCom/status/1189528574643982337?ref_src=twsrc%5Etfw">October 30, 2019</a></blockquote>

#### 其他缺點

- 同時只能保留一個版本
- 一直跳出更新提示

你完全可以避免這些問題😎，以下提供兩種方式。

### 直接從 Apple Developer 網站下載 Xcode

其實 Apple 官網一直有下載 `.xip` 壓縮檔版本 Xcode 的連結，但是藏得有點深。

下載頁面的首頁是 [https://developer.apple.com/downloads](https://developer.apple.com/downloads)。而列出下載檔的位置是在 [https://developer.apple.com/downloads/more](https://developer.apple.com/downloads/more)。都需要登入開發者帳號。

![](/assets/img/2019-11-01-developer-downloads.jpg)

要去按 **More**，是不是藏得有點深...

![](/assets/img/2019-11-01-developer-downloads-more.jpg)

是說，這邊最早還可以下載到 Xcode 3.2 呢。

自己下載唯一的缺點就是，通常這個版本會比 Mac App Store 還要晚個半天才會放上去。

但我通常都會在 Twitter 觀察一下災情，才決定要不要抓新版，所以沒差。

### 透過 xcode-install 套件管理 Xcode

如果你覺得手動下載、手動解壓縮好蠢，那麼來用 command line 吧。

[xcode-install](https://github.com/xcpretty/xcode-install) 是一個很方便的 Ruby 套件。

安裝 Xcode 11.0 只需要兩行：
```bash
gem install xcode-install
xcversion install 11.0
```

就會登入（使用跟 Fastlane 一樣的 Keychain 機制）、下載，並且解壓縮。

甚至可以列出所有可下載與已安裝的版本：
```bash
xcversion update
xcversion list
```

![](/assets/img/2019-11-01-xcversion-list.jpg)

## Xcode 與 iOS 相容性測試

（2020/06/23 更新：本段落舉例版號改成 WWDC20 推出的新版本，以利閱讀）

每次 Apple 發表新版 Xcode 的 beta 版以後，尤其是 WWDC 的年度大版本，開發者應該將 beta 版抓下來做專案的相容性測試。

我們應該要測試相容的有哪些呢？以下為了方便說明我們把時光假定為 beta 版期間。

以 2020 年發表的 Xcode 12 與 iOS 14 來說，相較於前一代的 Xcode 11 與 iOS 13，會有以下四種組合：

| | Xcode 11 | Xcode 12 beta |
| - | - | - |
| iOS 13 或更早 | A. 現況 🔁 | C. 向下相容 ⬇️
| iOS 14 | B. 向上相容 ⬆️ | D. 新東西 🆕

通常 A、C、D 這三種情境我們比較熟悉，也比較容易。

### A. 現況 🔁
專案在目前 Xcode 正式版的相容性，也就是現況。

### B. 向上相容 ⬆️
專案在舊版 Xcode 上 build 出來的，跑在新版的 iOS beta 裝置。比如 Xcode 11.5 正式版去連接 iOS 14 beta 裝置。

這一塊可以說是個大盲區。你想想看當新的 iOS 正式推出的時候，使用者可能就升級上去了，但你不見得已經準備好支援 iOS 14 的 app。就算準備好了，他們也不見得會更新 app。

這明明就是在新版系統正式推出以後，使用者最有可能遇到的情境。但是 **Apple 從來就沒有為了向上相容的測試提供方法**。把一台 iOS 14 的裝置接到 Xcode 10，會告訴你不支援，系統版本太新，沒辦法 run 在實機上。這樣子要怎麼確保向上相容呢？

幸好，要讓 Xcode 去支援它本來不支援的新版系統，只需一個關鍵—DeviceSupport。我們可以從新版 Xcode 裡面把對應的 DeviceSupport 資料夾，看是要用 symbolic link 還是複製一份的方式。我是比較推薦前者。

我寫了一個 [gist](https://gist.github.com/ethanhuang13/b9b4b875db9b49a124e2af194b97be68) 來做這件事情，裡面還有 watchOS 與 tvOS 的指令。你可能得依照自己的 Xcode 路徑來修改指令內容。

唉呀，其實我在 2017 年就寫過[類似的文章](https://medium.com/@ethanhuang13/從正式版-xcode-連到-beta-版裝置開發-d4a137c91618)了。

### C. 向下相容 ⬇️
專案在新版 Xcode build 出來以後，跑在舊版的 iOS 裝置。比如 Xcode 12 beta 連接 iOS 13 裝置。

WWDC 新版 Xcode 出來時，Apple 會希望你下載最新的 beta 版，來做向下相容的測試。直接把舊系統的裝置連到新版的 Xcode，通常安裝 app 不會有問題，我們要留意的是跑起來以後，新的 SDK 怎麼樣相容舊版系統，有沒有一些壞掉的情況。

**一般來說**向下相容比較不會有問題，因為 Apple 必須確保系統升級不會讓原有的應用程式無法使用。

而且除非你要升級 Xcode，不然這件事也沒那麼急。

### D. 新東西 🆕
專案對於新系統、新版 Xcode 的相容性。現有專案直接用新版 Xcode 打開看能否 build。比如 Xcode 12 beta 跑在 iOS 14 beta 裝置。

這邊主要看的是專案對於系統的相容性。越早版本的 beta 問題當然是越多。

但是除非你的產品非得要用到最新的 API，要不然 D 這個部份的相容性應該是最不急迫的。

就一個成熟的產品或是日常工作來說，我覺得處理的優先順序應該是 **A 現況 🔁 > B 向上相容 ⬆️ > C 向下相容 ⬇️ > D 新東西 🆕**。

2019 年大家都興沖沖地跑去玩 SwiftUI 或是 Combine，然後才發現坑超多。其實那些都是屬於 D 的部分，優先度最低🤣

以後 Apple 再發表新東西，我們最好還是吸取教訓，先搞定 A、B、C，再來玩玩具。

## 團隊協作

### 指定 Xcode 版本

有多個版本 Xcode 的話，用 `xcode-select` 來指定要使用的 Xcode 的路徑。這應該是基本功夫。
```bash 
sudo xcode-select -s /Applications/Xcode.app #路徑
``` 

### 在專案中鎖定 Xcode 版本

我建議在發布 app 時使用 Fastlane，就可以用 [`ensure_xcode_version`](https://docs.fastlane.tools/actions/ensure_xcode_version/) 來確保版本。

### 確定 Xcode 是沒有被動過手腳

你可能聽過 [XcodeGhost 事件](https://zh.wikipedia.org/wiki/XcodeGhost风波)。下載來路不明的 Xcode 是有可能抓到被駭過的版本。

使用 Fastlane 的 [`verify_xcode`](https://docs.fastlane.tools/actions/verify_xcode/#verify_xcode) 可以幫忙確認 Xcode 的 code sign，以及用 GateKeeper 檢查。

想要自己跑指令的話，也可以參考[這裡](https://github.com/fastlane/fastlane/blob/master/fastlane/lib/fastlane/actions/verify_xcode.rb)。

不過要注意的是，這個動作要跑好幾分鐘，比較建議是在出正式 Release 的 lane 再跑。

另外，如果因為前述的向上相容，而改過 DeviceSupport 資料夾的話，驗證會失敗。

### 我們到底要保留哪幾版 Xcode？

這完全是要看你手邊專案的狀況。三個版本不算誇張：

1. 前一個正式版，如果舊版 app 出了問題可能要回去看。比如說你舊版 app 的 Swift 版本是上一代
2. 目前的正式版，用在最近上架更新的 app
3. 最新的 beta 版，如果要使用一些新系統才有的 API

我以前也舉過一個[例子](https://13h.tw/2018/04/09/modern-ios-dev-life.html)。

## 結論

iOS 開發者的電腦硬碟要買大一點，MacBook Pro 要 512 GB 以上。

不是啦，講認真的：

- 不要用 Mac App Store 安裝 Xcode，從官網的 [More](https://developer.apple.com/downloads/more) 下載，或透過 [xcode-install](https://github.com/xcpretty/xcode-install) 管理
- 弄清楚相容性測試的優先順序
- 可以透過 Fastlane 幫助團隊管理 Xcode 版本

## 同場加映

### 空間清理工具

每次更新開發裝置的 iOS 版本以後，記得把電腦上舊的 cache 給清除。身為 Xcode 使用者，一次清出幾十 GB 也是很常有的事。

- 如果你偏好無腦解，[DevCleaner](https://apps.apple.com/tw/app/devcleaner-for-xcode/id1388020431?mt=12) 或 [Cleaner for Xcode](https://github.com/waylybaye/XcodeCleaner-SwiftUI)
- 如果你偏好自己來，[GrandPerspective](http://grandperspectiv.sourceforge.net)

### 跨版本安裝模擬器

- 皮樂的[手動安裝 iOS 模擬器到 Xcode](https://hiraku.tw/2019/09/4847/)
- 我寫的[在 Xcode 10 模擬器上跑 Xcode 9 build 的 app](/2018/09/14/build-xcode9-app-run-xcode10-simulator.html)

### 其他資料

- [#我會刷掉](https://twitter.com/ethanhuang13/status/1181897268363837440)
- [從 Xcode 正式版連到 iOS beta 版裝置](https://medium.com/@ethanhuang13/從正式版-xcode-連到-beta-版裝置開發-d4a137c91618)
- [weak self 0: 如果你想要浪費一個人的暑假](https://weakself.dev/episodes/0) 這集有聊到開發者該怎麼分配 WWDC 到正式版上架這段期間的時間與資源
- [weak self 9: 帶你親臨 iPlayground 現場](https://weakself.dev/episodes/9) 最後一段有講到不要用 Mac App Store 安裝 Xcode
- [weak self 13: 喬喬 Erasure](https://weakself.dev/episodes/13) 前面有聊到 xcode-install
- [Modern iOS dev life](https://13h.tw/2018/04/09/modern-ios-dev-life.html)
