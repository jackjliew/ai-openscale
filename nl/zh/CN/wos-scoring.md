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

# 发送评分请求
{: #cdb-score}

要配置监视器，{{site.data.keyword.aios_short}} 要求您发送评分有效内容，以便开始记录将受监视的数据。

- 对于 {{site.data.keyword.pm_full}} 中部署的模型，可以选择对 {{site.data.keyword.pm_full}} 中的已部署模型进行评分或者使用有效内容日志记录 API。对于在 {{site.data.keyword.pm_short}} 中进行评分的已部署模型，会将这些模型自动发送到 {{site.data.keyword.aios_short}}。 
- 对于其他机器学习引擎（例如 Microsoft Azure、Amazon SageMaker 或定制机器学习引擎），必须使用有效内容日志记录 API 来发送评分有效内容。有关更多信息，请参阅[非 {{site.data.keyword.pm_full}} 服务实例的有效内容日志记录](/docs/services/ai-openscale?topic=ai-openscale-cml-connect)。

## 有效内容日志记录的步骤
{: #cdb-score-apisteps}

1. 选择部署，然后转至**有效内容日志记录**页面。
2. 通过单击 `cURL` 或 `Python` 选项卡，选择使用 `cURL` 还是 `Python` 代码。
3. 单击**复制到剪贴板**并将其粘贴到日志模型部署请求和响应数据中。有关更多信息，请参阅[非 {{site.data.keyword.pm_full}} 服务实例的有效内容日志记录](/docs/services/ai-openscale?topic=ai-openscale-cml-connect)。

需要将代码片段中的字段和值替换为真实值，因为其中提供的值仅作参考之用。
{: important}

![选择数据库](images/config-send-scoring.png)

运行有效内容日志记录后，将在**监视就绪**列中针对所选部署显示复选标记。单击**配置监视器**以继续。

## 了解评分请求数
{: #cdb-score-capacity}

评分请求是 {{site.data.keyword.aios_short}} 处理不可或缺的一部分。发送到要评分的模型的每个事务记录都会生成其他处理，以便 {{site.data.keyword.aios_short}} 服务可以执行扰动并创建说明。

- 对于表格、文本和图像模型，以下基线请求将生成数据点：

   - 1 个评分请求生成 5000 个数据点。

- 仅对于表格分类模型，将发出其他评分请求以进行对比说明。以下请求会添加到上述基线请求：

   - 100 个评分请求中每个请求生成 51 个附加数据点。
   - 101 个评分请求中每个请求生成 1 个附加数据点。


## 后续步骤
{: #cdb-score-next-steps-scoringreq}

[配置监视器](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-mo-config)。
