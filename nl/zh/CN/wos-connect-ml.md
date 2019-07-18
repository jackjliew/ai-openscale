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

# 非 {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}} 服务实例的有效内容日志记录
{: #cml-connect}

如果 AI 模型部署在除 {{site.data.keyword.pm_full}} 以外的其他机器学习引擎中，那么您必须使用 Python 客户机为外部机器学习引擎启用有效内容日志记录。
{: shortdesc}

请参阅 [{{site.data.keyword.aios_short}} Python 客户机文档](http://ai-openscale-python-client.mybluemix.net/){: external}以及样本 {{site.data.keyword.aios_short}} Python 客户机笔记本（包含在 [{{site.data.keyword.aios_short}} 教程中](https://github.com/pmservice/ai-openscale-tutorials/blob/master/README.md){: external}），其中提供了更完整的信息。

## 开始之前
{: #cml-prereq}

您需要让 Db2 或 {{site.data.keyword.cos_full}} 能够使用您的模型的训练数据，这样才能监视模型的偏差。Python 函数不支持可解释性和准确性。有关训练数据的更多信息，请参阅 [ 为什么 {{site.data.keyword.aios_short}} 需要访问我的培训数据？](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

- 导入并启动 {{site.data.keyword.aios_short}}

    ```python
    from ibm_ai_openscale import APIClient

    aios_credentials = {
      "instance_guid": "***",
      "url": "https://api.aiopenscale.cloud.ibm.com",
      "apikey": "***"
    }

    client = APIClient(service_credentials)
    ```
  可以通过遵循“[创建凭证](/docs/services/ai-openscale?topic=ai-openscale-cred-create)”主题中显示的步骤来找到凭证。

- 在 PostgreSQL 数据库中创建模式名称

- 设置数据集市

    ```python
    client.data_mart.setup(db_credentials=postgres_credentials, schema=schemaName)

    client.data_mart.get_details()
    ```


## 后续步骤
{: #cml-next}

- 要继续使用 {{site.data.keyword.aios_short}} 客户机，请参阅[配置准确性或质量监视器](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor)。
- 要继续使用 Python 命令库，请参阅 [Python 客户机文档](http://ai-openscale-python-client.mybluemix.net/){: external}。
