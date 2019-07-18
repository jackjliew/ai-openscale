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

# 监视公平性、每分钟的平均请求数以及准确性
{: #it-ov}

个别部署的监视数据以时间序列图表形式显示。该图表跟踪过去 7 天的“公平性”、“每分钟的平均请求数”和“准确性”。
{: shortdesc}

## 查看部署的数据
{: #it-vdep}

从仪表板中选择部署以查看该部署的监视数据。标题显示有关已部署模型的信息，例如**模型标识**和**创建日期**字段。

![时间序列图表](images/insight-time-chart.png)

由于算法检查仅每小时运行一次，因此还提供了链接以按需检查公平性和质量。从**调度**面板中，可单击以下链接来对数据进行立即检查：

![“检查公平性”按钮](images/wos-fairness-button.png)


![“检查质量”按钮](images/wos-quality-button.png)

接下来，单击图表并在图表中移动标记以查看单个小时的统计信息：

![时间序列图表详细信息](images/wos-insight-time-detail.png)

- ***公平性***：两个公平性特征（Sex 和 Age）达到其设置的要进行核准的阈值。
- ***质量***：**ROC 下的面积**度量显示警报，因为它不在所配置的阈值范围内。
- ***每分钟平均请求数***：单击**吞吐量**度量可查看期间每分钟处理的记录数。吞吐量每分钟计算一次，并且在图表中报告了其一小时内的平均值。

## 可视化特定小时的数据
{: #it-vdet}

要查看特定公平性统计信息背后的详细信息，请单击特定时间的图表。

系统将打开受监视特征在所选小时的数据点的可视化。按照先前示例，将在以下示例中显示 Age 特征。

请注意页面顶部的三个过滤器（特征、日期和小时），通过它们可选择其他特征或时间以查看详细信息。

![时间序列图表](images/wos-insight-data-detail.png)

### 解释图表
{: #it-intp}

图表显示多个事项：

- 您可以观察遇到偏差的群体（年龄介于 18 岁到 23 岁之间的客户）。图表还显示此群体的预期结果百分比。

- 图表显示参考群体的预期结果百分比 (70%)。这是所有参考群体的预期结果的平均值。

- 图表指示存在偏差，因为年龄在 18 岁到 23 岁的群体的预期结果百分比值与参考群体的预期结果百分比值的比率超过阈值。换句话说，0.52/0.7 = 0.74，小于阈值 0.8。

- 图表还针对来自载荷表的数据（已进行分析来识别偏差）中属性的每个不同值，显示其参考值和受监视值的分布。换句话说，如果偏差检测算法分析了载荷表中的最后 1790 个记录，那么其中 120 个记录的客户年龄介于 18 岁到 23 岁之间，并且在该分布中，`Approved` 和 `Denied` 结果通过条形图来表示。对于公平性属性的每个不同值，将会显示载荷数据的分布（即使显示了参考值也如此）。此信息可用于将偏差与模型接收的数据量相关联。

- 该图表还显示年龄在 31 岁到 35 岁之间的群体接收到 91% 的预期结果。这表示偏差的来源，意味着该组中的数据导致结果偏差，并导致参考类的预期结果百分比增加。此信息可用于标识数据的各个部分，然后可在重新训练模型时对该数据进行低采样。

- 图表显示的另一个重要内容是包含已标识为手动标记的数据的表的名称。只要算法在模型中检测到偏差，它就还会识别可发送以由人类进行手动标记的数据点。然后，可以使用此手动标记的数据以及原始训练数据来重新训练模型。此经过重新训练的模型可能不会有偏差。手动标记表存在于与 {{site.data.keyword.aios_short}} 实例关联的数据库中。

## 查看事务
{: #it-tra}

通过此选项，您可以在单击**查看事务**按钮时查看导致偏差的个别事务。

![查看事务](images/view_transactions.png)

系统将列出部署行为有偏差的事务的列表。单击任何事务标识的**解释**链接，以在“可解释性”选项卡中获取有关该事务的详细信息。有关更多信息，请参阅[监视可解释性](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)。

选择**所有事务**视图以查看所选特征（在此示例中为“AGE”）和所选时间段（在此示例中为“September 15, 2018 1:00 PM”）中的所有事务：

![事务列表 - 所有](images/transaction_list1.png)

选择**有偏差事务**视图以仅查看事务中接收到有偏差结果的子集。每个有偏差事务与类似但略有更改（扰动）的事务进行比较，从而显示更改受监视特征 (AGE) 的值将如何导致有偏差事务产生有利结果：

![事务列表 - 有偏差](images/transaction_list2.png)

## 生产模型和已除偏模型
{: #it-prdb}

您可以使用这两个选项卡在生产模型和 {{site.data.keyword.aios_short}} 所创建的已除偏模型之间进行切换。请参阅[了解除偏的工作方式](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-debias)以获取更多详细信息。

![运行时训练切换](images/bias-debias.png)

选择**已除偏模型**选项卡会向您显示已除偏模型与生产中模型相比较的更改。在此示例中，模型“公平性”已从 74% 增加到 93%，而“准确性”仅下降 1%。图表还反映 18 岁到 23 岁的年龄组的结果状态有所改进。

![运行时训练切换](images/insight-data-detail2.png)

### 除偏选项
{: #it-dbo}

{{site.data.keyword.aios_short}} 使用两种类型的除偏：被动和主动。被动除偏让您了解如何对您造成偏差，而主动除偏则通过为当前应用程序实时更改模型来防止您保持该偏差。

- *被动除偏* - 被动除偏是 OpenScale 每小时自行自动执行的工作。由于它是在没有用户干预的情况下发生，因此被视为被动。当 {{site.data.keyword.aios_short}} 执行偏差检查时，它还通过分析模型的行为以及识别模型行为有偏差的数据来对数据执行除偏。

  然后，{{site.data.keyword.aios_short}} 构建机器学习模型以预测模型在给定的新数据点是否可能行为有偏差。{{site.data.keyword.aios_short}} 随后每小时分析模型接收的数据，并查找 {{site.data.keyword.aios_short}} 认为模型行为有偏差的数据点。对于此类数据点，公平性属性从少数到多数发生扰动，并且扰动数据会发送到原始模型以用于预测。原始模型的此预测用作已除偏输出。

  {{site.data.keyword.aios_short}} 每小时对模型在过去一小时接收到的所有数据执行此除偏。它还计算已除偏输出的公平性，并在**已除偏模型**选项卡中显示此公平性。

- *主动除偏* - 主动除偏是通过 REST API 端点来请求已除偏请求并将其引入到应用程序中的一种方式。您主动指导 {{site.data.keyword.aios_short}} 运行除偏并修改模型，以便能够以无偏差方式运行应用程序。在主动除偏中，您可以利用应用程序中的除偏 REST API 端点。此 REST API 端点将在内部调用模型并检查其行为。

  如果 {{site.data.keyword.aios_short}} 检测到模型行为有偏差，那么它将执行以上提及的数据扰动，并将数据发回到原始模型。原始模型对扰动数据的输出将作为已除偏预测进行返回。如果 {{site.data.keyword.aios_short}} 确定原始模型行为没有偏差，那么 {{site.data.keyword.aios_short}} 会将原始模型的预测作为已除偏预测进行返回。因此，通过使用此 REST API 端点，可以确保应用程序不会基于模型的有偏差输出来制定决策。

选择**已除偏评分端点**链接以查找除偏 REST API 端点

![除偏 API 端点](images/insight-debias-api.png)
