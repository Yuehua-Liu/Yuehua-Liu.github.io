---
layout: post
title: 用 Python 打造 Youtube 影片下載小幫手
date: 2025-02-04 19:17 +0800
categories: 技術分享
tags: [爬蟲, 自動化, 多媒體]
image:
    path: /assets/img/post_img/2025-02-06/pytube_cover.png
    alt: 用 Python 打造 Youtube 影片下載小幫手
---

## 0. 製作自己的 YT 影片下載工具

最近因為老婆需要宣導反詐，需要有相關影片素材講課，請我幫忙下載YT上的宣導影片，但內容實在有點多XD 如果要用一般的 YT Online Downloader 下載工具，超浪費時間且也怕遇到釣魚網站，後來想想還是自己手動來寫比較實在~

剛好看到「pytube」這個套件，試用之後覺得蠻好用的，這邊推薦給大家~

>💡 目前「pytube」套件直接使用會有問題，建議改用「pytubefix」的修補套件來處理。
{: .prompt-info }

## 1. 需求分析

### 🎯目標

老婆提供給我的目標網址：

[三不守則—不當車手、不借帳戶、不點可疑連結（30秒動畫）](https://youtu.be/wckNGrZuoO8)

[廢柴與防詐小天使的任務—破解投資詐騙（30秒版）](https://youtu.be/WFG0nL-of2k)

[冷靜想想反詐系列_30秒](https://youtube.com/playlist?list=PLTpYQm9I7B0Zw0KU7qkjqLOIVqLljNf8G&si=P6pZTDmT9DWSryp-)

[詐騙套路來解密系列_30秒](https://youtube.com/playlist?list=PLTpYQm9I7B0ZPgE_LP_GfaPxrxydawDIP&si=eg2xrhAcIO3vUWzz)

### 🧑‍💼功能需求

- 可以觀察到，前兩部影片是單一影片，比較單純，後兩個網址則是「Playlist」播放清單，裡面包含了多部影片。
- 我們期望輸入越單純越好，老婆只要把想要下載的網址提供給系統，不管連結是單一影片、播放清單，程式都可以自動處理，批次下載。
- 針對單一影片，直接下載後存到 `/Downloads/` 資料夾裡面，若是 Playlist，則自動生成 `/Downloads/Playlist_name/` 資料夾，把該清單的影片獨立下載到特定資料夾中。

## 2. 程式撰寫

```python
import os
# 處理SSL憑證驗證
import ssl
ssl._create_default_https_context = ssl._create_stdlib_context
# 主要用來下載 YT 影片的工具
from pytubefix import YouTube, Playlist
```

```python
# Function：下載 YT 程式的主邏輯
def download_youtube_video(url_list, output_path="downloads"):
    try:
        for dir, url in url_list:
            # 建立下載資料夾（如果不存在）
            if not os.path.exists(output_path):
                os.makedirs(output_path)

            # 取得 YouTube 影片
            yt = YouTube(url)
            stream = yt.streams.get_highest_resolution()  # 選擇最高畫質
            print(f"正在下載：{yt.title}")

            if dir:
                # 下載影片
                stream.download(f"{output_path}/{dir}")
                print(f"下載完成！影片已儲存於：{output_path}/{dir}/{yt.title}")
            else:
                # 下載影片
                stream.download(output_path)
                print(f"下載完成！影片已儲存於：{output_path}/{yt.title}")
            print("="*40)

    except Exception as e:
        print(f"發生錯誤：{e}")

# Function：分析是影片還是播放清單
def parse_url(url_list, output_path="downloads"):
    video_url_list = []
    for url in url_list:
        if "playlist" in url:
            playlist = Playlist(url)
            print(f"偵測到播放清單：{playlist.title}")
            # 建立下載資料夾（如果不存在）
            if not os.path.exists(output_path):
                os.makedirs(output_path)
            
            # 針對播放清單建立資料夾
            playlist_path = f"{output_path}/{playlist.title}"
            if not os.path.exists(playlist_path):
                os.makedirs(playlist_path)

            for url in playlist.video_urls:
                video_url_list.append([playlist.title, url])
        else:
            video_url_list.append([None, url])
    return video_url_list
```

- `download_youtube_video()` 是用來下載影片的主程式，只負責接收網址，並下載到目標資料夾。
- `parse_url()` 則會先進行網址解析，分辨「單一影片」or「播放清單」，做好歸類(預先建立歸檔資料夾)後，再丟給 `download_youtube_video()` 處理，將工作單一化。

```python
if __name__ == "__main__":
		# 目標網址清單
    video_url_list = ["https://youtu.be/wckNGrZuoO8",
                      "https://youtu.be/WFG0nL-of2k",
                      "https://youtu.be/jNUWS6_5bNU?si=RVryWYN49IidO1_h",
                      "https://youtube.com/playlist?list=PLTpYQm9I7B0Zw0KU7qkjqLOIVqLljNf8G&si=P6pZTDmT9DWSryp-",
                      "https://youtube.com/playlist?list=PLTpYQm9I7B0ZPgE_LP_GfaPxrxydawDIP&si=eg2xrhAcIO3vUWzz"]
    # 分析網址屬性(「單一影片」or「播放清單」)
    video_url_list = parse_url(video_url_list)
    # 下載影片
    download_youtube_video(video_url_list, output_path="downloads")
```

- 這邊用很陽春「列清單」的方式來輸入，是自己偷懶~如果要讓這支程式更優化，這邊可以改用「讀取 Excel」的方式，讓使用者輸入更加方便與直覺，這樣老婆就不用再麻煩我了~現在留著，還可以顯得自己還有點用處 (誤 XD

## 3. 結語

以上只是很快速地將基礎的影片下載程式呈現出來，整個完成程式大概只花不到30分鐘即可完成，後續當然還有很多優化空間，包括將其製作成一個網站服務或者增加更方便使用者輸入網址的前端介面，如果對此有興趣也可以自行多嘗試！！
