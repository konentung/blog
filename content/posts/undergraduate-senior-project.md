---
title: "畢業專題開發手冊"
date: 2025-03-07T17:06:25+08:00
lastmod: 2025-03-07T17:06:25+08:00
author: Konen Tung
cover: "https://hackmd.io/_uploads/HkfSAsinyl.png"
categories:
  - 畢業專題
tags:
  - python
  - django
  - 畢業專題
draft: false
---

畢業專題的開發手冊，讓組員知道如何進行開發的流程，也讓我體驗一次PM究竟有多難當

<!--more-->

## 開發環境建置

### 安裝Python
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

### 安裝VScode
1. 至[VSCode官網](https://code.visualstudio.com/)下載安裝檔
![image](https://hackmd.io/_uploads/r1HulXz_yg.png)
2. 開啟安裝檔選擇我同意並繼續下一步
![image](https://hackmd.io/_uploads/SJdhx7zOJe.png)
3. 選擇下一步
![image](https://hackmd.io/_uploads/BkmkbQzdyx.png)
4. 選擇下一步
![image](https://hackmd.io/_uploads/B1afZmGOke.png)
5. 按照圖中選項勾選後進行下一步
![image](https://hackmd.io/_uploads/rk8tWQGuJx.png)
6. 點擊安裝
![image](https://hackmd.io/_uploads/Bkhs-XGukl.png)
7. 這樣就安裝完成啦
![image](https://hackmd.io/_uploads/HJOR-XGOyx.png)

### 建立虛擬環境
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

### Django指令說明
1. 建立專案
```shell
django-admin startproject <專案名稱>
```
2. 建立APP
```shell
python manage.py startapp <APP名稱>
```
3. 專案設定
```python
# 將預設的帳號APP設定成自己建立的物件
AUTH_USER_MODEL = 'accounts.Student'

# 新增建立好的APP
INSTALLED_APPS = [
    'whitenoise.runserver_nostatic', # 新增whitenoise讀取靜態檔案
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    '你的APP名稱',
]

# 新增whitenoise
MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'whitenoise.middleware.WhiteNoiseMiddleware', # 新增whitenoise
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]

# 修改Template路徑
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [BASE_DIR / 'templates'], # 加入template路徑
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]

# database修改成使用postgresql
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',  #PostgreSQL
        'NAME': os.getenv('DATABASE_NAME'),  #資料庫名稱
        'USER': os.getenv('DATABASE_USER'),  #資料庫帳號
        'PASSWORD': os.getenv('DATABASE_PASSWORD'),  #資料庫密碼
        'HOST': os.getenv('DATABASE_HOST'),  #Server(伺服器)位址
    }
}

# 設定時區
TIME_ZONE = 'Asia/Taipei'

# 設定static路徑
STATIC_URL = '/static/'
STATICFILES_DIRS = [BASE_DIR / "static"]
STATIC_ROOT = BASE_DIR / "staticfiles"  # 這是 collectstatic 將收集靜態文件的目錄
```
4. 建立資料庫建構檔
```shell
python manage.py makemigrations accounts
python manage.py makemigrations posts
```
5. 建立資料庫
```shell
python manage.py migrate
```
6. 建立超級使用者
```shell
python manage.py createsuperuser
```
7. 蒐集靜態檔案
```shell
python manage.py collectstatic
```

### 安裝Postgresql
1. 至[Postgresql官網](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads)下載安裝檔
![image](https://hackmd.io/_uploads/SJohaMROye.png)
2. 啟動安裝檔後，點擊下一步
![image](https://hackmd.io/_uploads/ByXNAfRO1l.png)
3. 輸入使用者的資料庫密碼(要記得，這會是後續連線的環境變數)
![image](https://hackmd.io/_uploads/HkoCRGA_yg.png)
4. 確認是否有佔port(基本上沒設定過資料庫不會佔port)
![image](https://hackmd.io/_uploads/B1Hzy7Rdkl.png)
5. 點擊finish
![image](https://hackmd.io/_uploads/H1YkxQ0dke.png)
6. 選擇最新版本
![image](https://hackmd.io/_uploads/ByHWe7Rdyg.png)
7. 如果已經安裝了，點擊cancel，沒有安裝則需勾選並點擊next安裝
![image](https://hackmd.io/_uploads/S1dHxQ0O1e.png)
![image](https://hackmd.io/_uploads/Sykux7Au1l.png)
8. 開啟pgadmin，點擊左邊的server會需要你登入，密碼就是一開始安裝時輸入的密碼
![image](https://hackmd.io/_uploads/rJU--Q0_kl.png)
![image](https://hackmd.io/_uploads/HkvbbmROJx.png)
9. 右鍵點及database後選擇create database，並輸入database名稱，資料庫就建立完成了
![image](https://hackmd.io/_uploads/rJoNZXROkx.png)
![image](https://hackmd.io/_uploads/B1i8-mR_1g.png)

## git流程

1. 分支簡介
為什麼需要使用git?
使用git可以有效率的管理不同工程師修改的程式碼，也比較方便管理整個專案
每個工程師在自己本機端修改程式碼之後再推送到遠端，管理程式碼的就可以確認你的程式碼正不正確再併入，這樣就不會有萬一錯誤了就無法還原到舊版本的問題
![image](https://hackmd.io/_uploads/HyNvXyMKJx.png)

2. sourcetree安裝
    1. 至[sourcetree官網](https://www.sourcetreeapp.com/)下載sourcetree安裝檔
    ![image](https://hackmd.io/_uploads/Hyo977R_1x.png)
    2. 啟動安裝檔，選擇skip
    ![image](https://hackmd.io/_uploads/HkGSfQAOyg.png)
    3. 如果有安裝過git會自己找到git的位置，並選擇Next
    ![image](https://hackmd.io/_uploads/rJg6_z7R_kg.png)
    4. 安裝完tool選擇Next
    ![image](https://hackmd.io/_uploads/Sy83MmRdke.png)
    5. 輸入github的email後選擇Next
    ![image](https://hackmd.io/_uploads/r1FmmXCu1g.png)
    6. 他會跳出一個視窗問你需不需要建立ssh-key做連線，可以選擇no
    7. 跳出應用程式就是安裝完成了
    ![image](https://hackmd.io/_uploads/SJxw7X0_yg.png)

3. clone專案至本機
![image](https://hackmd.io/_uploads/HJs0XX0O1x.png)
![image](https://hackmd.io/_uploads/rkpM4QRdyl.png)

4. 建立新的branch
![image](https://hackmd.io/_uploads/SytSEXCu1g.png)

5. 選取改動的檔案進行commit
![image](https://hackmd.io/_uploads/ryvAVXRdkx.png)

6. 選取要push的分支
![image](https://hackmd.io/_uploads/Hk1lH7ROJe.png)

7. 到遠端建立pull request
![image](https://hackmd.io/_uploads/HJzMrm0dkg.png)
![image](https://hackmd.io/_uploads/B1HEr70Oyx.png)

8. force push
![image](https://hackmd.io/_uploads/BkVIS70ukx.png)
![image](https://hackmd.io/_uploads/rkOvBQAuJl.png)

## 設定環境變數
1. 點擊新增檔案，名稱為`.env`
![image](https://hackmd.io/_uploads/BkRKH7AdJg.png)
2. 新增以下環境變數
```
SECRET_KEY = <django專案的secret key，可以自己先建一個複製過來>
DATABASE_NAME = <你設定的database名稱>
DATABASE_UAER = <預設是postgres，要看你有沒有修改>
DATABASE_HOST = 'localhost'
DATABASE_PASSWORD = <你安裝postgresql設定的password>
DATABASE_PORT = <預設是5432，要看你有沒有修改>
CSRF_TRUSTED_ORIGINS_URL = <你的對外網址的URL，如果沒有先隨便填一個即可>
OPENAI_API_KEY = <OPENAI_API_KEY>
```

## 設定python debugger
![image](https://hackmd.io/_uploads/ByVASm0O1e.png)
![image](https://hackmd.io/_uploads/ByHJL7Cdkl.png)
![image](https://hackmd.io/_uploads/SkdeUXAOkg.png)
![image](https://hackmd.io/_uploads/ByF-LXAdJx.png)

## Azure雲端部屬

> Reference：[開始使用 Git 管理專案](https://wellstsai.com/post/git-tutorial-init/)
