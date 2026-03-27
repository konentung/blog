---
title: "Anaconda 安裝與 Conda 指令速查"
date: 2025-03-07T16:02:13+08:00
lastmod: 2025-03-07T16:02:13+08:00
author: Konen Tung
cover: "https://hackmd.io/_uploads/SkpTNM4cJg.png"
categories:
  - 程式語言
tags:
  - python
  - conda
  - 環境建置
draft: false
---

Anaconda的安裝以及環境指令的教學

<!--more-->

## 安裝Anaconda

到[Anaconda官網](https://www.anaconda.com/download)下載並安裝

選擇skip
![image](https://hackmd.io/_uploads/SkpTNM4cJg.png)

選擇你的作業系統做下載(以win做範例)
![image](https://hackmd.io/_uploads/rykkHMVqJg.png)


## Conda指令

確認Anaconda版本
```shell
conda -V
```

查看目前所有conda虛擬環境
```shell
conda env list
```

建立conda虛擬環境
```shell
conda create --name <虛擬環境名稱> python=X.X.X
```

啟用指定的conda虛擬環境
```shell
conda activate <虛擬環境名稱>
```

停用目前的conda虛擬環境
```shell
conda deactivate
```

刪除指定的conda虛擬環境
```shell
conda remove --name <虛擬環境名稱> --all
```

安裝指定套件
```shell
conda install <套件名稱>
```

安裝特定版本的套件
```shell
conda install <套件名稱>=X.X.X
```

移除已安裝的套件
```shell
conda remove <套件名稱>
```

查看虛擬環境內已安裝的套件
```shell
conda list
```

更新已安裝的套件
```shell
conda update <套件名稱>
```

更新所有已安裝的套件
```shell
conda update --all
```

匯出目前環境的套件列表（產生 `environment.yml`）
```shell
conda env export > environment.yml
```

使用 `environment.yml` 建立新環境
```shell
conda env create -f environment.yml
```

設定 Conda 為默認 Python 套件管理工具
```shell
conda config --set auto_activate_base false
```

清除 Conda 暫存檔案以釋放空間
```shell
conda clean --all
```

回復 Conda 預設設定
```shell
conda config --remove-key auto_activate_base
```
