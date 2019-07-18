---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: payload, non-Watson, machine learning, services, subscription

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

# 非 {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}} 服務實例的有效負載記載
{: #cml-connect}

如果您的 AI 模型部署在 {{site.data.keyword.pm_full}} 以外的機器學習引擎中，您必須使用 Python 用戶端，針對外部機器學習引擎啟用有效負載記載。
{: shortdesc}

如需更完整的資訊，請參閱 [{{site.data.keyword.aios_short}} Python 用戶端說明文件](http://ai-openscale-python-client.mybluemix.net/){: external}，以及樣本 {{site.data.keyword.aios_short}} Python 用戶端記事本（為 [{{site.data.keyword.aios_short}} 指導教學](https://github.com/pmservice/ai-openscale-tutorials/blob/master/README.md){: external}的一部分）。

## 開始之前
{: #cml-prereq}

Db2 或 {{site.data.keyword.cos_full}} 中需要有模型訓練資料可用，才能監視您模型的偏誤。對於 Python 函數，不支援可解釋性和精確度。如需訓練資料的相關資訊，請參閱[為何 {{site.data.keyword.aios_short}} 需要存取我的訓練資料？](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

- 匯入並起始 {{site.data.keyword.aios_short}}

    ```python
    from ibm_ai_openscale import APIClient

    aios_credentials = {
      "instance_guid": "***",
      "url": "https://api.aiopenscale.cloud.ibm.com",
      "apikey": "***"
    }

    client = APIClient(service_credentials)
    ```
  只要遵循「[建立認證](/docs/services/ai-openscale?topic=ai-openscale-cred-create)」主題中的步驟，即可找到認證。

- 在 PostgreSQL 資料庫中建立綱目名稱

- 設置資料集區

    ```python
    client.data_mart.setup(db_credentials=postgres_credentials, schema=schemaName)

    client.data_mart.get_details()
    ```


## 後續步驟
{: #cml-next}

- 如果要繼續執行 {{site.data.keyword.aios_short}} 用戶端，請參閱[配置「精確度」或「品質」監視器](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor)。
- 如果要繼續執行 Python 指令庫，請參閱 [Python 用戶端說明文件](http://ai-openscale-python-client.mybluemix.net/){: external}。
