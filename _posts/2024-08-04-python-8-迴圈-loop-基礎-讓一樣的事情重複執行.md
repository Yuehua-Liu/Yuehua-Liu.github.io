---
layout: post
title: Python-8-迴圈(Loop)(基礎)—讓一樣的事情重複執行！
date: 2024-08-04 00:20 +0800
categories: [超新手 Python 教學]
tags: [基礎, 迴圈]
---
### 零、前言

寫程式幫我們處理日常事務，最棒的事情就是，當我們需要一直重複一個流程或者行為，我們只需要透過「迴圈」這概念，便可以幫助我們把事情通通搞定！

迴圈是**一段在程式中我們只定義一次，但可能會連續執行多次的程式碼**。迴圈中的程式碼會執行特定的次數，或者是執行到特定條件成立時結束迴圈，或者是針對某一集合中的所有項目都執行一次。

舉個例子：

> 有一個水果清單(fruit_list)，裡面分別存放'apple', 'banana', 'guava', 'pineapple'四種水果，我想依次把他們輸出，該怎麼做？
{: .prompt-info }

在還沒有學習迴圈前，直覺上想到的做法可能是

```python
fruits = ['apple', 'banana', 'guava', 'pineapple']
print(fruit[0]) //輸出 'apple'
print(fruit[1]) //輸出 'banana'
print(fruit[2]) //輸出 'guava'
print(fruit[3]) //輸出 'pineapple'
```

但仔細想想，這種作法很不科學，萬一有一萬種水果，自己不是要打字打到死嗎QQ 所以這種時候就該透過「迴圈」的概念來幫我們自動輸出，而我們只要把這些「重複的」輸出動作定義一次就好！

在 Python 中，迴圈主要有兩種語法：

1. for 迴圈
2. while 迴圈

### 一、for-loop

先看結構：

```python
for 暫存變數 in 可迭代物件:
    執行迴圈中動作
```

註：迭代（iteration）可以想像成更替的概念，四季迭代=四季更替，具有前後關係。

再看範例：

```python
# 依次讀取 List 中元件
fruits = ['apple', 'banana', 'guava', 'pineapple']

# loop 邏輯
for each_fruit in fruits:
    # 迴圈中，每一次循環要處理的事情
    print(each_fruit)
```

在上面程式碼中，fruits 是一個預先定義好的list，存放四種水果名稱，而「for each_fruit in fruits」則代表建立一個依序讀取 fruit 內容的迴圈，每一次循環會把讀取到的內容存進 each_fruit 這個變數中。

按照上面邏輯，我們可以知道，這個迴圈總共會進行4次循環：

1. 提取”apple”，存進 each_fruit
2. 提取”banana”，存進 each_fruit
3. 提取”guava”，存進 each_fruit
4. 提取”pineapple”，存進 each_fruit

![輸出結果](/assets/img/post_img/Python-8-迴圈(Loop)(基礎)—讓一樣的事情重複執行%20ea71043bdfba42da89dfe085c74d0f76/Untitled.png)
_輸出結果_

如此一來，如果今天要 print 100種、10000種水果，我都只需要短短幾行程式碼，就可以幫我們輕鬆解決啦！

綜上所述，在定義 for-loop 時，我們需要提供：

1. 一個「可以被迭代」的物件(上面的 fruits)，例如 string、list、tuple 等，這邊例子來說，是一個 list。
2. 一個自己定義的暫存變數(上面的 each_fruit)，存放每次提取出來的內容，方便自己在迴圈中做使用，這邊的例子來說，就是要讓我可以用來輸出。

### 二、while-loop

先看結構：

```python
while 是否滿足條件:
    執行迴圈中動作
```

再看範例：

```python
# 定義 fruits list 內容
fruits = ['apple', 'banana', 'guava', 'pineapple']
# 紀錄 list 的長度，這邊是 4
list_length = len(fruits)

# loop 邏輯
index = 0
while (index < list_length):
    print(fruits[index])
    index += 1
```

while 迴圈與 for 比較不一樣的地方在於，while 屬於在「條件滿足的情況下」，會「無限執行」的迴圈，代表她不會像 for-loop 一樣，每次從可迭代物件依序抓內容，而是單純以「設定條件是否滿足」做迴圈判斷。

這邊的例子，我們思考步驟如下:

1. 首先定義一個新變數 list_length，代表 fruits 的長度，這邊透過 len() 這個python內建方法來取得 fruits list 的長度。
2. 建立一個初始為 0 的 index 變數，代表我們要讀取 fruits list 的位置。
3. while 迴圈的意思為「在 index 位置還沒超過 fruits list 最大長度的情況下，執行迴圈內步驟」
4. 輸出 fruits 第 index 個位置的值
5. 迴圈最後，index 必須 +1，這動作很重要，否則 index 都會是 0，導致迴圈永遠無法結束。

![輸出結果](/assets/img/post_img/Python-8-迴圈(Loop)(基礎)—讓一樣的事情重複執行%20ea71043bdfba42da89dfe085c74d0f76/Untitled%201.png)
_輸出結果_

綜上所述，在定義 while-loop 時，我們需要提供：

1. 一個「在符合的情況下需要執行迴圈事項」的條件，在這邊例子，就是當 index 小於 list_length 的情況下，進下面輸出文字的行為。

### 三、兩種迴圈使用時機

兩者在此範例中都可以達到一樣的效果，但如果稍微觀察一下，應該會覺得，for-loop 在這個案例中好像是比較直覺簡單的做法，事實上也確實如此，每種迴圈語法都有適合自己使用的時機，這在未來看到更多程式碼時，就會越來越有當下該使用哪種方法的感覺。

- 使用 for-loop 時機：
    - 需要從一個 List、Set 等資料中，每次取不同值做相同SOP時
    
    ```python
    # 定義一個「從資料庫取得個股當天的收盤價」的 Function
    def get_stock_price(stock_id):
        # 這邊是程式碼
        # ...
        # ...
        
        # 最後將資料庫的股價回傳給主程式
        return stock_price
    
    # 建立我的股票清單
    stock_list = ["2330", "2331", "3036"]
    # 依序取得 stock_list 清單中每檔股票的收盤價
    for each_stock in stock_list:
        stock_close_price = get_stock_price(each_stock) # 從上面方法取得股價
        print(f"股票代號：{each_stock}, 當日收盤價為：{stock_close_price}") # 輸出
    ```
    
- 使用 while-loop 時機：
    - 永遠重複下去，直到某個條件達成的循環
    
    ```python
    # 遊戲程式，除非點擊 quit，不然遊戲會一直進行下去
    print("Game Start!")
    while True:
        # 遊戲流程
        # ...
        # ...
        if game_over:
            # break 代表直接跳出迴圈
            break
            
    print("Game Over...")
    ```