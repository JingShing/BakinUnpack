[English](README.md) | 繁體中文
# 我找到一個很厲害的 Bakin 拆解工具
在幾個月後，我找到了一個聰穎的工程師的作品: [Bakin 拆解工具](https://github.com/HNIdesu/BakinExtractor/tree/main)

* 如何使用：
```bash
python unpack.py rbpack檔案路徑 輸出資料夾路徑
```
# BakinUnpack
一篇研究如何拆包 rpg develop bakin 的 repo。

# 我為什麼要做這個？
RPG Developer Bakin 是一個很新的遊戲引擎。

網路上沒有太多的資訊，更不用提如何拆包 Bakin 做的遊戲。

我很好奇 Bakin 這一個新穎的遊戲引擎是如何處理檔案和架構，所以我開始嘗試研究 Bakin 的檔案和編碼。

# 該如何開始？
我對Bakin了解有限，所以我嘗試了一些途徑，包括 google 以及向一些了解 Bakin 的朋友請教。

> 底下的內容參考了 [這篇推文的內容](https://twitter.com/KerokeroCoder/status/1120027976320421888) 。
> 還有一些我的猜想。
我得知Bakin是SGB（Smile Game Builder）的新版本，SGB使用一種特殊的文件格式稱為```.sgbpack```。它在編碼上有一定的模式：
* 在SGB的早期版本中，它使用zip格式來打包遊戲文件。
  * 但是它將zip文件標頭: ```50 4B 03 04 14 00 00 00```，更改為自己的文件標頭：```59 55 4B 41 52 50 4B 47 (YUKARPKG)```
* 但是官方很快就改動了編碼方法：
  * ```53 47 42 44 41 54 00 01 (SGBDAT)```
  * 我沒找到方法處理這種編碼。
  * 而 Bakin 可能仍在使用這種編碼。

在Bakin中，我假設它使用```.rbpack```來打包遊戲文件。
* 我發現它的文件頭是```42 4b 4e 50 41 4k (BKNPAK)```
* ![rbpack_hex](image/rbpack_hex.png)

# 暫存檔(Temp file)
此外，我還發現Bakin在遊戲運行期間會在Windows的臨時文件夾中創建臨時文件夾：
* ```C:\Users\{你的用戶名}\AppData\Local\Temp\bakin_engine_tmp```

在該臨時文件夾中有許多```.rbr```文件，但目前還不清楚如何處理這些文件。
![temp_files](image/temp_files.png)
