---
title: "Django 全端網頁開發入門"
date: 2025-03-07T15:13:04+08:00
lastmod: 2025-03-07T15:13:04+08:00
author: Konen Tung
cover: "https://hackmd.io/_uploads/ByQdBXuoyl.png"
categories:
  - 全端網頁
tags:
  - python
  - django
  - 網頁開發
draft: false
---

使用Django進行全端網頁開發，基礎的前置教學

<!--more-->

Django是一個高階的Python網頁框架，專為快速開發而設計，它內建了許多常見的功能，讓開發者能夠專注於邏輯的編寫。Django的物件關聯對應（ORM）系統，使開發者能夠輕鬆操作資料庫，免去手動編寫SQL查詢語句的麻煩。同時，Django也提供了用戶認證系統，開發者可以輕鬆實現用戶註冊、登入與權限管理，這大大提高了開發效率。這篇要交大家怎麼用Django製作一個有後台的網頁

## 建立Django開發環境

由於使用的是Python，所以需要先建立Python的虛擬環境

1. 建立Python虛擬環境
    > 可以參考我的[Python Venv 筆記](/notes/python-beginner/)

2. 安裝Django套件
    ```bash
    pip install django
    ```

## 建立Django預設伺服器

前面已經完成開發環境的建置了，接下來就要用指令建立一個Django的專案了

1. 建立Django專案
    在cmd切換到你要建專案的路徑後，輸入下面的指令
    ```bash
    django-admin startproject <專案名稱>
    ```

2. 建立APP
    先進入專案的資料夾後，再輸入下面的指令
    ```bash
    cd <專案名稱>
    python manage.py startapp <APP名稱>
    ```

3. 建立靜態檔案資料夾
    一樣在專案的資料夾底下，輸入下面的指令，template對應到的是HTML，static則是css以及javascript
    ```bash
    md template
    md static
    ```

4. 建立資料庫
    Django有預設使用sqlite3作為資料庫，可以直接拿來做使用，如果不想用sqlite3的也可以使用Postgresql等sql資料庫
    ```shell
    # app名稱可有可無
    python manage.py makemigrations <APP名稱>
    python manage.py migrate <APP名稱>
    ```
    若要使用postgresql則需要在migrate前先修改Django專案底下的`setting.py`

    修改範例
    ```python
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.postgresql',  #PostgreSQL
            'NAME': '資料庫的名稱',
            'USER': '資料庫帳號',  # 預設是posgres
            'PASSWORD': '資料庫密碼',  # 安裝時設定的密碼
            'HOST': 'localhost',  #Server(伺服器)位址
        }
    }
    ```

5. 架設預設伺服器
    在專案資料夾內的路徑執行下面的指令運行伺服器
    ```shell
    python manage.py runserver
    ```

## Django專案設定
在Django執行伺服器的程式前，我們需要修改`setting.py`的路徑和APP，才可以進到我們建立的資料夾內讀取資料

1. 新增建立好的APP
    ```python
    # 新增建立好的APP
    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        '你的APP名稱',
    ]
    ```

2. 修改template路徑
    ```python
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
    ```

3. 設定時區
    ```python
    # 設定時區
    TIME_ZONE = 'Asia/Taipei'
    ```

4. 新增static路徑
    ```python
    # 設定static路徑
    STATIC_URL = 'static/'
    STATICFILES_DIRS = [    #加入static路徑
        BASE_DIR / 'static'
    ]
    ```

## Django專案的view與url

1. 在templates中建立一個簡單的HTML
```html
<p>Lorem ipsum dolor sit amet.</p>
<p>Ullam sunt sed eligendi a!</p>
<p>Vero unde itaque ex animi?</p>
<p>Fugit exercitationem consequuntur vitae nostrum.</p>
<input type="text" style="text-align: center;"></body>
```

2. 在views.py中新增呼叫的HTML頁面
```python
def index(request):
    return render(request, 'index.html')
```

3. 在urls.py中新增對應到的路由
```python
from django.contrib import admin
from django.urls import path
import posts.views as posts_views # import view

urlpatterns = [
    path('admin/', admin.site.urls),
    path('/', posts_views.index), # 設定路由為此時執行的python view function
]
```

> Reference：https://docs.djangoproject.com/en/4.2/
