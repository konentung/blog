---
title: "Java 開發環境建置"
date: 2025-02-28T19:22:58+08:00
lastmod: 2025-02-28T19:22:58+08:00
author: Konen Tung
cover: "https://hackmd.io/_uploads/ry-LpojhJl.png"
categories:
  - 程式語言
tags:
  - java
  - 環境建置
draft: false
---

Java 開發環境建置與基本語法入門

<!--more-->

## VScode環境建置

### JAVA JDK 下載安裝

JAVA有很多種版本，這邊直接提供[我用的版本](https://www.oracle.com/java/technologies/downloads/)

直接安裝完後要新增環境變數→系統環境變數→新增
變數名稱：
```bash
JAVA_HOME
```
變數值：
```bash
C:Program Files/Java/jdk-XX<版本號>
```

### 安裝maven
直接下載[壓縮檔](https://maven.apache.org/download.cgi)
![image](https://hackmd.io/_uploads/SkBcoqZ5yx.png)
下載之後解壓縮並將`apache-maven-3.8.8`移動至以下路徑
```shell
C:/Program Files
```
接著將以下路徑加入至環境變數→使用者環境變數→Path
```shell
C:/Program Files/apache-maven-3.8.8/bin
```

## JAVA 程式語言定位
主要是後端的程式語言，可以做Android APP的撰寫，或者是Web Application的Backend

### JAVA 架構
![image](https://hackmd.io/_uploads/BJAodsWqye.png)

## JAVA 基本結構

### 第一個JAVA

#### JAVA Hello
新增一個專案資料夾，底下新增一個Hello.Java
![image](https://hackmd.io/_uploads/ryDu09-9kx.png)

接著打以下程式碼
```java
public class Hello {

    public static void main(String[] args) {
        System.out.println("Hello, java!");
    }
}
```

開啟Terminal
![image](https://hackmd.io/_uploads/HJOWyj-9Jg.png)

輸入以下指令編譯java檔案
```shell
javac Hello.java
```
![image](https://hackmd.io/_uploads/ryrpJsW51l.png)
編譯完成後會多一個`Hello.class`的檔案
![image](https://hackmd.io/_uploads/rykegsZqyl.png)

執行java檔案
```shell
java Hello
```
![image](https://hackmd.io/_uploads/By2Vxib9kg.png)

每次修改完成都需要編譯一次才可以做執行，JAVA並非編譯式語言，而是編譯與直譯的混和

> Reference：https://www.tsnien.idv.tw/Java1_WebBook/chap1/1-2%20Java%20%E8%AA%9E%E8%A8%80%E7%9A%84%E7%89%B9%E6%80%A7.html
