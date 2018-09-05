---
layout: post
title: git 不能保證專案在每台電腦上的狀態完全一樣
---
A quick reminder for iOS dev: git status clean != everything the same between 💻 machines 🖥:

- Files in .gitignore: Non-shared Scheme/Workspace settings 🛠
- Empty folders: Search Paths 👀
- Case-insensitive FS: Change name case of files in .xcassets, crash on #imageLiteral 💥

---
git 不能保證專案在每台電腦上的狀態完全一樣。以我曾遇過的坑為例：

- 列在 .gitignore 的檔案：scheme 或 workspace 的設定，如果不是 shared，每台電腦可以完全不一樣。天差地遠
- 空的資料夾：同事換了 framework 的位置，但 Header Search Paths 設定沒拿掉舊的。他的電腦可以 build，我 pull 後卻不行，因為我的空資料夾還在
- 檔名不區分大小寫的檔案系統（Mac 預設）：把 xcassets 底下的檔案大小寫改掉。git 看不出來差異，build 得過，但是 runtime 時 #imageLiteral 這種 code 會 crash

不是要提出解法，只是講一下有這些坑
