---
layout: post
title: Python-6-資料類型—字典 Dict—查詢資料的好幫手
date: 2024-08-03 22:38 +0800
categories: [超新手 Python 教學系列課程]
tags: [基礎, 資料結構]
---
### 零、前言

前面我們學到使用 List、Tuple 等工具來存放資料，但你有沒有想過一個問題，當資料存很多時，我應該怎麼有效率的找到我們需要的東西？

舉個例子：今天我想建立一個各產業的股票關注名單，方便我需要時可以搜尋，如果只知道 List、及Tuple 的前提下該如何實作？這樣的效率好嗎？下面我會在應用案例時做講解比較，方便讀者對照，也明白字典(Dict)在這種情境下的威力。

### 一、字典(Dict) 資料格式介紹

Python 中字典(Dict) 的格式架構如下：

```python
# Dict 基本是由 key(索引值)、value(值)組成，兩個為一組
my_dict = {key: value}
```

- Key：索引值，就像是字典中我們會先查「字根」、「筆劃」一樣，是我們查詢的依據
- Value：值，代表索引值類別下的實際資料內容
- 兩者之間需要以「：」做分隔，這樣為一組「鍵-值對」
- 須以`{}` 創建字典

實際我們用一個餐點的案例來舉例：

```python
# 餐廳清單選項
restaurant = {  1: "麥當勞",
                2: "肯德基",
                3: "西堤",
                4: "原燒"}

# 菜單依照用餐順序分類
menu = {"開胃菜": ["南瓜濃湯", "氣炸馬鈴薯"],
        "主餐": ["伊比利豬排", "紐約客牛排"],
        "甜點": ["提拉米蘇", "花生麻糬"],
        "飲料": ["檸檬氣泡水", "威士忌", "紅酒"]}

# 從字典中取值
today_res = restaurant[3] # 注意：這邊的 3 不是第 3 個位址，而是 key = 3，西堤
my_order = menu["主餐"][0] # 選擇主餐，因為回傳一個 list，因此進一步選擇第 0 個位址的 "伊比利豬排"

# 輸出文字
print(f"今天餐廳我想吃這間：{today_res}")
print(f"主餐我想點：{my_order}")

# 【輸出結果】
# 今天餐廳我想吃這間：西堤
# 主餐我想點：伊比利豬排
```

- 建立兩個 dict：`restaurant`、`menu` ，前者以`int`為 key；後者以`str`為 key
- 兩個 dict 存的 value 也不同，前者存`str`；後者存`list`
- 取值時，我們只要提供 key，便可以回傳該 key 類別下的值

### 二、常見功能使用

1. dict 修改值
    
    ```python
    # 建立我的股票觀察清單
    stock_watchlist = { "水泥": ['1101', '1102'],
                        "金融": ['2801', '2809'],
                        "電子零組件": ['2327']}
    
    # 修改 "金融" 相關產業的關注清單
    stock_watchlist['金融'] = ['2834', '2886']
    ```
    
2. dict 加入新的鍵值
    
    ```python
    # 新增 "食品" 產業關注名單
    stock_watchlist["食品"] = ['1201', '1203']
    
    # 更新「多筆」產業關注名單方式如下
    more_watchlist = {  "半導體": ['2330'],
                        "航運": ['2603']}
    stock_watchlist.update(more_watchlist) # dict().update() 方法可以將別的 dict 加入
    ```
    
3. dict 刪除既有鍵值
    
    ```python
    # 刪除 "食品" 產業關注項目 (key-value 都刪)
    del stock_watchlist["食品"]
    ```
    
4. 列出所有 dict 的 keys/values/items
    
    ```python
    # 列出所有 Keys
    print(stock_watchlist.keys())
    # 列出所有 Values
    print(stock_watchlist.values())
    # 列出所有 Items，會列出所有「鍵-值對」
    print(stock_watchlist.items())
    ```
    
    ![輸出結果](/assets/img/post_img/Python-6-資料類型—字典%20Dict—查詢資料的好幫手%20c1d637386eb0430aaf10d8fcc3c81290/Untitled.png)
    _輸出結果_
    
5. **產生或列印 dict 中的鍵-值對**
    
    ```python
    # 逐一列出所有 Keys
    for key in stock_watchlist:
        print(key)
    
    # 逐一列出所有「鍵-值對」，這邊因為每次會回傳 key、value 兩個值，故用兩個變數
    for key, value in stock_watchlist.items():
        print(key, value)
    ```
    
    ![輸出結果](/assets/img/post_img/Python-6-資料類型—字典%20Dict—查詢資料的好幫手%20c1d637386eb0430aaf10d8fcc3c81290/Untitled%201.png)
    _輸出結果_
    

### 三、應用案例

還記得我們一開始提到的案例嗎？

> 今天我想建立一個各產業的股票關注名單，方便我需要時可以搜尋
{: .prompt-info }

以下我們分別試著使用「List」與「Dict」來實做這個功能，比較看看兩者優劣：

1. 以 List 實作
    
    ```python
    # 建立我的股票觀察清單
    industry_list = ["水泥", "金融", "電子零組件"]
    stock_list = [  ['1101', '1102'],
                    ['2801', '2809'],
                    ['2327']]
    
    # 輸入產業
    target_industry = input("請輸入想看的產業:")
    
    if target_industry in industry_list:
        # 先比對 target_industry 在 industry_list 的位址
        # 進一步找出對應的 stock_list 位址
        index = 0
        for each_industry in industry_list:
            if target_industry == each_industry:
                print(f"【{target_industry}】關注股票：{stock_list[index]}")
                break
            else:
                index += 1
    ```
    
    ![輸出結果](/assets/img/post_img/Python-6-資料類型—字典%20Dict—查詢資料的好幫手%20c1d637386eb0430aaf10d8fcc3c81290/Untitled%202.png)
    _輸出結果_
    
2. 以 Dict 實作
    
    ```python
    # 建立我的股票觀察清單
    stock_watchlist = { "水泥": ['1101', '1102'],
                        "金融": ['2801', '2809'],
                        "電子零組件": ['2327']}
    
    # 輸入產業						
    target_industry = input("請輸入想看的產業:")
    
    if target_industry in stock_watchlist.keys():
        print(f"【{target_industry }】關注股票：{stock_watchlist[target_industry]}")
    ```
    
    ![輸出結果](/assets/img/post_img/Python-6-資料類型—字典%20Dict—查詢資料的好幫手%20c1d637386eb0430aaf10d8fcc3c81290/Untitled%203.png)
    _輸出結果_
    

從上面例子，我們可以看出：

- 用 List 來處理這種需要查找的問題時，步驟上會比較繁瑣，程式碼也相對不直覺，且在未來維護上也會有很大的隱憂存在，例如兩 List 順序上可能不小心沒對上就尷尬了
- 以 Dict 來處理時，程式碼就相對簡潔好懂，維護性也更佳

### 四、結語

能善加使用 Dict，對於我們在處理適合分類的資料時，是非常好用的工具，有點像是把一群資料貼上一個標籤，當我們需要這標籤下所有資料時，就可以透過 Key，把我們要的資料像是抓葡萄一樣，整串抓出來！