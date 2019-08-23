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

# 除偏选项
{: #it-dbo}

{{site.data.keyword.aios_short}} 使用两种类型的除偏：被动和主动。被动除偏让您了解如何对您造成偏差，而主动除偏则通过为当前应用程序实时更改模型来防止您保持该偏差。

- *被动除偏* - 被动除偏是 OpenScale 每小时自行自动执行的工作。由于它是在没有用户干预的情况下发生，因此被视为被动。当 {{site.data.keyword.aios_short}} 执行偏差检查时，它还通过分析模型的行为以及识别模型行为有偏差的数据来对数据执行除偏。

  然后，{{site.data.keyword.aios_short}} 构建机器学习模型以预测模型在给定的新数据点是否可能行为有偏差。{{site.data.keyword.aios_short}} 随后每小时分析模型接收的数据，并查找 {{site.data.keyword.aios_short}} 认为模型行为有偏差的数据点。对于此类数据点，公平性属性从少数到多数发生扰动，并且扰动数据会发送到原始模型以用于预测。原始模型的此预测用作已除偏输出。

  {{site.data.keyword.aios_short}} 每小时对模型在过去一小时接收到的所有数据执行此除偏。它还计算已除偏输出的公平性，并在**已除偏模型**选项卡中显示此公平性。

- *主动除偏* - 主动除偏是通过 REST API 端点来请求已除偏请求并将其引入到应用程序中的一种方式。您主动指导 {{site.data.keyword.aios_short}} 运行除偏并修改模型，以便能够以无偏差方式运行应用程序。在主动除偏中，您可以利用应用程序中的除偏 REST API 端点。此 REST API 端点将在内部调用模型并检查其行为。

  如果 {{site.data.keyword.aios_short}} 检测到模型行为有偏差，那么它将执行以上提及的数据扰动，并将数据发回到原始模型。原始模型对扰动数据的输出将作为已除偏预测进行返回。如果 {{site.data.keyword.aios_short}} 确定原始模型行为没有偏差，那么 {{site.data.keyword.aios_short}} 会将原始模型的预测作为已除偏预测进行返回。因此，通过使用此 REST API 端点，可以确保应用程序不会基于模型的有偏差输出来制定决策。

选择**已除偏评分端点**链接以查找除偏 REST API 端点

![显示除偏 API 端点详细信息屏幕，其中在代码片段框中显示 cURL 示例](images/insight-debias-api.png)

## 后续步骤
{: #it-dbo-nextsteps}

- 要缓解漂移，在检测到它之后，必须构建用于修正问题的新模型版本。{{site.data.keyword.aios_short}} 将有偏差记录存储在手动标注表中。需要手动标注这些有偏差记录，然后需要使用此附加数据对模型进行重新培训，以构建无偏差的新模型版本。


