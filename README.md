# Homework 2 (Due: 11/5)

- 寫下這週觀看 FutureLearn 課程的不解問題。
- 爬取 ptt 任兩個版當月的文章，各計算出其前百名之`詞頻表`、`詞類頻表` 與 `詞意頻表`。


## 繳交內容

- FutureLearn 問題：PDF 檔 (檔案請命名為：`<姓名>_futurelearn.pdf` 例如，`謝舒凱_futurelearn.pdf`)
- 程式作業：
    1. 原始碼 (`.py` or `.ipynb`)
    2. 資料
        1. 直接寫在 Jupyter Notebook 裡，或
        2. 存成 `.csv` (or `.tsv`)： `詞頻表` (`form_freq.tsv`)、`詞類頻表` (`form-pos_freq.tsv`) 與 `詞意頻表` (`form-sense_freq.tsv`)



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
