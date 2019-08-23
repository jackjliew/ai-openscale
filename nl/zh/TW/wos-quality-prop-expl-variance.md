---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Proportion explained variance

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

# 可解釋變異比例
{: #quality_var}

「可解釋變異比例」提供可解釋變異與目標變異的比例。可解釋變異是指目標變異與預測錯誤變異之間的差異。
{: shortdesc}

## 「可解釋變異比例」摘要
{: #quality_var-glance}

- **說明**：可解釋變異比例是指可解釋變異與目標變異的比例。可解釋變異是指目標變異與預測錯誤變異之間的差異。
- **預設臨界值**：下限 = 80%
- **預設建議**：
   - **上升趨勢**：上升趨勢表示度量在改進中。這表示模型重新訓練有效。
   - **下跌趨勢**：下跌趨勢表示度量在惡化中。回饋資料變成與訓練資料大不相同。
   - **錯誤或不規則變異**：錯誤或不規則變異指出回饋資料的評估之間不一致。增加「品質」監視器的最小樣本大小。
- **問題類型**：迴歸
- **圖表值**：時間範圍內的最後一個值
- **可用的度量詳細資料**：無

## 解讀顯示畫面
{: #quality_var-display}

![顯示「可解釋變異比例」圖表。](images/xxxx.png)

## 數學計算
{: #quality_var-math}

「可解釋變異比例」的計算方式如下：求取數目的平均值，然後針對每一個數字，減去平均值，並對結果開平方。然後算出平方值

```
                                  群組之間的平方和
可解釋變異比例 =                 ________________________________

                                      平方和總計
```
