---
layout: post
title: 在 Xcode 10 模擬器上跑 Xcode 9 build 的 app
---
如果還不急著切換到 Xcode 10，可以使用這個技巧來測試 Xcode 9 build 出來的 app，跑在 iPhone XS Max / XR 模擬器的情況：

1. 用 Xcode 9 選一個模擬器為目標來 build
2. 在 Products/OOO.app 上按右鍵、Show in Finder
3. 打開 Xcode 10 的 Simulator app，Hardware 選 XS Max 或 XR
4. 從 Finder 裡把 OOO.app 拖拉到上述的 Simulator 視窗裡（會安裝）
5. 點開 app 來觀察狀況

以上方法來自[這篇文章](https://medium.com/@hacknicity/ipad-navigation-bar-and-toolbar-height-changes-in-ios-12-91c5766809f4)的 Wait, What Did You Say? 那一段。