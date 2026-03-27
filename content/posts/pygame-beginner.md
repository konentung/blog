---
title: "Pygame 新手教學 — 用 Pygame 學物件導向"
date: 2025-03-07T16:17:40+08:00
lastmod: 2025-03-07T16:17:40+08:00
author: Konen Tung
cover: "https://hackmd.io/_uploads/H1059ionye.png"
categories:
  - 物件導向程式設計
tags:
  - python
  - pygame
  - 遊戲開發
draft: false
---

Pygame的新手教學，用pygame製作簡易的動畫並學習物件導向程式設計

<!--more-->

## Pygame簡介

`pygame`是一個Python的套件，主要用來創建 2D 遊戲和多媒體應用程式。它提供了一系列的功能，使開發者能夠輕鬆地處理圖形、音效、動畫以及使用者互動等方面。

## 建立開發環境

1. 確定使否已安裝Python
```shell
python --version
```

2. 開啟要建立環境的路徑
```shell
cd <路徑位置>
```

3. 輸入下方指令建立一個新的環境
```shell
python -m venv <環境名稱>
```

4. 進入虛擬環境路徑並啟動
```shell
cd <路徑位置>\Scripts
// 切換玩路徑後再執行
activate.bat
```

5. 切換完成後輸入下面指令安裝套件
```shell
pip install pygame
```

這樣就完成環境設定了！

## 基本Pygame指令

### 基本範例程式碼

下面是官方提供的基本的範例程式碼，包括最基本的pygame需要的東西。後面會依序介紹他們的功能。

```python
# Example file showing a basic pygame "game loop"
import pygame

# pygame setup
pygame.init()
screen = pygame.display.set_mode((1280, 720))
clock = pygame.time.Clock()
running = True

while running:
    # poll for events
    # pygame.QUIT event means the user clicked X to close your window
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # fill the screen with a color to wipe away anything from last frame
    screen.fill("purple")

    # RENDER YOUR GAME HERE

    # flip() the display to put your work on screen
    pygame.display.flip()

    clock.tick(60)  # limits FPS to 60

pygame.quit()
```

### 初始化pygame物件
```python
pygame.init()
```

### 顯示視窗

1. 設定顯示視窗物件（指定視窗的高度與寬度, flag是用來設定顯示模式的例如全螢幕等等）
```python
screen = pygame.display.set_mode((width, height), flags=0)
```

2. 設定視窗標題
```python
pygame.display.set_caption("遊戲標題")
```

3. 顯示更新畫面（可以選擇是否只更新哪個區塊，如未設定則整個畫面更新）
```python
pygame.display.update(rectangle=None)
```

4. 獲取畫面資訊（解析度，顯示方式等）
```python
info = pygame.display.Info()
```

5. 切換螢幕顯示方式（全螢幕↔視窗）
```python
pygame.display.toggle_fullscreen()
```

6. 設定視窗的icon
```python
icon = pygame.image.load('icon.png')
pygame.display.set_icon(icon)
```

### 設定畫布

`Surface`是Pygame中一個非常重要的物件，它代表了所有可顯示的畫面、圖像或介面元素。幾乎所有在Pygame中的圖形繪製，都是在`Surface`上進行的。

1. 創建Surface
```python
# 創建一個 800x600 的空白 Surface
surface = pygame.Surface((800, 600))
```

2. 繪製圖形和顏色
```python
surface.fill((255, 0, 0))  # 填充紅色
pygame.draw.rect(surface, (0, 255, 0), (50, 50, 200, 100))  # 繪製綠色矩形
```

3. Surface圖像
```python
image = pygame.image.load('image.png')
surface.blit(image, (0, 0))  # 將圖像繪製到surface上
```

4. 複製Surface
```python
new_surface = surface.copy()  # 複製 Surface
```

5. 旋轉Surface
```python
rotated_surface = pygame.transform.rotate(surface, 90)  # 旋轉 Surface
```

6. 透明度
```python
surface.set_alpha(128)  # 設定透明度（範圍：0-255，0為完全透明）
```

7. 繪製Surface到視窗中
```python
screen = pygame.display.set_mode((800, 600))
screen.blit(surface, (0, 0))  # 將 surface 繪製到螢幕
pygame.display.update()  # 更新螢幕顯示
```

前面說明完了最基本的語法，有了這些語法我們可以開始製作簡易的動畫了！

> Reference：https://www.pygame.org/docs/
