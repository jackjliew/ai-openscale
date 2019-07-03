---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: drift, behavior, metrics

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

# 漂移偵測 ![測試版標記](images/beta.png)
{: #behavior-drift-ovr}

模型中某些特性的重要性和影響，會隨時間而變更。這會影響相關聯的應用程式和產生的商業結果。透過漂移偵測，{{site.data.keyword.aios_short}} 讓您能夠追蹤模型度量、模型效能，以及特性的加權如何隨著時間而變更。漂移是指因隱藏的環境定義，使得預測效能隨時間而下降。由於您的資料會隨時間而變更，模型做出精確預測的能力可能會遞減。{{site.data.keyword.aios_short}} 既會偵測也會突顯漂移，以致於您可以採取更正動作。
{: shortdesc}

{{site.data.keyword.aios_short}} 會分析所有交易，以尋找促成漂移的交易。接著它會根據明顯促成漂移的屬性值，將記錄加以分組。

## 「漂移」摘要
{: #behavior-drift-glance}




## 解讀顯示畫面
{: #behavior-drift-display}

![公平性度量圖表，顯示漂移低於所設定的臨界值](images/fairness_metrics_001.png)


## 數學計算
{: #behavior-drift-math}

{{site.data.keyword.aios_short}} 會計算漂移 
