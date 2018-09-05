---
layout: post
title: 簡單說一下 fastlane.ci
---
昨天 4/7 在 @johnlinvc 的大力協助之下，fastlane 開發團隊成員 Felix(@KrauseFx) 與 Josh(@taquitos) 在 iCHEF 樓下的場地介紹了 [fastlane](https://fastlane.tools) 與 [fastlane.ci](https://github.com/fastlane/ci)。

fastlane 大家比較熟悉，就是把行動應用開發中，主要跟認證簽署及發佈相關的流程（當然還有更多）給自動化，並且統統加入版控。優勢是開發工具的環境設定都可以在 repo 裡面一起管理。

這樣一來，就算你今天換個地點、換了一台電腦，或是來了新夥伴，只要能夠 checkout 就可以無縫接軌。這精神在其中的套件 match 尤其徹底發揮。（這會讓人想把整個系統會用到的設定都給版控化，不過這是另一個題目了）

基於同樣的理念，fastlane.ci 是把連續整合的流程也版控化。如果有用過 Jenkins 或其他 CI 系統就會知道環境設定有多麻煩，還很難管理。用 fastlane.ci 的話，原則上架設一台新的 CI 只要 checkout 就可以掛好所有設定，然後工作流程就可以繼續囉。

fastlane.ci 前幾天才剛 alpha，昨天則是首次 live demo👏，Felix 跟 Josh 他們建議至少到 beta 再來用。當然你很勇敢也可以 alpha 就來玩，然後認真報 bug。fastlane.ci 是完全開源的，有興趣的話也可以 contribute。另外就是他們強調團隊會有 Google 的 designer，所以到時候一定會比某 CI 好看、好用😂

我個人是 fastlane 的長期愛用者，對 fastlane.ci 相當期待！
