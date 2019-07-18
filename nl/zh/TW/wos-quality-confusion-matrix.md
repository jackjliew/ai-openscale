---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, confusion matrix

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

# 混淆矩陣 ![測試版標記](images/beta.png)
{: #it-conf-mtx}

這是品質度量的詳細資料，您可以檢視模型分析錯誤的記錄。這類異常可能是二進位分類模型的誤肯定或誤否定，或是多類別模型的不正確類別指派。您也可以檢視模型未正確分析的意見記錄清單。
{: shortdesc}

如果要檢閱相關明細（例如，適用於某些度量的二進位和多類別分類混淆矩陣），請按一下圖表。

![品質度量的明細表](images/quality_metrics_002.png)

對於二進位問題，{{site.data.keyword.aios_full}} 會指派目標種類給 `positive` 或 `negative` 層次。因此，混淆矩陣輸出會遵循使用慣例，其中，肯定種類的標籤位於第二列或第二欄。


## 步驟
{: #it-conf-mtx-steps}

1. 從任何**品質**圖表（例如**精確度**）中，按一下圖表中的小時/日。
    
    ![交易清單 - 偏誤](images/Confusion_Matrix_040819.004.png)

1. 混淆矩陣顯示誤肯定和誤否定。按一下資料格以檢視意見記錄的子集。

    ![交易清單 - 偏誤](images/Confusion_Matrix_040819.005.png)

1. 檢閱意見記錄，並要求意見記錄的分析說明。

    ![交易清單 - 偏誤](images/Confusion_Matrix_040819.006.png)

1. 交易出現在行內。

    ![交易清單 - 偏誤](images/Confusion_Matrix_040819.007.png)

