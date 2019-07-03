---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, R squared

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

# R 平方 ![測試版標記](images/beta.png)
{: #quality_r_squared}

「R 平方」是指目標變異與目標變異預測錯誤之變異兩者之間的誤差率。它可告訴您用來建立模型的資料有多適合迴歸。
{: shortdesc}

## 「R 平方」摘要
{: #quality_r_squared-glance}

- **說明**：目標變異與目標變異預測錯誤之變異兩者之間的誤差率
- **預設臨界值**：下限 = 80%
- **預設建議**：
   - **上升趨勢**：上升趨勢表示度量在改進中。這表示模型重新訓練有效。
   - **下跌趨勢**：下跌趨勢表示度量在惡化中。回饋資料變成與訓練資料大不相同。
   - **錯誤或不規則變異**：錯誤或不規則變異指出回饋資料的評估之間不一致。增加「品質」監視器的最小樣本大小。
- **問題類型**：迴歸
- **圖表值**：時間範圍內的最後一個值
- **可用的度量詳細資料**：無

## 解讀顯示畫面
{: #quality_r_squared-display}

![顯示「R 平方」圖表。](images/xxxx.png)

## 數學計算
{: #quality_r_squared-math}

「R 平方」度量是以下列公式來定義。

```
                    可解釋的變異
R 平方 = 1 -      _____________________

                    變異總計
```
