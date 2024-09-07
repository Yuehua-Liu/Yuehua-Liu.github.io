---
layout: post
title: 煩人的驗證碼破解，ddddocr 超好用Python 套件工具使用方式
date: 2024-09-06 18:24 +0800
categories: [技術分享]
tags: [爬蟲, Selenium, 驗證碼處理]
---

# 零、前言

寫爬蟲最討厭就是遇到各種驗種碼的機制，往往最難處理的都不是資料本身，而是如何繞過層層防護網，在傳統因應做法上，除了透過一般OCR工具自行辨識，可能就是透過像是 2Captcha 這類線上「人肉驗證碼破解」的方式來處理，但這終究還是讓人覺得有點沒效率。

最近在網路上找到一個蠻厲害的驗證碼辨識工具—ddddocr，可以直接透過深度學習預訓練好的模型進行辨識，並且具備一定的通用性，以下就來介紹其相關使用方式吧!

# 一、ddddocr 基本介紹

[GitHub - sml2h3/ddddocr: 带带弟弟 通用验证码识别OCR pypi版](https://github.com/sml2h3/ddddocr)

專案連結在此，此套件目標是成為「通用型」的驗證碼識別套件，可以應付大部分的驗證碼方式，包含但不僅限：

1. 文字驗證碼
2. 數字驗證碼
3. 文字點選驗證碼
4. 滑動方塊驗證碼

![image.png](/assets/img/post_img/2024-09-06-驗證碼破解/181126ba-2fb7-45ce-86c7-f59423b5ab4a.png)

因為是基於深度學習模型所做的辨識套件，因此就會有一定機率的辨識錯誤，但在驗證碼的處理上，其實只要重新整理，再辨識一次，就有大概率重整到模型可以辨識通過的結果。

# 二、套件基礎用法示範

## 基本流程概念：

1. 取得驗證碼圖片檔
2. 圖片檔匯入 model 進行辨識
3. 將回傳結果輸入驗證碼輸入框，Done!

以下針對我們最常遇到的文字驗證碼進行辨識示範～～～～

## 基礎 OCR 辨識：

我們以證交所買賣日報表查詢網站驗證碼為例：

![image.png](/assets/img/post_img/2024-09-06-驗證碼破解/image.png)

1. 先觀察網站的 html 結構，可以找到驗證碼圖片的下載網址
2. 載下圖片後，即可進行辨識
3. 使用下面程式碼進行圖片辨識
4. 最後輸出結果即為「驗證碼文字」
5. 將文字輸入回網站

```python
import ddddocr

# 建立OCR物件
ocr = ddddocr.DdddOcr()

# 先把驗證碼圖片下載下來，再讀檔
image = open("example.jpg", "rb").read()
result = ocr.classification(image)
print(result)
```

![image.png](/assets/img/post_img/2024-09-06-驗證碼破解/image%201.png)

從結果可以看到，ddddocr 的辨識度很高，自己實際測試，10 張驗證碼圖片的準確度基本上可以達到約 80%～90% 左右，這對於一般爬蟲程式來說，已經非常夠用。

更多驗證碼示範可以參考專案中的範例，這邊不多示範。

# 三、結語

這工具是自己試過許多驗證碼處理工具後，目前認為最好使用的，但驗證碼種類繁多，其實這應該也無法一套打天下，還是要 case by case 處理，如果有網友知道別種更有用的工具，也歡迎留言處分享，互相交流！

# 四、其他好用教學

1. 透過 Excel VBA 串接 ddddocr 處理網路驗證碼問題

[带带弟弟OCR，纯VBA本地获取网络验证码整体解决方案-Excel VBA程序开发-ExcelHome技术论坛 -](https://club.excelhome.net/thread-1666823-1-1.html)

1. ddddocr Rust 版本

[GitHub - 86maid/ddddocr: ddddocr rust 版本，ocr_api_server rust 版本，二进制版本，验证码识别，不依赖 opencv 库，跨平台运行，a simple OCR API server, very easy to deploy。](https://github.com/86maid/ddddocr)

1. ddddocr 部署 fastapi 服務

[GitHub - sml2h3/ddddocr-fastapi: 使用ddddocr的最简api搭建项目，支持docker](https://github.com/sml2h3/ddddocr-fastapi?tab=readme-ov-file)
---
