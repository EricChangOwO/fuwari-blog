---
title: 在 Windows 裡面的 VSCode 編譯並執行 C / C++ 但用的是 WSL 環境
published: 2025-04-12
description: '這篇應該會非常 user friendly 所以高手應該可以直接跳著看，或著不看'
image: ''
tags: []
category: ''
draft: false 
lang: ''
---
#### 這篇應該會非常 user friendly 所以高手應該可以直接跳著看，或著不看

### 前言

會想寫這個是因為看到了超多文章有在講這個，但不是太舊了，就是沒有更新
所以找了個~~簡單一點的~~ (並沒有)，雖然要安裝 [WSL](https://zh.wikipedia.org/zh-tw/%E9%80%82%E7%94%A8%E4%BA%8ELinux%E7%9A%84Windows%E5%AD%90%E7%B3%BB%E7%BB%9F) 但對新手應該是不會太難吧，畢竟 VSCode 自己的[官方教學](https://code.visualstudio.com/docs/cpp/config-mingw)也有叫你用 MSY32 去裝，然後這樣還可以多多學習一下 Linux 的用法，非常好！！

### 先放個成品照
![image](https://i.imgur.com/bTz56dT.png)




## 1. 安裝 WSL
首先，對著你的 Windows 按鈕按下滑鼠的右鍵，打開系統管理員的終端機

![image](https://i.imgur.com/cnO8V08.png)

開啟之後輸入
```
wsl --install
```

之後照著指示走，中途可能會叫你重新開機，就按照他的步驟做，直到你看到終端機有多出一個 Ubuntu 的欄位給你選擇，恭喜你就安裝成功了！

![image](https://i.imgur.com/CODpXbC.png)

然後這時候你打開他可能會要你設定使用者名稱和密碼，請你好好記住
然後如果過程沒有出現問題的話，這樣你的電腦裡面就會多出一個 Ubuntu 的子系統環境了！

**那如果你安裝失敗的話 請你根據他給的你的錯誤訊息去找找哪裡有問題**

## 2. 調整 VSCode
首先你要有 VSCode 安裝在你電腦裡，不然我不知道你要怎麼做下一步
接下來打開他，並且來到擴充插件的頁面來安裝 Code Runner

### 2-1 安裝 Code Runner 插件

![image](https://i.imgur.com/eu6ADGS.png)


> 這裡簡單介紹一下 Code Runner 在幹嘛：
> 總而言之就是你把你的 MinGW 的 bin 資料夾加進環境變數的 Path 裡面，但這樣子每次還是得自己去呼叫 `g++ a.cpp` 這類的指令，有了 Code Runner 之後他就可以直接幫我們省去這個打指令，只要按一個按鈕就可以用了！

### 2-2 調整終端機設定

安裝好之後，首先先設定一下預設的終端機設定檔，這樣 Code Runner 按下 Run Code 按鈕之後才會去用 WSL 環境去做執行，不然預設的話還是走 `cmd.exe`

先來按加號右邊的按鈕，選取預設的終端機預設設定檔
![image](https://i.imgur.com/QstARdu.png)
然後接下來就會跳出這個視窗
![image](https://i.imgur.com/HYZRe20.png)
選擇 WSL 這樣他就會變成預設

### 2-3 Code Runner 設定

首先到設定這裡來，如圖片上的按鈕
![image](https://i.imgur.com/YLH6CXG.png)
這時候你就會發現右上角多了一個檔案的按鈕，按下去你就可以到 `settings.json` 的編輯頁面來
![image](https://i.imgur.com/1sCC7Kk.png)
接下來你應該會看到類似這樣的畫面，然後你的一定跟我長不一樣，這是正常的
![image](https://i.imgur.com/K6MrKOS.png)


然後接下來我們只需要把三行的設定加進去

```
    "code-runner.terminalRoot": "/mnt/",
    "code-runner.runInTerminal": true,
    "editor.mouseWheelZoom": true,
```

加完之後記得存檔！
**然後解釋一下那三行是幹嘛的**

> 第一行是切換執行目錄到 /mnt/ 底下，因為 `C:\` 掛載在 /mnt 底下 (必要)
> 第二行是跑在終端機裡面，因為這樣才能輸入文字 (必要)
> 第三行是我自己多加的，但你不覺得用 `Ctrl + 滾輪` 放大很棒嗎 (可選)
> 
## 3. 在 Ubuntu 裡面安裝 gcc / g++
跟上面一樣，打開你的終端機，然後切換至 Ubuntu 接下來就開裝

```
sudo apt update && sudo apt install g++
```

然後照著指示安裝，之後重開你的 VSCode 然後隨便開一個 cpp 檔案
右上角的 Run Code 按下去

### 恭喜你安裝成功
![image](https://i.imgur.com/bTz56dT.png)

## 後記
Windows 就很麻煩，就這樣
如果要懶惰的話請你去裝 **DEV C++** 或著 **Visual Studio**
然後我很懶惰，沒人叫我的話應該是不太會來更新文章，希望就這樣就好

##### 然後我超爛，文章裡面有任何解釋錯誤請直接連絡[我](https://linktr.ee/e0pwr)
##### 我會盡我最大的能力做修正，麻煩請各位電神指點指點！

---
#### 參考資料
1. [windows 下vscode coderunner+bash 编程](https://blog.csdn.net/rush_mj/article/details/124028347)
2. [Using C++ and WSL in VS Code](https://code.visualstudio.com/docs/cpp/config-wsl)

