---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, F1-Measure

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

# F1-測量 ![測試版標記](images/beta.png)
{: #quality_f1-measr}

「F1-測量」提供查準率和查全率的調和平均值。
{: shortdesc}

## 「F1-測量」摘要
{: #quality_f1-measr-glance}

- **說明**：查準率及查全率的調和平均值
- **預設臨界值**：下限 = 80%
- **預設建議**：
   - **上升趨勢**：上升趨勢表示度量在改進中。這表示模型重新訓練有效。
   - **下跌趨勢**：下跌趨勢表示度量在惡化中。回饋資料變成與訓練資料大不相同。
   - **錯誤或不規則變異**：錯誤或不規則變異指出回饋資料的評估之間不一致。增加「品質」監視器的最小樣本大小。
- **問題類型**：二進位分類
- **圖表值**：時間範圍內的最後一個值
- **可用的度量詳細資料**：混淆矩陣

## 解讀顯示畫面
{: #quality_f1-measr-display}

![顯示「F1-測量」圖表。](images/quality-f1-meas.png)

## 數學計算
{: #quality_f1-measr-math}

「F1-測量」是查準率和查全率的加權調和平均值。

```
          (查準率 * 查全率)
F1 = 2 *  ____________________

          (查準率 + 查全率)
```
