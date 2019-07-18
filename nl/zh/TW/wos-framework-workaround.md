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

# 將協力廠商的 ML 引擎與 {{site.data.keyword.aios_short}} 整合
{: #fmrk-workaround}

{{site.data.keyword.aios_full}} 整合了外部機器學習服務引擎，例如：Microsoft Azure ML Studio、Microsoft Azure ML Service 和 Amazon SageMaker。
{: shortdesc}

您可以採取下列方式，將 {{site.data.keyword.aios_short}} 與協力廠商引擎整合在一起：

- 引擎連結層次：能夠列出部署，並取得部署明細。
  
- 部署訂閱層次：{{site.data.keyword.aios_short}} 需要能夠以必要格式（例如 {{site.data.keyword.pm_full}} 格式）來評分所訂閱的部署，並接收相同之相容格式的輸出。{{site.data.keyword.aios_short}} 必須配置成同時處理輸入及輸出格式。
   

- 有效負載記載：使用者應用程式所觸發之所部署模型的每一項輸入及輸出，都必須儲存在有效負載儲存庫中。有效負載記錄的格式遵循上述有關部署訂閱層次一節中所提及的相同規格。
   
   {{site.data.keyword.aios_short}} 會使用那些記錄來計算偏誤和解釋等。{{site.data.keyword.aios_short}} 不可能自動儲存使用者網站（位於 {{site.data.keyword.aios_short}} 系統外）上所執行的交易。這是 {{site.data.keyword.aios_short}} 保護專有資訊的作法之一。請使用 {{site.data.keyword.aios_short}} Rest API 或 Python SDK 來處理安全資料。
   
## 用來實作這個解決方案的步驟
{: #fmrk-workaround-steps}

1. [瞭解自訂機器學習引擎](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-customengine)。
2. [設置有效負載記載](/docs/services/ai-openscale?topic=ai-openscale-cdb-payload)。
3. [自動執行有效負載記載](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-pyld-lg)。
4. 使用這些[自訂機器學習引擎範例](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-cstmmlsengex)之一，來設置自訂機器學習引擎。

