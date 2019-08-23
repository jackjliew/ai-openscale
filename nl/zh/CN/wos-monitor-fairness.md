---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, fairness monitor, payload, perturbation, training data, debiased

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

# 配置公平性监视器
{: #mf-monitor}

在 {{site.data.keyword.aios_full}} 中，公平性监视器会扫描部署是否存在偏差，以确保不同群体的结果公平。
{: shortdesc}

## 步骤
{: #mf-config}

从**什么是公平性？**页面上的**公平性**选项卡中，单击**开始**以启动配置过程。

![“什么是公平性？”页面](images/fair-what-is.png)

在此过程中，{{site.data.keyword.aios_full}} 分析模型并根据逻辑性最强的结果作出建议。在**公平性**选项卡的连续页面上，必须执行以下任务：

1. 选择要监视的特征。仅支持公平性数据类型为分类、数字（整数）、浮点值或双精度值的特征。不支持具有其他数据类型的特征。
    

1. 指定参考组和受监视组。

   每个特征具有要配置的特定需求。例如，如果选择 `age` 作为其中一个受监视特征，那么必须通过直接在每个组中输入值来定义**参考组**和**受监视组**的年龄范围。

1.  设置特征的公平性警报阈值。

    公平性阈值用于指定受监视组的有利结果百分比相比于参考组的有利结果百分比的可接受差值。

    假设一个模型用于预测谁应获得贷款 (`favorable outcome=loan granted`)，谁不应获得贷款 (`unfavorable outcome=loan denied`)。此外，年龄的受监视值为 `[18,25]`，参考值为 `[26,100]`。当偏差检测算法运行时，如果它发现最后 `N` 个记录中年龄组 `[18,25]` 内的人员的有利结果百分比加上扰动数据为 `50%`，而年龄组 `[26,100]` 内的人员的有利结果百分比为 `70%`，那么公平性计算为 50*100/70 = 71.42。

    如果公平性阈值设置为 80%，那么算法会将模型标记为有偏差，因为计算出得公平性超过阈值。但是，如果阈值设置为 70%，那么它不会将模型报告为有偏差。

     您在这些屏幕中输入的值应是发送到模型评分端点（并因此将添加到有效内容表）的值。如果数据在发送到评分端点之前进行处理，那么输入已处理的值。例如，如果原始数据针对 *Gender* 的值为 `Male` 和 `Female`，并且它已经过处理，以便发送到评分端点的数据为 `M` 和 `F`，那么在此屏幕上输入 `M` 和 `F`。

1.  指定表示模型的有利结果的值。如果模型输出模式包含映射列，那么值将派生自[训练数据](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)中的 `label` 列。 在 {{site.data.keyword.pm_full}} 中，`prediction` 列始终具有双精度值。映射列用于指定此 `prediction` 值到类标签的映射。

    例如，如果 `prediction` 值为 `1.0`，那么映射列的值可能为 `Loan denied`；这暗示模型的预测为 `Loan denied`。因此，如果模型输出模式包含映射列，那么使用映射列中存在的值来指定“有利”和“不利”值。

    但是，如果映射列在模型输出模式中不存在，那么需要使用 `prediction` 列的值（`0.0` 或 `1.0` 等）来指定“有利”和“不利”值。

1.  最后，设置最小样本大小，以防止在评估数据集中提供最小数量的记录之前测量公平性。这确保样本大小不会太小而导致结果偏差。每次在偏差检查运行时，它将使用最小样本大小来决定将对其执行偏差计算的记录数。

    系统会呈现您的选择的摘要以供查看。如果要更改任何内容，请单击该部分的**编辑**链接，否则单击**保存**。

    您还可以单击**添加其他特征**以返回到特征选择屏幕，并将更多特征（例如 `City`、`Zip Code` 或 `Account Balance`）添加到公平性监视器。

### 了解除偏的工作方式
{: #mf-debias}

要检查除偏端点，请单击**除偏端点**按钮。然后，可以查看和复制不同格式的端点，例如 cURL、Java 或 Python。 

已除偏评分端点完全可用作已部署模型的正常评分端点。除返回已部署模型的响应以外，它还返回 `debiased_prediction` 和 `debiased_probability` 列。

- `debiased_prediction` 列包含已除偏预测值。在使用 {{site.data.keyword.pm_full}} 的情况下，这是预测的编码表示。例如，如果模型预测为“Loan Granted”或“Loan Denied”，那么 {{site.data.keyword.pm_full}} 可以将这两个值分别编码为“0.0”和“1.0”。`debiased_prediction` 列包含已除偏预测的此类编码表示。

- 另一方面，`debiased_probability` 列表示已除偏预测的概率。这是双精度值的数组，其中每个值表示属于其中一个预测类的已除偏预测的概率。

此外，还会返回另一列 `debiased_decoded_target`，以防您在输出模式中有一个列包含以 `modeling-role` 作为 `decoded-target` 的列。

- `debiased_decoded_target` 列包含已除偏预测的字符串表示。在以上示例中，如果预测值为“0.0”或“1.0”，那么 `debiased_decoded_target` 将包含“Loan Granted”或“Loan Denied”。

理想情况下，将会直接从生产应用程序调用此端点，而不是直接调用模型服务引擎（{{site.data.keyword.pm_full}}、Amazon Sagemaker、Microsoft Azure ML Studio 等）中部署的模型的评分端点。通过此方式，{{site.data.keyword.aios_short}} 也会将 `debiased` 值存储在模型部署的载荷日志记录表中。然后，通过此端点执行的所有评分都将自动除偏。

由于此端点处理运行时偏差，因此它将继续对载荷日志记录表中的最新评分数据运行背景检查，并保持更新用于对所发送的评分请求进行除偏的偏差缓解模型。通过此方式，{{site.data.keyword.aios_short}} 始终具有最新的入局数据，并且其行为会检测和缓解偏差。

最后，{{site.data.keyword.aios_short}} 使用阈值来决定数据现在是否可接受并被认为无偏差。该阈值被视为公平性监视器中为所配置的所有公平性属性设置的阈值中的最小值。

## 后续步骤
{: #mf-next}

要继续配置监视器，请单击**漂移**选项卡，然后单击**开始**。有关更多信息，请参阅[配置漂移检测监视器](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-config)。
