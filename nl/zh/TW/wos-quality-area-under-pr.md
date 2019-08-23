---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Area under PR

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:download: .download}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:faq: data-hd-content-type='faq'}

# PR 下方的區域
{: #quality-area-pr}

「查準率及查全率下方的區域」提供查準率和查全率曲線下方的區域，這在類別格外不平衡時就很好用。
{: shortdesc}

## 「PR 下方的區域」摘要
{: #quality-area-pr-glance}

- **說明**：在查準率和查全率曲線下方的區域
- **預設臨界值**：下限 = 80%
- **預設建議**：
   - **上升趨勢**：上升趨勢表示度量在改進中。這表示模型重新訓練有效。
   - **下跌趨勢**：下跌趨勢表示度量在惡化中。回饋資料變成與訓練資料大不相同。
   - **錯誤或不規則變異**：錯誤或不規則變異指出回饋資料的評估之間不一致。增加「品質」監視器的最小樣本大小。
- **問題類型**：二進位分類
- **圖表值**：時間範圍內的最後一個值
- **可用的度量詳細資料**：混淆矩陣

## 解讀顯示畫面
{: #quality-area-pr-display}

![顯示「PR 下方的區域」，其中度量為下跌趨勢](images/quality-area-under-pr.png)

### 公平性評分
{: #quality-area-pr-display-fairness-score}

對於「PR 下方的區域」度量，會顯示下列公平性評分。 

![顯示「PR 下方的區域」評分百分比。](images/wos-quality-area-pr-score.png)

### 排程
{: #quality-area-pr-display-schedule}

**排程**窗格會顯示**前次評估**和**下次評估**的時間。品質度量每小時會評估一次。您可以按一下**立即檢查品質**，以強制評估。您也可以按一下**新增回饋資料**，以新增回饋。

![顯示排程窗格，其中顯示前次評估時間和下次評估時間](images/wos-quality-schedule.png)


### 建議
{: #quality-area-pr-display-recommendations}

為了協助您解讀圖表，**建議**窗格會顯示哪些趨勢代表改進中或惡化中的模型成效。

![顯示建議窗格。](images/wos-quality-positive-recommendation.png)




## 數學計算
{: #quality-area-pr-math}

「查準率及查全率下方的區域」提供 `Precision + Recall` 兩者的總計。

查準率 (P) 的定義如下：真肯定 (Tp) 數目佔「真肯定數目加誤肯定 (Fp) 數目」的比率。

```
               真肯定數目
查準率 =      ______________________________________________________

              （真肯定數目 + 誤肯定數目）
```

查全率 (R) 的定義如下：真肯定 (Tp) 數目佔「真肯定數目加誤否定 (Fn) 數目」的比率。

```
            真肯定數目
查全率 =   ______________________________________________________

           （真肯定數目 + 誤否定數目）
```
