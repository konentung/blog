---
title: "VS Code Debug launch.json 設定技巧"
date: 2025-12-30T20:20:05+08:00
lastmod: 2025-12-30T20:20:05+08:00
author: Konen Tung
cover: ""
categories:
  - 工具
tags:
  - vscode
  - debug
  - 開發工具
draft: false
---

VS Code Debug 模式下 launch.json 的正確設定方式，解決 .env 無法載入、模組找不到等問題。

<!--more-->

在 VS Code 使用 Debug 模式啟動前後端分離專案時，若專案目錄與 .vscode/launch.json 不在同一層，常會遇到 Debug 可啟動但 .env 無法載入、模組找不到等問題。本篇整理實務中最穩定的設定方式，適合直接套用於個人或團隊專案。

在 VS Code 使用 Debug 模式啟動後端專案時，常見遇到以下狀況：

後端專案資料夾與 .vscode/launch.json 不在同一層

Debug 可以啟動，但出現：

- 無法 import module
- .env 沒有成功載入
- 環境變數讀取失敗（如 os.getenv、BaseSettings 等）

## 專案結構範例

```
workspace-root/
├─ backend/
│  ├─ app/
│  │  ├─ __init__.py
│  │  └─ main.py
│  ├─ .env
│  └─ venv/
└─ .vscode/
   └─ launch.json
```

## launch.json 正確設定（核心解法）

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "FastAPI Debug",
      "type": "python",
      "request": "launch",
      "module": "uvicorn",
      "cwd": "${workspaceFolder}/backend",
      "envFile": "${workspaceFolder}/backend/.env",
      "args": [
        "app.main:app",
        "--reload"
      ],
      "jinja": true
    }
  ]
}
```

| 設定 | 說明 |
|------|------|
| module | 使用 python -m 啟動對應模組 |
| cwd | 指定後端專案根目錄 |
| envFile | 明確指定 .env 路徑 |
| args | 啟動參數需以 cwd 為基準 |
