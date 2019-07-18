---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: databases, connections, scoring, requests

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

# 傳送評分要求
{: #cdb-score}

如果要配置監視器，{{site.data.keyword.aios_short}} 會要求您傳送評分有效負載，以便開始記載將要監視的資料。

- 對於部署在 {{site.data.keyword.pm_full}} 中的模型，您可以選擇在 {{site.data.keyword.pm_full}} 中對所部署的模型評分，或是使用有效負載記載 API 來評分。如果是在 {{site.data.keyword.pm_short}} 中對所部署模型評分，則會自動將它們傳送給 {{site.data.keyword.aios_short}}。 
- 對於其他的機器學習引擎（例如 Microsoft Azure、Amazon SageMaker 或自訂機器學習引擎），則必須使用「有效負載記載 API」來傳送評分有效負載。如需相關資訊，請參閱[非 {{site.data.keyword.pm_full}} 服務實例的有效負載記載](/docs/services/ai-openscale?topic=ai-openscale-cml-connect)。

## 有效負載記載的相關步驟
{: #cdb-score-apisteps}

1. 選取一項部署，並移至**有效負載記載**頁面。
2. 按一下 `cURL` 或 `Python` 標籤，選擇要使用 `cURL` 還是 `Python` 程式碼。
3. 按一下**複製到剪貼簿**，並將它貼到日誌模型部署要求和回應資料中。如需相關資訊，請參閱[非 {{site.data.keyword.pm_full}} 服務實例的有效負載記載](/docs/services/ai-openscale?topic=ai-openscale-cml-connect)。

程式碼 Snippet 中的欄位和值需要換成實際值，因為所提供的欄位及值只是範例。
{: important}

![選取資料庫](images/config-send-scoring.png)

執行有效負載記載之後，所選部署的**準備監視**直欄中會出現一個勾號。請按一下**配置監視器**以繼續。

## 瞭解評分要求數目
{: #cdb-score-capacity}

評分要求是 {{site.data.keyword.aios_short}} 處理程序不可或缺的一部分。您傳送給模型來評分的每一筆交易記錄，都會產生額外的處理程序，以便讓 {{site.data.keyword.aios_short}} 服務可以執行擾動，並建立解釋。

- 對於列表、文字、影像模型，下列基準線要求會產生資料點：

   - 1 項評分要求會產生 5000 個資料點。

- 單就列表分類模型而言，會發出額外的評分要求，以提供對比解釋。上述基準線要求中會新增下列要求：

   - 若有 100 項評分要求，則每一項要求各會額外產生 51 個資料點。
   - 若有 101 項評分要求，則每一項要求各會額外產生 1 個資料點。


## 後續步驟
{: #cdb-score-next-steps-scoringreq}

[配置監視器](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-mo-config)。
