---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Mean absolute error

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

# 平均絕對誤差 ![測試版標記](images/beta.png)
{: #quality_abserror}

「平均絕對誤差」提供模型預測與目標值間之絕對誤差的平均值。
{: shortdesc}

## 「平均絕對誤差」摘要
{: #quality_abserror-glance}

- **說明**：模型預測與目標值間之絕對誤差的平均值
- **預設臨界值**：上限 = 80%
- **預設建議**：
   - **上升趨勢**：上升趨勢表示度量在惡化中。回饋資料變成與訓練資料大不相同。
   - **下跌趨勢**：下跌趨勢表示度量在改進中。這表示模型重新訓練有效。
   - **錯誤或不規則變異**：錯誤或不規則變異指出回饋資料的評估之間不一致。增加「品質」監視器的最小樣本大小。
- **問題類型**：迴歸
- **圖表值**：時間範圍內的最後一個值
- **可用的度量詳細資料**：無

## 解讀顯示畫面
{: #quality_abserror-display}

![顯示「平均絕對誤差」圖表。](images/xxxx.png)

## 數學計算
{: #quality_abserror-math}

「平均絕對誤差」的計算方式如下：加總所有的絕對誤差，然後除以誤差數目。

```
                         SUM  | Yi - Xi |
平均絕對誤差 =         ____________________

                          誤差數
```
