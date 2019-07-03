---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, Area under ROC

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

# ROC 下方的面積 ![測試版標記](images/beta.png)
{: #quality_roc}

接收端操作特徵曲線下方的面積提供查全率和誤肯定率曲線下方的面積。它會針對錯檢率，計算靈敏度。
{: shortdesc}

## 「ROC 下方的面積」摘要
{: #quality_roc-glance}

- **說明**：在查全率和誤肯定率曲線下方的區域
- **預設臨界值**：下限 = 80%
- **預設建議**：
   - **上升趨勢**：上升趨勢表示度量在改進中。這表示模型重新訓練有效。
   - **下跌趨勢**：下跌趨勢表示度量在惡化中。回饋資料變成與訓練資料大不相同。
   - **錯誤或不規則變異**：錯誤或不規則變異指出回饋資料的評估之間不一致。增加「品質」監視器的最小樣本大小。
- **問題類型**：二進位分類
- **圖表值**：時間範圍內的最後一個值
- **可用的度量詳細資料**：混淆矩陣

## 解讀顯示畫面
{: #quality_roc-display}

![顯示「ROC 下方的面積」圖表。](images/quality-area-under-roc.png)

## 數學計算
{: #quality_roc-math}

「ROC 下方的面積」會以參數形式，相對於臨界值 `T`，繪製成`真肯定率`與`誤判率`的對照。

