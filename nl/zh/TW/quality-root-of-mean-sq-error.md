---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds

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

# 均方根誤差 ![測試版標記](images/beta.png)
{: #supqualdets_squ_errors_mean}

「均方根誤差 (RMSE)」視圖顯示模型中預測值與觀察值之間的誤差。
{: shortdesc}

## 「均方根誤差」摘要
{: #anlz_metrics_supqualdets_squ_errors_mean}

- **說明**：模型預測值與目標值之間的均方根誤差
- **預設臨界值**：上限 = 80%
- **預設建議**：
   - **上升趨勢**：上升趨勢表示度量在惡化中。回饋資料變成與訓練資料大不相同。
   - **下跌趨勢**：下跌趨勢表示度量在改進中。這表示模型重新訓練有效。
   - **錯誤或不規則變異**：錯誤或不規則變異指出回饋資料的評估之間不一致。增加「品質」監視器的最小樣本大小。
- **問題類型**：迴歸
- **圖表值**：時間範圍內的最後一個值
- **可用的度量詳細資料**：無

## 解讀顯示畫面
{: #supqualdets_squ_errors_mean-display}

![顯示「均方根誤差」圖表。](images/xxxx.png)

## 數學計算
{: #supqualdets_squ_errors_mean-math}

「均方根誤差」等於（預測減去觀察值）平方均值的平方根。

```
          ___________________________________________________________
RMSE  =  √(預測 - 觀察值)*(預測 - 觀察值)
```
