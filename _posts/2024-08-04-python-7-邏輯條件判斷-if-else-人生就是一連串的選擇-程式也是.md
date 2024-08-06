---
layout: post
title: Python-7-邏輯條件判斷(if…else…)—人生就是一連串的選擇，程式也是！
date: 2024-08-04 00:17 +0800
categories: [超新手 Python 教學系列課程]
tags: [基礎, 邏輯判斷]
---
### 零、前言

程式最重要的就是會透過一連串流程，協助我們自動化完成許多事情，而流程控制就像是整個過程裡面的主要骨架，所有的邏輯判斷，幾乎都是透過邏輯控制完成，這樣程式才能在不同情境下，執行不同的步驟，達成複雜的工作。

### 一、if…else 邏輯控制

我們先來看主要語法架構：

```python
if (條件式):
    # 情境1: 符合條件下的執行程式
elif (條件式):
    # 情境2: 符合條件下的執行程式
else:
    # 情境3: 上面條件都不符合時，要執行的程式
```

語法說明：

- 當`if`後面條件式滿足，則會執行「情境1」的程式
- 若`if`條件式不滿足，則會往下判斷`elif`的條件式，若滿足則執行「情境2」的程式
- 如果都沒滿足上面的條件，則全部歸類到`else`部分，執行「情境3」的程式

> 注意：判斷式後面都必須以「:」結尾，下面則包含條件成立下要執行的程式
{: .prompt-info }

這邊舉個簡單例子，現在要設計一個成績等第系統，把輸入的成績分等第，程式碼如下：

```python
score = 80

if score >= 90:
    print("成績等第：A")
elif score >= 80:
    print("成績等第：B")
elif score >= 70:
    print("成績等第：C")
elif score >= 60:
    print("成績等第：D")
else:
    print("成績等第：X，不及格！")

# 輸出結果：成績等第：B
```

程式說明：

- elif 可以建立很多個判斷式
- 一旦程式判斷到符合的條件，後面的判斷式就不會繼續做判斷，以這邊例子來說，score 再低一個判斷不符合「≥90」條件，因此往下一個判斷式走，第二個判斷式確認符合「≥80」的條件後，就不會繼續往下判斷

### 二、條件式的表達

下面舉例判斷式撰寫的方式：

```python
# 數字判斷 1
if num >= 100:
    pass # 代表不執行任何東西語法

# 數字判斷 2 (要注意，這邊不是用「=」，而是使用「==」來表示判斷是否相等)
if num == 100:
    pass

# List 是否有值判斷
my_list = [1, 2, 3]
if len(my_list) > 0:
    pass

# 文字是否相等判斷
keyword = "apple"
if keyword == "apple":
    pass

# 布林值判斷（判斷式的本質就是長這樣）
if True:
    pass

# 判斷是否非 None
my_to_list = []
if my_to_list is not None:
    pass
```

說明：

- 判斷式其實都是一個布林值(True or False)，例如：當 score=90，則「(score≥90)」這個條件式就是`True`，條件就會成立，反之會是`False`，條件不成立
- Python 的 `None` 是一個特殊的常數，用來表示「沒有值」或「空值」，但它不是「0」喔，0 還是一個數值

### 三、更多判斷式舉例

- 判斷 List 內有無值

```python
# 如果零食櫃裡面沒有商品，則出門採購零食
零食櫃 = []

if len(零食櫃) == 0:
    print("出門採購零食～～～")
else:
    print("零食還有，還不用出門～")

# 輸出：出門採購零食～～～
```

- List 內值判斷：判斷客人是否為黑名單，如果是，請趕他出門

```python
# 建立客戶黑名單
black_list = ['Jack', 'Lory', 'Kevin']

customer = "Howard"

# 如果 customer 名字出現在 black_list 中，就請他滾！
if customer in black_list:
    print("滾！！")
else:
    print("歡迎光臨！")

# 輸出結果：歡迎光臨！
```

- 文字判斷：輸入產業，輸出對應關注股票名單

```python
# 建立我的個股觀察清單
stock_list_1 = ["1101-台泥", "1102-亞泥"]
stock_list_2 = ["2002-中鋼", "2006-東和鋼鐵"]
stock_list_3 = ["2330-台積電", "2303-聯電"]
stock_list_4 = ["1201-味全", "1203-味王"]

# 建立一個 input，讓使用者輸入欲搜尋產業
search_industry = input("輸入要查詢的產業:")

# 這邊會判斷輸入的產業是否有在 industry 清單中，若有則輸出對應的股票清單
if search_industry == "水泥": # 水泥 (第 0 個位址)
    print(stock_list_1)
elif search_industry == "鋼鐵製造": # 鋼鐵製造 (第 1 個位址)
    print(stock_list_2)
elif search_industry == "半導體": # 半導體 (第 2 個位址)
    print(stock_list_3)
elif search_industry == "食品": # 食品 (第 3 個位址)
    print(stock_list_4)
else:
    print("查詢不到相關股票清單")
```

![Untitled](/assets/img/post_img/Python-7-邏輯條件判斷(if…else…)—人生就是一連串的選擇，程式也是！%205657c8b3829349f99e89c8890d11feaf/Untitled.png)

![輸出結果](/assets/img/post_img/Python-7-邏輯條件判斷(if…else…)—人生就是一連串的選擇，程式也是！%205657c8b3829349f99e89c8890d11feaf/Untitled%201.png)
_輸出結果_