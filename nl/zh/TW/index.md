---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: supported frameworks, models, model types, limitations, limits

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
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

# 關於
{: #in-ov}

{{site.data.keyword.aios_full}} 是一個適用於 AI 融入式應用程式的企業級環境，可讓企業認識如何根據商業規模，來建置及使用 AI，以及 AI 如何實現投資報酬率。
{: shortdesc}

<p>&nbsp;</p>

## 實作
{: #in-imp}

這裡說明您將如何實作 {{site.data.keyword.aios_short}}：

- **配置 {{site.data.keyword.aios_short}}**：透過好用的圖形環境，來[設置有效負載記載資料庫](/docs/services/ai-openscale?topic=ai-openscale-connect-db)，以及用來儲存您的 AI 模型和部署的 [Watson Machine Learning 實例](/docs/services/ai-openscale?topic=ai-openscale-wml-connect)。

- **使用監視器**：針對每一項部署，配置 {{site.data.keyword.aios_short}} 要如何監視該部署。您可以監視：

    - [公平性](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)
    - [精確度](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor)
    - [效能](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics#anlz_metrics_performance)

- **檢視及編輯受監視資料**：{{site.data.keyword.aios_short}} [儀表板](/docs/services/ai-openscale?topic=ai-openscale-io-ov)可讓您輕鬆檢視關鍵的洞察，以及識別您部署的問題。視覺化每一項受監視特性的個別資料點，會提供額外的詳細資料。

<p>&nbsp;</p>

## 限制
{: #in-lim}

- 現行版本只支援一個資料庫、一個 {{site.data.keyword.pm_full}} 實例，以及一個 {{site.data.keyword.aios_short}} 實例

- 資料庫和 {{site.data.keyword.pm_full}} 實例必須部署在相同的 {{site.data.keyword.cloud_notm}} 帳戶中。

- Lite（免費）方案具有下列的每月限制：

    - 兩個受監視的所部署模型
    - 可解釋 20 項交易
    - 50,000 筆有效負載記錄（累加）
    - 50,000 筆回饋記錄（累加）

- {{site.data.keyword.aios_short}} 使用 PostgreSQL 或 Db2 資料庫，來儲存模型相關資料（回饋資料、評分有效負載）和計算後的度量。目前不支援「精簡 Db2」方案。

- 根據授權限制，每一個 {{site.data.keyword.aios_short}} 實例只能有 20 個所部署模型。

- 對於 {{site.data.keyword.pm_full}}，經由機器學習閘道所傳送之擾動影像的有效負載不得超過 1 MB。若要避免發生逾時問題，影像不得超過 125 x 125 像素，且必須循序傳送，如此才會在第一個影像完成時，要求取得第二個影像的解釋。


<p>&nbsp;</p>

## 已知問題
{: #rn-12ki}

- **Microsoft Azure**

    - Azure Machine Learning Web 服務有兩種類型，但 {{site.data.keyword.aios_short}} 只支援`新`類型。不支援`標準`類型。

    - __*必須使用預設輸入名稱*__：在 Azure Web 服務中，預設輸入名稱是 `"input1"`。目前 {{site.data.keyword.aios_short}} 規定要使用此欄位，如果遺漏，{{site.data.keyword.aios_short}} 就無法運作。

      如果您的 Azure Web 服務不是使用預設名稱，請將輸入欄位名稱變更為 `"input1"`，這樣程式碼就會運作。

- **AWS SageMaker**

    - __*不支援 BlazingText 演算法*__：在 {{site.data.keyword.aios_short}} 現行版本中，不支援 AWS SageMaker BlazingText 演算法輸入有效負載格式。

- **自訂 ML 服務實例**

    - [Python 模組](/docs/services/ai-openscale?topic=ai-openscale-as-module)目前無法將「可解釋性」運用於「自訂」服務實例上。這是因為「自訂」服務實例要求回應資料中需有一項數值預測，但這並未隨附於模組 Script 中。

<p>&nbsp;</p>

## 支援機器學習引擎和架構
{: #in-fram}

{{site.data.keyword.aios_short}} 服務支援下列機器學習引擎。每個執行時期都支援在下列架構中建立的模型：

- [{{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-wml#frmwrks-wml) 
- [Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure#frmwrks-azure)
- [AWS Sagemaker](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-aws-sage#frmwrks-aws-sage)
- [自訂](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-custom#frmwrks-custom)


- [SAS AI Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-sas#frmwrks-sas)
{: download}
- [Google Cloud ML Engine](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-google#frmwrks-google)
{: download}
- [SPSS C&DS（僅適用於 ICP）](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-spss#frmwrks-spss)
{: download}

完整支援包括特定架構、問題和資料類型的下列特性：

- 有效負載記載	
- 回饋記載	
- 效能精確度	
- 執行時期偏誤偵測	
- 可解釋性	
- 自動除去偏誤

<p>&nbsp;</p>

## 瀏覽器支援
{: #in-brw}

{{site.data.keyword.aios_short}} 服務工具所需要的瀏覽器軟體層次，與 {{site.data.keyword.cloud_notm}} 所需的相同。如需詳細資料，請參閱 {{site.data.keyword.cloud_notm}} [必要條件](/docs/overview?topic=overview-prereqs-platform#browsers-platform)主題。

<p>&nbsp;</p>

## ModelOps CLI 工具
{: #in-mop}

[{{site.data.keyword.aios_short}} CLI 模型作業工具 ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://github.com/IBM-Watson/aiopenscale-modelops-cli){: new_window} 可讓您執行與機器學習模型生命週期管理有關的作業。這是 {{site.data.keyword.cloud_notm}} CLI 工具的補充工具，其中擴增了[機器學習外掛程式 ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://www.ibm.com/support/knowledgecenter/DSXDOC/analyze-data/ml_dlaas_environment.html){: new_window}。

<p>&nbsp;</p>

## Python 用戶端
{: #in-pyc}

[{{site.data.keyword.aios_short}} Python 用戶端 ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](http://ai-openscale-python-client.mybluemix.net/){: new_window} 是一個 Python 程式庫，可讓您直接在 {{site.data.keyword.cloud_notm}} 上使用 {{site.data.keyword.aios_short}} 服務。您可以使用 Python 用戶端而非 {{site.data.keyword.aios_short}} 用戶端使用者介面，以直接配置記載資料庫、連結您的機器學習引擎，以及選取及監視部署。如需就這樣使用 Python 用戶端的相關範例，請參閱 [{{site.data.keyword.aios_short}} 樣本記事本 ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks)。

<p>&nbsp;</p>

## 後續步驟
{: #in-next}

- [開始使用](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted)此服務。
- 檢視 [API 參照資料 ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://{DomainName}/apidocs/ai-openscale){: new_window}。

還有其他問題嗎？ 

- [新增功能](/docs/services/ai-openscale?topic=ai-openscale-rn-relnotes)
- [請聯絡 IBM ![「外部鏈結」圖示](../../icons/launch-glyph.svg "「外部鏈結」圖示")](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: new_window}。
