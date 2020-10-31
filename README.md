# Homework 2 (Due: 11/5)

- 寫下這週觀看 FutureLearn 課程的不解問題
- 爬取 ptt 任兩個版當月的文章，各計算出其前百名之**詞頻表**、**詞類頻表**與**詞意頻表**:
    - 10/31 補充: 兩版各抽 **20-30 篇文章**就好


## 繳交內容

- FutureLearn 問題：PDF 檔 (檔案請命名為：`<姓名>_futurelearn.pdf` 例如，`謝舒凱_futurelearn.pdf`)
- 程式作業：
    1. 原始碼 (`.py` or `.ipynb`)
    2. 資料
        1. 直接寫在 Jupyter Notebook 裡，或
        2. 存成 `.csv` (or `.tsv`)：  
            **詞頻表**: `form-freq-<board>.tsv`  
            **詞類頻表**: `form-pos_freq-<board>.tsv`  
            **詞意頻表**: `form-sense_freq-<board>.tsv`



## Python 環境設定

1. 安裝 [Python 3](https://www.python.org/downloads/)

2. 安裝套件：`DistilTag`, `CwnSenseTagger`
    - 請打開 Terminal (Mac: 搜尋 terminal; Windows: 命令提示字元) 輸入指令
        ```bash
        pip3 install -U DistilTag CwnSenseTagger  #or, pip install -U DistilTag CwnSenseTagger
        ```
    - 在 Windows 上安裝可能會出錯，可嘗試下列安裝方式 (詳見 [pytorch 官網](https://pytorch.org/get-started/locally/))：
        ```bash
        pip install torch==1.6.0+cpu torchvision==0.7.0+cpu -f https://download.pytorch.org/whl/torch_stable.html
        pip install -U DistilTag CwnSenseTagger
        ```


## 小提示

- PTT 的資料抓取，可以使用 <https://github.com/jwlin/ptt-web-crawler>，就不須自行剖析 HTML
- 建議不要爬太大的板 (e.g., Gossiping)，因為語料太大需要花相當多的時間處理
    - 如果處理時間過長，可以兩版各抽 **20-30 篇文章**處理就好
- 使用 `DistilTag` 斷詞與標注詞性時，最好一篇篇分別處理 (把所有文章串成一個字串會比較耗時)
    - 斷詞、標記之前，需將字串轉成**全形**，否則會出錯。可透過下方的 `strB2Q()` 進行：
        ```python
        def strB2Q(ustring):
            ss = []
            for s in ustring:
                rstring = ""
                for uchar in s:
                    inside_code = ord(uchar)
                    if inside_code == 32:  # 全形空格直接轉換
                        inside_code = 12288
                    elif (inside_code >= 33 and inside_code <= 126):  # 全形字元（除空格）根據關係轉化
                        inside_code += 65248
                    rstring += chr(inside_code)
                ss.append(rstring)
            return ''.join(ss)
        
        >>> strB2Q('我會寫 Python!')
        '我會寫Ｐｙｔｈｏｎ！'
        ```


### Starter Code (參考)

```python
import json
from DistilTag import DistilTag
from CwnSenseTagger import senseTag


# 半形轉全形函數 (斷詞需要全形符號才能運作)
def strB2Q(ustring):
    ss = []
    for s in ustring:
        rstring = ""
        for uchar in s:
            inside_code = ord(uchar)
            if inside_code == 32:
                inside_code = 12288
            elif (inside_code >= 33 and inside_code <= 126):
                inside_code += 65248
            rstring += chr(inside_code)
        ss.append(rstring)
    return ''.join(ss)


# 讀取文章 (文章爬取見 https://github.com/jwlin/ptt-web-crawler)
with open("<某板文章>.json", "r", encoding="UTF-8") as f:
    articles = json.load(f)
    ## 後續處理...


# 斷詞、PoS tag、Sense tag
tagger = DistilTag()
for article in articles:
    tagged = tagger.tag(strB2Q(article))
    sense_tagged = senseTag(tagged)
    ## 後續處理...


# 計算詞頻表、詞類頻表、詞意頻表
## 後續處理...
```
