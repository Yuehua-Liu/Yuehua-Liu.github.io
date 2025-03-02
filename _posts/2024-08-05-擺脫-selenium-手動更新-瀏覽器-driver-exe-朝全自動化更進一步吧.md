---
layout: post
title: 擺脫 Selenium 手動更新 瀏覽器 driver.exe，朝全自動化更進一步吧！
date: 2024-08-05 20:48 +0800
categories: 技術分享
tags: [爬蟲, Selenium, 自動化測試, 版本差異]
image:
    path: /assets/img/post_img/2024-08-05/selenium_cover.png
    alt: Selenium driver 自動更新技巧
---

### 零、前言

在使用 Selenium 進行瀏覽器自動化作業的過程中，許多人一開始會遇到一個常見的問題：每次使用前都必須手動下載對應版本的 `driver.exe`，才能啟動瀏覽器並進行自動化測試。

這個過程不僅繁瑣，還容易因為驅動版本與瀏覽器版本不匹配而導致錯誤。

因此，如何自動化管理 Selenium 驅動的更新，成為了使用者們非常關心的議題。在這篇文章中，我們將探討如何透過不同版本的 Selenium，自動更新並管理瀏覽器驅動程式，以提升自動化測試的效率。
![Untitled](/assets/img/post_img/2024-08-05/selenium_cover.png)

### 一、Selenium Driver 版本更新自動化 (以 Chrome 為例)

`Selenium 4.x.x` 版本後的方法(套件內已內建)：

```python
from selenium import webdriver
# import Service 元件，自動抓取最新版本 driver
from selenium.webdriver.chrome.service import Service

# 加入這兩行，程式便會自動抓取最新版本 Chromedriver，並存在記憶體中使用
service = Service()
driver = webdriver.Chrome(service=service)
```

---

`Selenium 3.x.x` 版本的方法(必須先安裝 `webdriver-manager`，靠他自動抓新版本 driver)：

```bash
pip install webdriver-manager
```

安裝完套件後，便可透過以下程式碼實行自動抓 driver 的操作：

```python
from selenium import webdriver
# import webdriver_manager 來輔助自動安裝 Driver 功能
from webdriver_manager.chrome import ChromeDriverManager

# ChromeDriverManager 會透過 install() 方法 自動下載最新 driver 版本
driver = webdriver.Chrome(ChromeDriverManager().install())
```

>🌟 如果不得已得用 Selenium 3 系列的版本，可以嘗試使用第二的方式。
{: .prompt-info }

### 二、參考

- [Selenium 官方手冊](https://www.selenium.dev/selenium/docs/api/py/webdriver_chrome/selenium.webdriver.chrome.service.html)
- [Webdriver-manager 套件說明](https://pypi.org/project/webdriver-manager/)
