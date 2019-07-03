---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: fairness, fairness monitor, payload, perturbation, training data, debiased

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

# 圖表建置器 ![測試版標記](images/beta.png)
{: #chart_builder}

使用 {{site.data.keyword.aios_short}} 圖表建置器，來建立自訂視覺化，以便可以在執行時期更充分瞭解模型的預測和輸入。當模型針對企業視為重要的特性或資料範圍進行預測時，圖表建置器讓您能夠檢視該預測的輸出。它有助於揭示資料中的新趨勢，以便提示企業和資料科學團隊考量對 AI 模型進行變更。
{: shortdesc}

例如，如果您從指導教學熟悉我們的信用風險模型，您可以看到預測類別中，針對「信用歷程」屬性的不同範圍所做的分割。 

   ![依特徵年齡顯示性別特徵預測的圖表](images/by_custom_chart.png)
      
   當針對「信用歷程」的這些範圍進行預測時，您也可以看到該模型的可信賴度。您可以利用自訂圖表，在所選資料範圍內（在特性、預測類別和信賴度之間挑選），分析傳送至部署中的評分有效負載。

   ![依特徵年齡顯示性別特徵預測的圖表](images/by_custom_chart002.png)
   
