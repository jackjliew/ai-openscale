---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: FAQs, frequently asked questions, questions

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

# 常見問題 (FAQ)
{: #wos-faqs}

您可以在這裡找到來自 {{site.data.keyword.aios_full}} 使用者的一些常見問題。
{: shortdesc}

## 問題
{: #wos-faqs-questions}

- [何謂 {{site.data.keyword.aios_short}}？](#faq-whatsa)
- [{{site.data.keyword.aios_short}} 如何計價？](#faq-pricing)
- [{{site.data.keyword.aios_short}} 可免費試用？](#faq-freetrial)
- [我所有的 AI 模型都在 Azure 中。Microsoft Azure ML 引擎可以與 {{site.data.keyword.aios_short}} 搭配使用嗎？](#faq-azure)
- [我所有的 AI 模型都在 Amazon 中。Amazon SageMaker ML 引擎可以與 {{site.data.keyword.aios_short}} 搭配使用嗎？](#faq-sagemaker)
- [{{site.data.keyword.aios_short}} 可在 {{site.data.keyword.icp4dfull_notm}} 上使用嗎？](#faq-icp)
- [我想在自己的伺服器上執行 {{site.data.keyword.aios_short}}。我應該配置多少電腦處理能力？](#faq-sizing)
- [如何將預測直欄從整數資料類型轉換成種類資料類型？](#wos-faqs-convert-data-types)
- [{{site.data.keyword.aios_short}} 為何需要存取我的訓練資料？](#trainingdata)

### 何謂 {{site.data.keyword.aios_short}}
{: #faq-whatsa}

Watson OpenScale 會追蹤及測量 AI 在整個生命週期中的輸出結果，以及調整及控管 AI，以因應多變的商業情況 - 讓模型可隨處建置及執行。

觀看這部影片，以快速概覽 {{site.data.keyword.aios_short}}。

<p>
  <div class="embed-responsive embed-responsive-16by9">
    <iframe class="embed-responsive-item" id="youtubeplayer" title="AI 具備可信任性與透明度" type="text/html" width="640" height="390" src="https://www.youtube.com/embed/6Ei8rPVtCf8" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>
  </div>
</p>

### {{site.data.keyword.aios_short}} 如何計價？
{: #faq-pricing}

當您準備好從 Lite 方案轉移時，**標準**計價方案可讓您監視最多 24 個已部署模型，且有效負載數、回饋列數或可解釋性的交易數目不限。最新資訊可在 [{{site.data.keyword.Bluemix}}型錄](https://cloud.ibm.com/catalog/services/watson-openscale?cm_sp=WatsonPlatform-WatsonPlatform-_-OnPageNavCTA-IBMWatson_OpenScale-_-AIOSProductPage){: external} 中找到。


### {{site.data.keyword.aios_short}} 可免費試用？
{: #faq-freetrial}

{{site.data.keyword.aios_short}} 透過 Lite 方案提供免費試用。若要註冊，請造訪 [{{site.data.keyword.aios_short}} 網頁](https://www.ibm.com/cloud/watson-openscale/){: external}，並按一下**立即著手開始**。您隨時可以使用 Lite 方案，且沒有期限（但每個月有用量限制，一個月重新整理一次）。

### 我所有的 AI 模型都在 Azure 中。Microsoft Azure ML 引擎可以與 {{site.data.keyword.aios_short}} 搭配使用嗎？
{: #faq-azure}

{{site.data.keyword.aios_short}} 同時支援 Microsoft Azure ML Studio 和 Microsoft Azure ML Service 引擎。如需相關資訊，請參閱 [Microsoft Azure ML Studio 架構](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure)和 [Microsoft Azure ML Service 架構](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure-service)。

### 我所有的 AI 模型都在 Amazon 中。Amazon SageMaker ML 引擎可以與 {{site.data.keyword.aios_short}} 搭配使用嗎？
{: #faq-sagemaker}

{{site.data.keyword.aios_short}} 支援 Amazon SageMaker ML 引擎。如需相關資訊，請參閱 [Amazon SageMaker 架構](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-aws-sage)。

### Is {{site.data.keyword.aios_short}} 可在 {{site.data.keyword.icp4dfull_notm}} 上使用嗎？
{: #faq-icp}

{{site.data.keyword.aios_short}} 是 {{site.data.keyword.icp4dfull_notm}} 的其中一個付費附加程式。 

### 我想在自己的伺服器上執行 {{site.data.keyword.aios_short}}。我應該配置多少電腦處理能力？
{: #faq-sizing}

對於三節點和六節點配置，會有特定的[硬體配置](/docs/services/ai-openscale?topic=ai-openscale-inst-install-icp#inst-hwt)準則。您的「IBM 技術銷售團隊」也可以協助您調整您特定配置的大小。由於 {{site.data.keyword.aios_short}} 是以 {{site.data.keyword.icp4dfull_notm}} 的附加程式形式執行，您需要兼顧這兩個軟體產品的需求。

### 如何將預測直欄從整數資料類型轉換成種類資料類型？
{: #wos-faqs-convert-data-types}

在配置模型的公平性監視時，預測直欄只接受整數值，即使預測標籤是種類也一樣。如何針對種類特性（亦即，不是整數）來配置此項？需要手動轉換嗎？ 

訓練資料可能有 "Loan Denied"、"Loan Granted" 等之類的類別標籤。{{site.data.keyword.pm_full}} 評分端點所傳回的預測值會是 "0.0"、"1.0" 等之類的值。評分端點也有一個選用直欄，其中含有以文字表示的預測。例如，如果 prediction=1.0，則 predictionLabel 直欄的值可能是 "Loan Granted"。如果這類直欄是可用的，則在配置模型的有利和不利輸出結果時，您可以指定字串值 "Loan Granted" 和 "Loan Denied"。如果這類直欄無法使用，則對於有利/不利類別，需要指定整數/倍精準數值 1.0、0.0。

{{site.data.keyword.pm_full}} 具有輸出綱目概念，藉以定義 {{site.data.keyword.pm_full}} 評分端點輸出的綱目，以及不同直欄的角色。這些角色用來識別哪個直欄含有預測值，哪個直欄含有預測機率，以及類別標籤值等。輸出綱目會自動設定給使用模型建置器建立的模型。此外，也可以使用 {{site.data.keyword.pm_full}} Python 用戶端來設定它。使用者可以使用輸出綱目，來定義含有以字串表示之預測的直欄。其作法是將直欄的 modeling_role 設為 'decoded-target'。{{site.data.keyword.pm_full}} Python 用戶端的相關說明文件位於：http://wml-api-pyclient-dev.mybluemix.net/#repository。搜尋 "OUTPUT_DATA_SCHEMA"，以瞭解輸出綱目和 store_model API，此 API 可接受以 OUTPUT_DATA_SCHEMA 作為參數。

### {{site.data.keyword.aios_short}} 為何需要存取我的訓練資料？
{: #trainingdata}

您必須提供存取權給 {{site.data.keyword.aios_short}} 去存取儲存在 Db2 中或 {{site.data.keyword.cos_full_notm}} 中的訓練資料，否則您必須執行一個可以存取該訓練資料的記事本。基於下列原因，{{site.data.keyword.aios_short}} 需要存取您的訓練資料：

- 為了產生對比說明：為了產生說明，需要有對於統計資料（例如中位數值、標準差和特殊值）的存取權。
- 為了顯示訓練資料統計資料：為了移入偏移詳細資料頁面，{{site.data.keyword.aios_short}} 必須具有能從中產生統計資料的訓練資料。

<!---
- To compute drift: Training data is required to build the drift detection model.
- To identify and suggest features to monitor for fairness: {{site.data.keyword.aios_short}} needs access to training data to suggest reference and monitored ranges.
--->

在記事本型方法中，您在 {{site.data.keyword.aios_short}} 中配置部署時應該上傳統計資料和其他資訊。這意味著 {{site.data.keyword.aios_short}} 不再對您環境中所執行的記事本以外的訓練資料具有存取權。它只可存取配置期間上傳的資訊。


