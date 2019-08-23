---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, monitoring, charts, de-biasing, bias, accuracy

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

# 除去偏誤選項
{: #it-dbo}

{{site.data.keyword.aios_short}} 使用兩種類型的除去偏誤：被動和主動。被動除去偏誤可讓您知道您的偏誤現象，而主動除去偏誤則會藉由即時變更現行應用程式的模型，來阻止您繼續帶有該偏誤。

- *被動除去偏誤* - 被動除去偏誤是 OpenScale 會自行、自動且每小時就會進行的工作。之所以視為被動，是因為它不需要使用者介入就會進行。當 {{site.data.keyword.aios_short}} 執行偏誤檢查時，也會對資料執行除去偏誤，其作法是分析模型的行為，並識別模型在其中以偏誤的方式執行的資料。

  接著，{{site.data.keyword.aios_short}} 會建置一個機器學習模型，以預測模型在給定的新資料點上，是否可能以偏誤的方式執行。接著，{{site.data.keyword.aios_short}} 會每小時分析一次模型所收到的資料，並尋找 {{site.data.keyword.aios_short}} 認為模型在其中以偏誤的方式執行的資料點。對於這類資料點，會從少到多擾動公平性屬性，並將擾動資料傳送給原始模型進行預測。對原始模型的這項預測，會作為已除去偏誤的輸出。

  {{site.data.keyword.aios_short}} 會針對過去一小時模型所收到的所有資料，每小時執行一次這項除去偏誤。它也會針對已除去偏誤的輸出，計算其公平性，並顯示在**除去偏誤模型**標籤中。

- *主動除去偏誤* - 主動除去偏誤可讓您透過 REST API 端點，要求取得已除去偏誤的結果，並帶到您的應用程式中。您是主動指示 {{site.data.keyword.aios_short}} 執行除去偏誤，並變更模型，以便能以無偏誤方式來執行您的應用程式。在主動除去偏誤中，您可以從您的應用程式利用除去偏誤 REST API 端點。此 REST API 端點會在內部呼叫您的模型，並檢查其行為。

  如果 {{site.data.keyword.aios_short}} 偵測到模型以偏誤的方式執行，它會依照上述來擾動資料，並將它傳回給原始模型。會傳回原始模型對擾動資料的輸出，以作為已除去偏誤的預測。如果 {{site.data.keyword.aios_short}} 判定原始模型不會以偏誤的方式執行，則 {{site.data.keyword.aios_short}} 會傳回原始模型的預測，來作為已除去偏誤的預測。因此，藉由使用這個 REST API 端點，可確保您的應用程式不會根據模型的偏誤輸出來做出決策。

選取**已除去偏誤的評分端點**鏈結，以尋找您除去偏誤的 REST API 端點

![顯示「除去偏誤 API 端點明細」畫面，且程式碼 Snippet 方框中會顯示 cURL 範例](images/insight-debias-api.png)

## 後續步驟
{: #it-dbo-nextsteps}

- 如果要減輕偏誤，在偵測到偏誤之後，您必須建置新版本的模型，來修正問題。{{site.data.keyword.aios_short}} 會將有偏誤的記錄儲存在手動標示表格中。這些有偏誤的記錄需要手動標示，然後需使用此額外的資料來重新訓練模型，以便為無偏誤的模型建置一個新版本。


