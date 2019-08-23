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

# 可视化特定小时的数据
{: #it-vdet}

要查看特定公平性统计信息背后的详细信息，请单击特定时间的图表。系统将打开受监视特征在所选小时的数据点的可视化。按照先前示例，将在以下示例中显示 Age 特征。
{: shortdesc}

请注意页面顶部的三个过滤器（特征、日期和小时），通过它们可选择其他特征或时间以查看详细信息。

![显示时间序列图表，其中包含表示有效内容、年龄的扰动数据以及有利结果数的列](images/wos-insight-data-detail.png)

## 解释图表
{: #it-intp}

图表显示多个事项：

- 您可以观察遇到偏差的群体（年龄介于 18 岁到 23 岁之间的客户）。图表还显示此群体的预期结果百分比。

- 图表显示参考群体的预期结果百分比 (70%)。这是所有参考群体的预期结果的平均值。

- 图表指示存在偏差，因为年龄在 18 岁到 23 岁的群体的预期结果百分比值与参考群体的预期结果百分比值的比率超过阈值。换句话说，0.52/0.7 = 0.74，小于阈值 0.8。

- 图表还针对来自载荷表的数据（已进行分析来识别偏差）中属性的每个不同值，显示其参考值和受监视值的分布。换句话说，如果偏差检测算法分析了载荷表中的最后 1790 个记录，那么其中 120 个记录的客户年龄介于 18 岁到 23 岁之间，并且在该分布中，`Approved` 和 `Denied` 结果通过条形图来表示。对于公平性属性的每个不同值，将会显示载荷数据的分布（即使显示了参考值也如此）。此信息可用于将偏差与模型接收的数据量相关联。

- 该图表还显示年龄在 31 岁到 35 岁之间的群体接收到 91% 的预期结果。这表示偏差的来源，意味着该组中的数据导致结果偏差，并导致参考类的预期结果百分比增加。此信息可用于标识数据的各个部分，然后可在重新训练模型时对该数据进行低采样。

- 图表显示的另一个重要内容是包含已标识为手动标记的数据的表的名称。只要算法在模型中检测到偏差，它就还会识别可发送以由人类进行手动标记的数据点。然后，可以使用此手动标记的数据以及原始训练数据来重新训练模型。此经过重新训练的模型可能不会有偏差。手动标记表存在于与 {{site.data.keyword.aios_short}} 实例关联的数据库中。
