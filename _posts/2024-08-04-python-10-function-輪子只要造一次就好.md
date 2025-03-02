---
layout: post
title: Python-10-Function—輪子只要造一次就好
date: 2024-08-04 00:33 +0800
categories: [超新手 Python 教學系列課程]
tags: [基礎, Function]
image:
    path: /assets/img/post_img/Python-0-程式設計入門：淺顯易懂的基礎介紹%20f4f5613bb0b84a269c7899042f9a7014/Untitled.png
    alt: Python 程式設計入門系列
---
### 零、前言

一個 Function 就是把一組指令們，打包成一個功能，讓我們可以在程式中呼叫使用。例如做早餐，可能包含了「煮咖啡、煎蛋、擺餐盤、烤土司」等一系列動作，而我們就把這一系列動作，用一個「做早餐」來代替，此時「做早餐」就類似一個 Function，這樣的好處就是：我跟任何人溝通做早餐時，大家都知道它背後代表的一系列動作，我不用還得一次一次重複把該做哪些動作講清楚，會節省很多力氣！

### 一、Function 結構

一個 function 的結構如下：

```python
def my_function():
  print("Hello from a function")
```

- 說明
    - def：define，這邊定義一個叫做「`my_function()`」的功能 (function)。
    - 縮排內容：本功能(function) 要做的事情，用縮排劃分區塊，可以很簡單，也可以很複雜。

接著看一個超簡單使用 Function 範例：

```python
def my_function():
  print("Hello from a function")

# 在主程式中使用這個 function
my_function()
```

![輸出結果](/assets/img/post_img/Python-10-Function—輪子只要造一次就好%208face9bd31db4c1aa22a942880725ada/Untitled.png)
_輸出結果_

> Function 的定義必須要在主程式之前，就是要前面先定義過才能引用，也就是電腦需要先知道到 Function 的定義，後面程式要使用時，電腦才知道這是什麼東西，否則會出錯喔！
{: .prompt-tip }

### 二、代入參數的 Function

有時候，在不同時機下，雖然我們要做的事情都差不多，但會因為當下的情境不同而有些許差異。例如：一樣都是見人打招呼，遇見 Howard 會說「Hi！Howard~」，遇見 Eva 會說「Hi！Eva~」。這就是 Function「參數」的意義。

把上述例子轉成 Function：

```python
# 定義 say_hello 的 Function
def say_hello(name):
    print(f"Hi！{name}~")

# 遇到 Howard 情境 (若 False 就是遇到 Eva)
meet_howard = True
# 遇到不同人，參數也應該要不一樣
if meet_howard:
    say_hello("Howard") # 遇到 Howard，就會輸出「Hi!Howard~」
else:
    say_hello("Eva") # 遇到 Eva，就會輸出「Hi!Eva~」
```

![輸出結果](/assets/img/post_img/Python-10-Function—輪子只要造一次就好%208face9bd31db4c1aa22a942880725ada/Untitled%201.png)
_輸出結果_

- 說明：
    - `f”{}”`這是一個小技巧(f-string)，可以把變數內容顯示在字串中，這樣就不用把`name`寫死，可以隨著每次`name`的變化，就改變輸出的字串內容，注意，變數需要用 “{ }” 包住來表示。
    - 在主程式引用`say_hello()`Function 時，後面帶入了 “Howard”/”Eva” 的參數，這對應到上面`def say_hello()`中的`name`，也就是說，在遇到`“Howard”`情境下，`say_hello()`中的`name = “Howard”`；在遇到 `“Eva”`情境下，`say_hello()`中的`name = “Eva”`。

### 三、參數多一點的 Function

當然，有時候會有複合的情境需要判斷，不會只需要傳入一個參數，因此下面展示多參數的傳入：

```python
# 定義 say_hello 的 Function
def say_hello(name, sex):
    if sex == "male":
        print(f"你好！{name}~")
    elif sex == "female":
        print(f"妳好！{name}~")

# 遇到 Howard 情境 (若 False 就是遇到 Eva)
meet_howard = False
# 遇到不同人，參數也應該要不一樣
if meet_howard:
    say_hello("Howard", "male") # 遇到 Howard，並且是男的，就會輸出「你好!Howard~」
else:
    say_hello("Eva", "female") # 遇到 Eva，並且是女的，就會輸出「妳好!Howard~」
```

![輸出結果](/assets/img/post_img/Python-10-Function—輪子只要造一次就好%208face9bd31db4c1aa22a942880725ada/Untitled%202.png)
_輸出結果_

- 說明：
    - 我們讓`say_hello()`多增加一個參數，除了可以針對不同名字輸出不同字串，也可以針對不同性別輸出不同「你」/「妳」。
    - 下面主程式在引用`say_hello()`Function 時，裡面帶入的參數順序，必須與上面`def say_hello()`時定義的參數順序一致。

### 四、Function 回傳值

不只幫你執行工作，有時主程式也需要使用到 Function 執行工作完的結果，這時就需要 Function return 我們要的結果。

這邊舉一個工作上常用到計算「平均數」的例子：

```python
# 定義一個計算平均數的 Function
def average(num_of_list):
    res = 0
    total_num = len(num_of_list)
    for each_num in num_of_list:
        res = res + each_num
    avg = res / total_num
    return avg

# 主程式
score = [60, 80, 90, 50, 100, 66, 70]
score_avg = average(score)
print(f"整體平均數為：{score_avg}")
```

![輸出結果](/assets/img/post_img/Python-10-Function—輪子只要造一次就好%208face9bd31db4c1aa22a942880725ada/Untitled%203.png)
_輸出結果_

### 五、總結

善用 Function 可以很多時後大大減少程式碼的撰寫，當某個流程需要使用到某種制式功能，我們就可以直接引用已經開發完成的 Function，不用再重新寫一次程式碼，以增加開發效率。

未來我們在引用第三方套件(例如：pandas、matplotlib、numpy…)，其實也是同樣概念，都是使用別人已經造好的輪子，而不用自己從 0 開始手刻。