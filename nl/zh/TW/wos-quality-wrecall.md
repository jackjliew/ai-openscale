---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, weighted recal

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

# 加權查全率
{: #quality_weighted_recall}

「加權查全率」提供查全率的加權平均值，且其加權等於類別機率。
{: shortdesc}

## 「加權查全率」摘要
{: #quality_weighted_recall-glance}

- **說明**：查全率的加權平均值，其加權等於類別機率
- **預設臨界值**：下限 = 80%
- **預設建議**：
   - **上升趨勢**：上升趨勢表示度量在改進中。這表示模型重新訓練有效。
   - **下跌趨勢**：下跌趨勢表示度量在惡化中。回饋資料變成與訓練資料大不相同。
   - **錯誤或不規則變異**：錯誤或不規則變異指出回饋資料的評估之間不一致。增加「品質」監視器的最小樣本大小。
- **問題類型**：多類別分類
- **圖表值**：時間範圍內的最後一個值
- **可用的度量詳細資料**：混淆矩陣

## 解讀顯示畫面
{: #quality_weighted_recall-display}

![顯示「加權查全率」圖表](images/quality-recall.png)

## 數學計算
{: #quality_weighted_recall-math}

「加權查全率 (wR)」的定義如下：在使用加權資料的情況下，真肯定 (Tp) 數目佔「真肯定數目加誤否定 (Fn) 數目」的比率。 

```
            真肯定數目
查全率 =   ______________________________________________________

           （真肯定數目 + 誤否定數目）
```
