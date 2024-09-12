English | [繁體中文](README_TCH.md)
# I found a awesome bakin extractor
After several months. I've found an awesome extractor by a clever engineer: [Bakin Extractor](https://github.com/HNIdesu/BakinExtractor/tree/main)

* How to use：
```bash
python unpack.py rbpack_path output_directory
```
# BakinUnpack
A repo for researching how to unpack games made in rpg develop bakin.

# Why am I doing this?
RPG Developer Bakin is a new game makeing engine.

Apearly there is nothing on the internet to show how to unpack game file of bakin games.

I wondered how bakin packed game files and make its own struct, so I started to research their encoding and game files.

# How to start?
I know little about bakin. So I googled it and asked some of my friends who also know little about bakin.

All I got is that bakin is a new version of SGB, also known as Smile Game Builder.

There is less bakin discussion on internet. But there is more discussion about SGB.

> This section is based on [a tweet from x](https://twitter.com/KerokeroCoder/status/1120027976320421888).
> Also some of my inference.
SGB uses a special file format called ```.sgbpack```. And it has a certain pattern in its encoding:
* In the early edition of SGB using zip to pack its game file.
  * But it changed the file header from zip: ```50 4B 03 04 14 00 00 00``` to its own header: ```59 55 4B 41 52 50 4B 47 (YUKARPKG)```
* But soon official changes were made to the method of encoding:
  * ```53 47 42 44 41 54 00 01 (SGBDAT)```
  * Nobody knows how to deal with it.
  * And there is a high chance that Bakin still uses this encoding.

In bakin I assume it uses ```.rbpack``` to pack game files.
* I found that the header is ```42 4b 4e 50 41 4b (BKNPAK)```.
![rbpack_hex](image/rbpack_hex.png)

# temp file
I found out that bakin will create temp files during games at the windows temp path:
* ```C:\Users\{username}\AppData\Local\Temp\bakin_engine_tmp```

There are many ```.rbr``` files. Still have no clue how to deal with it.
![temp_files](image/temp_files.png)
