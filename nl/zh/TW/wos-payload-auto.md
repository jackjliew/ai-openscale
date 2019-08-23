---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: machine learning engines, frameworks, Microsoft Azure, Amazone SageMaker, custom ML engine 

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

# 自動執行有效負載記載
{: #fmrk-workaround-pyld-lg}

如果 {{site.data.keyword.aios_full}} 與 {{site.data.keyword.pm_full}} 都是以相同的 {{site.data.keyword.Bluemix_notm}} 帳戶來佈建時，則會在它們之間自動執行有效負載記載。您也可以使用下列其中一個案例和選項，針對其他機器學習提供者，或針對不是使用相同帳戶的 {{site.data.keyword.pm_full}} 實例，自動執行有效負載記載：
{: shortdesc}

### 案例 1：保留評分輸入及輸出的原始格式（不同於 {{site.data.keyword.aios_short}} 所需的格式）
{: #fmrk-workaround-case1}

如果您的應用程式使用原始有效負載格式，且無法變更，請選擇下列其中一個選項：

- 選項 1：自訂機器學習引擎的評分端點應接受這兩種有效負載格式。 

   視有效負載格式而定：{{site.data.keyword.aios_short}}（類似於 {{site.data.keyword.pm_full}}）或使用者的格式會以對應的格式來傳回輸出。如果是使用者的格式，則會將它轉換成 {{site.data.keyword.aios_short}} 的格式，並在有效負載記載表格中儲存成有效負載記錄。如果評分輸入格式是 {{site.data.keyword.aios_short}} 的格式，就不會儲存有效負載（此有效負載來自 {{site.data.keyword.aios_short}}，而非來自使用者）。

   如需相關資訊，請參閱[使用兩種有效負載格式](#fmrk-workaround-notsuppt)。

- 選項 2：如果因某些原因，不可能將這樣的邏輯內嵌在單一 REST API 端點中，您可以定義兩個端點。 

   其中一個端點供您的應用程式使用，不過，您必須新增有效負載記載，並將它轉換成預期的格式。第二個端點供 {{site.data.keyword.aios_short}} 用來進行必要的計算，例如：偏誤和可解釋性。這個端點不需要任何有效負載記載。在 {{site.data.keyword.aios_short}} 配置期間，第二個端點應指向採用相容格式的端點。

   如需相關資訊，請參閱[使用兩個端點](#fmrk-workaround-opt2-cs1)。

- 選項 3：將有效負載記載模組移至原始端點或下游應用程式。 

   如果您的應用程式支援這個選項，則只需在自訂機器學習引擎上開發一個端點：供 {{site.data.keyword.aios_short}} 使用的端點。

### 案例 2：處理 {{site.data.keyword.aios_short}} 所需的有效負載格式
{: #fmrk-workaround-case2}

在這類案例中，不需要將使用者的格式（評分輸入/輸出）轉換成 {{site.data.keyword.aios_short}} 所需的格式。

由於我們不想將內部評分要求記載成使用者有效負載（由 {{site.data.keyword.aios_short}} 負責計算），您必須開發兩個端點，或者必須針對單一端點編寫額外的邏輯。

- 選項 1：兩個端點。幾乎與「案例 1」中的選項 2 相同。唯一差別在於，不需要進行任何格式轉換，因為那些格式已相符。

- 選項 2：單一端點。需要偵測評分要求是否來自使用者的應用程式。可藉由在評分有效負載中傳送一些額外的資訊（又稱為 meta 資料）來達成此目的。如果偵測到這類 meta 資料，則應記載有效負載。

## 使用兩種有效負載格式
{: #fmrk-workaround-notsuppt}

假設我使用 XYZ 供應項目來處理我的模型。在這個階段，{{site.data.keyword.aios_short}} 不支援 XYZ。

我有很多下游應用程式會取用我在 XYZ 上的部署，而我無法變更評分有效負載的格式。不過，我可以修改評分端點邏輯。

### 步驟

1. 開發一個封裝了 XYZ 部署的自訂機器學習引擎。
2. 在自訂機器學習引擎上實作評分端點，以同時支援 XYZ 和 {{site.data.keyword.aios_short}} 的有效負載格式。
3. 在您自訂機器學習引擎上的評分端點中新增邏輯，以偵測有效負載的格式。
4. 如果有效負載來自下游應用程式，則將它轉換成 {{site.data.keyword.aios_short}} 格式，並在 {{site.data.keyword.aios_short}} 中記載成有效負載記錄。
5. 將下游應用程式的評分端點切換成您所建立的新評分端點。

如果評分端點的 URL 需維持相同，請使用 URL 重新導向（亦稱為 Proxy）。

## 使用兩個端點
{: #fmrk-workaround-opt2-cs1}

如果您有效負載的格式無法變更，例如，如果這會造成您下游應用程式中斷，您必須使用另外的端點。這種作法由下列元件組成：

- 評分端點（採用使用者的格式）；其原始評分端點對於輸入及輸出，都採用使用者定義的格式
- 自訂 ML 引擎，具有擾動端點（{{site.data.keyword.aios_short}} 格式）和探索端點。擾動端點會包裝原始評分端點，外加將 {{site.data.keyword.aios_short}} 格式轉換成使用者的格式，以及將使用者的輸出轉換成 {{site.data.keyword.aios_short}} 輸出。這對 {{site.data.keyword.aios_short}} 來說必須這樣做，如此才能發出正確的評分要求，以及瞭解輸出。
- 具備有效負載記載功能的評分端點封套。此封套供下游應用程式（而非原始評分端點）取用。已擴充其邏輯，而具備有效負載記載功能。每當執行評分要求時，會將輸入及輸出轉換成 {{site.data.keyword.aios_short}} 格式，並加以記載。

下列流程圖顯示自訂機器學習引擎解決方案，其中自訂機器學習引擎會處理擾動和探索端點，並將它轉換成您的格式：

![REST API 端點規格](images/woscustommlworkflow.png)

### 步驟
{: #fmrk-workaround-smple-cd}

1. 在 Microsoft Azure Machine Learning Service 上，使用記事本，針對信用風險模型 (scikit-learn) 部署建立評分端點。如需相關資訊，請參閱[這個樣本記事本](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/azure/Credit%20model%20with%20Azure%20ML%20Service%20and%20scikit-learn.ipynb)。
2. 建立自訂機器學習引擎，並將它部署在「Microsoft Azure 雲端」上，以作為 Flask 應用程式。建立擾動和探索端點。如需相關資訊，請參閱[這些部署指示](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-azure)。
3. 將 {{site.data.keyword.aios_short}} 配置成使用自訂機器學習引擎。如需相關資訊，請參閱[這個樣本記事本](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/azure/OpenScale%20and%20Custom%20ML%20Engine%20configuration.ipynb)。
4. 建立評分端點封套，以便在 Microsoft Azure Machine Learning Service 上自動執行有效負載記載。如需相關資訊，請參閱[這個樣本記事本](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/azure/Credit%20scoring%20endpoint%20wrapper%20with%20payload%20logging.ipynb)。

請特別注意下列項目：

- 認證：為了易於遵循指導教學，{{site.data.keyword.aios_short}} 認證已寫在程式碼內（評分端點封套）。您必須將這些值更新成您實際的認證。
- Python SDK 與 REST API：指導教學採用 Python SDK 來記載有效負載。您也可以使用 REST API 來這樣做，不過，您必須自行產生或重新整理記號。 
- {{site.data.keyword.cloud_notm}} 與 Cloud Pak for Data：如果您使用 {{site.data.keyword.wos4d_notm}}，則認證採用不同的格式；[這裡是樣本記事本](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine%20-%20ICP.ipynb)。{{site.data.keyword.aios_short}} 用戶端類別也不同。它使用的是 `APIClient4ICP` 用戶端類別。
- 成為個別端點/套件的有效負載記載 - 將有效負載記載和轉換方法擷取至個別的套件或端點。如此一來，如果您想將有效負載的批次注入到評分端點封套外部，就可以重複使用它。

