---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, fairness monitor, payload, perturbation, training data, debiased, Logarithmic loss

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

# 對數損失 ![測試版標記](images/beta.png)
{: #quality_log_loss}

「對數損失」提供對數目標類別機率（信賴度）的平均值。亦稱為「期望對數似然」(Expected log-likelihood)，是一種有效測量模型效能的方式。
{: shortdesc}

## 「對數損失」摘要
{: #quality_log_loss-glance}

- **說明**：對數目標類別機率（信賴性）的平均值。它也稱為 Expected log-likelihood（期望對數似然）。
- **預設臨界值**：下限 = 80%
- **預設建議**：
   - **上升趨勢**：上升趨勢表示度量在惡化中。回饋資料變成與訓練資料大不相同。
   - **下跌趨勢**：下跌趨勢表示度量在改進中。這表示模型重新訓練有效。
   - **錯誤或不規則變異**：錯誤或不規則變異指出回饋資料的評估之間不一致。增加「品質」監視器的最小樣本大小。
- **問題類型**：二進位分類及多類別分類
- **圖表值**：時間範圍內的最後一個值
- **可用的度量詳細資料**：無

## 解讀顯示畫面
{: #quality_log_loss-display}

![顯示「對數損失」](images/quality-log-loss.png)

## 數學計算
{: #quality_log_loss-math}

對於二進位模型，「對數損失」的計算公式如下：

```
-(y log(p) + (1-y)log(1-p))
```

其中 p = true 標籤，y = 預測機率

對於多類別模型，「對數損失」的計算公式如下：

```
  M
-SUM Yo,c log(Po,c)
 c=1 
```

其中 M > 2，p = true 標籤，y = 預測機率
