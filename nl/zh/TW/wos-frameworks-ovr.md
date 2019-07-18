---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits

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

# 支援的機器學習引擎、架構和模型
{: #in-fram}

{{site.data.keyword.aios_short}} 服務支援下列機器學習引擎。每個執行時期都支援在下列架構中建立的模型：

- [{{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-wml#frmwrks-wml) 
- [Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure#frmwrks-azure)
- [Azure ML Service](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azureservice#frmwrks-azureservice)
- [AWS SageMaker](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-aws-sage#frmwrks-aws-sage)
- [自訂](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-custom#frmwrks-custom)
- [SPSS C&DS](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-spss#frmwrks-spss)（只適用於 {{site.data.keyword.wos4d_full}}）

- [SAS AI Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-sas#frmwrks-sas)
{: download}
- [Google Cloud ML Engine](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-google#frmwrks-google)
{: download}

完整支援包括特定架構、問題和資料類型的下列特性：

- 有效負載記載	
- 回饋記載	
- 效能精確度	
- 執行時期偏誤偵測	
- 可解釋性	
- 自動除去偏誤

<p>&nbsp;</p>


## 支援的模型類型
{: #abt-models}

表 1. 模型支援明細

|演算法|**公平性**|**自動除去偏誤**|**解釋**|**精確度**|
|:---|:---:|:---:|:---:|:---:|
|**結構化分類**|是|是<sup>1</sup>|是<sup>1</sup>|是|
|**結構化迴歸**|是|即將納入|是|是|
|**文字分類**|否 - 進行中的研究主題|否 - 進行中的研究主題|是<sup>1</sup>|否|
|**影像分類**|否 - 進行中的研究主題|否 - 進行中的研究主題|是<sup>1</sup>|否||
{: caption="模型支援明細" caption-side="top"}

<sup>1</sup> 如果您的模型 / 架構會輸出預測機率

<p>&nbsp;</p>

## 瀏覽器支援
{: #in-brw}

{{site.data.keyword.aios_short}} 服務工具所需要的瀏覽器軟體層次，與 {{site.data.keyword.cloud_notm}} 所需的相同。如需詳細資料，請參閱 {{site.data.keyword.cloud_notm}} [必要條件](/docs/overview?topic=overview-prereqs-platform#browsers-platform)主題。

<p>&nbsp;</p>

## ModelOps CLI 工具
{: #in-mop}

[{{site.data.keyword.aios_short}} CLI 模型作業工具](https://github.com/IBM-Watson/aiopenscale-modelops-cli){: external}可讓您執行與機器學習模型生命週期管理有關的作業。這是 {{site.data.keyword.cloud_notm}} CLI 工具的補充工具，其中擴增了[機器學習外掛程式](https://www.ibm.com/support/knowledgecenter/DSXDOC/analyze-data/ml_dlaas_environment.html){: external}。

<p>&nbsp;</p>

## Python 用戶端
{: #in-pyc}

[{{site.data.keyword.aios_short}} Python 用戶端](http://ai-openscale-python-client.mybluemix.net/){: external} 是一個 Python 程式庫，可讓您直接在 {{site.data.keyword.cloud_notm}} 上使用 {{site.data.keyword.aios_short}} 服務。您可以使用 Python 用戶端而非 {{site.data.keyword.aios_short}} 用戶端使用者介面，以直接配置記載資料庫、連結您的機器學習引擎，以及選取及監視部署。如需以此方式使用 Python 用戶端的相關範例，請參閱 [{{site.data.keyword.aios_short}} 樣本記事本](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks)。

<p>&nbsp;</p>

## 後續步驟
{: #in-next}

- 檢視 [API 參照資料](https://{DomainName}/apidocs/ai-openscale){: external}。

還有其他問題嗎？ 

- [新增功能](/docs/services/ai-openscale?topic=ai-openscale-rn-relnotes)
- [聯絡 IBM](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: external}。
