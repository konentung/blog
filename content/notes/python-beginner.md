---
title: "Python 環境建置與基本語法"
date: 2025-02-28T18:38:44+08:00
lastmod: 2025-02-28T18:38:44+08:00
author: Konen Tung
cover: "https://hackmd.io/_uploads/rJF6IMf_1g.png"
categories:
  - 程式語言
tags:
  - python
  - 環境建置
draft: false
---

Python Venv 環境建置與基本語法速查

<!--more-->

## Python安裝
1. 至[Python官網](https://www.python.org/downloads/)下載Python的安裝檔(本教學以3.12.2的版本為例)
    ![image](https://hackmd.io/_uploads/rJChcWG_kl.png)
2. 開啟下載後的安裝檔後先選擇加入環境變數後再點及安裝
    ![image](https://hackmd.io/_uploads/HkwjFZMOkl.png)
    ![image](https://hackmd.io/_uploads/rJF6IMf_1g.png)

    > 如果沒有加到環境變數怎麼辦?

    (1) 在設定中找到進階系統設定
        ![upload_d002a0ceb865b2ba0888dbe89275efb5](https://hackmd.io/_uploads/Hyfdjzzuyx.png)
    (2) 選擇環境變數
        ![image](https://hackmd.io/_uploads/SJKP5zfuJe.png)
    (3) 找到Path這個選項點兩下進去
        ![Screenshot_1](https://hackmd.io/_uploads/S1AtafGuJl.png)
    (4) 將前面安Python的路徑加入環境變數按下確定就完成了
        ![Screenshot_2](https://hackmd.io/_uploads/HJtik7f_1x.png)

## Python Venv
1. 在桌面新增一個資料夾venv
![image](https://hackmd.io/_uploads/Sko5zQzukx.png)
2. 開啟資料夾後在上面的路徑欄輸入cmd後按下enter開啟命令提示字元
![image](https://hackmd.io/_uploads/ByWaM7z_1x.png)
3. 輸入下面指令建立虛擬環境
```bash
python -m venv <環境名稱>
```
![image](https://hackmd.io/_uploads/SkEK77M_Jx.png)
4. 輸入指定切換路徑到activate的路徑
```bash
cd <環境名稱>/Script
```
![image](https://hackmd.io/_uploads/r1Mur7M_kx.png)
5. 輸入指令切換虛擬環境
```bash
activate.bat
```
![image](https://hackmd.io/_uploads/ryhkLQfOyx.png)
6. 安裝套件的指令(需先切換到requirements.txt的路徑位置)
```bash
pip install -r requirements.txt
```
7. 離開虛擬環境指令
```bash
deactivate
```

## Python 基本語法

* 輸入輸出
```python
# 印出Hello World
print("Hello World")
# 跳出輸入框可以輸入
input("輸入的提示訊息")
```

* 變數
```python
int a = 5
float b = 2.5
str c = '你好'
```

* 數學運算子
```python
X + Y
X - Y
X * Y
X / Y # X除以Y
X // Y # X除以Y並且只取整數解
X % Y # X除以Y的餘數
X ** Y # X的Y次方
```

* 流程控制
```python
if <條件>:
    <執行的程式碼>
elif<條件>:
    <執行的程式碼>
else:
    <執行的程式碼>
```

* for迴圈
```python
for <儲存的變數> in <序列型別的資料或數字>:
    <執行的程式碼>
```

* while迴圈
```python
while <成立的條件>:
    <執行的程式碼(需要有中止條件)>
```
