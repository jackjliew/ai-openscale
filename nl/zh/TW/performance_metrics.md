---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: metrics, monitoring, custom metrics, thresholds

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# 分析度量及交易 ![測試版標記](images/beta.png)
{: #anlz_metrics}

您可以使用 {{site.data.keyword.aios_full}}，透過各種方法來分析度量及交易。
{: shortdesc}

## 混淆矩陣 ![測試版標記](images/beta.png)
{: #it-conf-mtx}

這是品質度量的詳細資料，您可以檢視模型分析錯誤的記錄。這類異常可能是二進位分類模型的誤肯定或誤否定，或是多類別模型的不正確類別指派。您也可以檢視模型未正確分析的意見記錄清單。
{: shortdesc}

1. 從任何**品質**圖表（例如**公平性**）中，按一下圖表中的小時/日。
    
    ![交易清單 - 偏誤](images/Confusion_Matrix_040819.004.png)

1. 混淆矩陣顯示誤肯定和誤否定。按一下資料格以檢視意見記錄的子集。

    ![交易清單 - 偏誤](images/Confusion_Matrix_040819.005.png)

1. 檢閱意見記錄，並要求意見記錄的分析說明。

    ![交易清單 - 偏誤](images/Confusion_Matrix_040819.006.png)

1. 交易出現在行內。

    ![交易清單 - 偏誤](images/Confusion_Matrix_040819.007.png)

