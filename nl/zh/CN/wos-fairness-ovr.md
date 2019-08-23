---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds

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

# 公平性度量概述
{: #anlz_metrics_fairness}

使用 {{site.data.keyword.aios_full}} 公平性监视来确定模型生成的结果对于受监视组是否公平。启用了公平性监视时，缺省情况下，每小时生成一组度量。您也可以通过单击**立即检查质量**按钮或使用 Python 客户机，根据需要来生成这些度量。
{: shortdesc}

{{site.data.keyword.aios_short}} 自动识别模型中是否存在任何已知的受保护属性。当 {{site.data.keyword.aios_short}} 检测到这些属性时，它会自动建议为存在的每个属性配置偏差监视器，以确保在生产中跟踪针对这些潜在敏感属性的偏差。 

目前，{{site.data.keyword.aios_short}} 检测以下受保护属性并为其建议监视器： 

- sex
- ethnicity
- marital status
- age
- zip code

除检测受保护属性以外，{{site.data.keyword.aios_short}} 还建议应将每个属性中的哪些值设置为受监视值和参考值。因此，例如，{{site.data.keyword.aios_short}} 建议在“Sex”属性中配置偏差监视器，以便“Woman”和“Non-Binary”为受监视值，“Male”为参考值。如果要更改任何建议，那么可以通过偏差配置面板对其进行编辑。 

建议的偏差监视器有助于加速配置，并确保您正在检查 AI 模型以了解针对敏感属性的公平性。随着监管者开始对算法偏差更加密切关注，各组织清楚了解其模型的性能及其是否针对特定组生成不公平结果变得日益重要。

## 了解公平性
{: #mf-understand}

{{site.data.keyword.aios_short}} 在运行时检查已部署模型是否存在偏差。要检测已部署模型的偏差，必须定义 Age 或 Gender 之类的公平性属性，如下面的[配置公平性监视器](#mf-config)部分中所详述。

必须在 {{site.data.keyword.pm_short}} 中指定模型或函数的输出模式，以在 {{site.data.keyword.aios_short}} 中启用偏差检查。可以使用 `store_model` API 的元数据部分中的 `client.repository.ModelMetaNames.OUTPUT_DATA_SCHEMA` 属性来指定输出模式。有关更多信息，请参阅 [{{site.data.keyword.pm_full}} 客户机文档](http://wml-api-pyclient-dev.mybluemix.net/#repository){: external}。

### 工作方式
{: #mf-works}

在配置公平性监视器之前，有几个要了解的至关重要的关键概念：

- 公平性属性是模型可能展现偏差的模型属性。例如，对于公平性属性 **`Gender`**，模型可能针对特定性别值（`Female` 或`Transgender` 等）存在偏差。公平性属性的另一个示例是 **`Age`**，其中模型可能会针对年龄组（例如 `18 to 25`）中的人员展现偏差。

- 参考值和受监视值：公平性属性的值分为两个不同类别：“参考”和“受监视”。受监视值是指可能会区分对待的值。对于诸如 **`Gender`** 之类的公平性属性，受监视值可能为 `Female` 和 `Transgender`。对于数字公平性属性（例如 **`Age`**），受监视值可能为 `[18-25]`。然后，给定公平性属性的所有其他值会被视为参考值，例如 `Gender=Male` 或 `Age=[26,100]`。

- 有利和不利结果：模型的输出分类为“有利”或“不利”。例如，如果模型预测的是某个人是否应获得贷款，那么有利结果可能为 `Loan Granted` 或 `Loan Partially Granted`，而不利结果可能为 `Loan Denied`。因此，有利结果是被视为肯定结果的结果，而不利结果被视为否定。

{{site.data.keyword.aios_short}} 使用载荷日志记录表中的最后 `N` 个记录每小时计算偏差；在配置“公平性”时会指定值 `N`。算法会扰动这最后 `N` 个记录以生成其他数据。

通过将公平性属性的值从“参考”更改为“受监视”可执行扰动，反之亦然。然后，会将扰动数据发送到模型以评估其行为。算法会查看载荷表中的最后 `N` 个记录，以及模型在扰动数据上的行为，以决定模型行为是否有偏差。

如果在此组合数据集中，受监视类的有利结果的百分比小于参考类的有利结果的百分比（差异达到某个阈值），那么会将模型视为有偏差。在配置公平性时将指定此阈值。

公平性值可以大于 100%。这意味着受监视组接收到的有利结果数超过参考组。此外，如果未发送新的评分请求，那么公平性值将保持不变。
{: note}

### 测算
{: #mf-bias-math}

{{site.data.keyword.aios_short}} 中使用的公平性度量是差别影响，它用于度量无特权组接收特定结果的速率与特权组接收同一结果的速率的比较情况。

以下数学公式用于计算差别影响：

```
                     (num_positives(privileged=False) / num_instances(privileged=False))
Disparate impact =   ______________________________________________________________________

                     (num_positives(privileged=True) / num_instances(privileged=True))
```

其中 `num_positives` 是组中接收到肯定结果的个人的数量（privileged=False，即无特权；或 privileged=True，即有特权），num_instances 是组中个人的总数。

产生的数字将是百分比，即，非特权组接收肯定结果的速率占特权组接收肯定结果的速率的百分比。例如，如果信用风险模型将“no risk”预测分配给 80% 的无特权申请人和 100% 的特权申请人，那么模型将具有 80% 的差别影响（呈现为 {{site.data.keyword.aios_short}} 中的公平性分数）。

在 {{site.data.keyword.aios_short}} 中，肯定结果指定为有利结果，否定结果指定为不利结果。特权组指定为参考组，无特权组指定为受监视组。


### 偏差可视化 ![beta 标签](images/beta.png)
{: #mf-monitor-bias-viz}

当检测到潜在偏差时，{{site.data.keyword.aios_short}} 将执行多个函数以确认偏差是否真实。{{site.data.keyword.aios_short}} 通过根据参考值翻动受监视值，然后通过模型运行此新记录来扰动数据。随后，它会将生成的输出显示为已除偏输出。{{site.data.keyword.aios_short}} 还会训练影子已除偏模型，然后，它将使用该模型来检测模型何时将作出有偏差预测。 

使用两个不同的数据集来计算公平性和准确性。使用有效内容 + 扰动数据来计算公平性。使用反馈数据来计算准确性。要计算准确性，{{site.data.keyword.aios_short}} 需要手动标记的数据，该数据仅出现在反馈表中。

这些决定的结果可在偏差可视化中获取，其中包含以下视图。（仅当存在要支持的数据时，您才会看到视图）

- **有效内容 + 扰动量**：包括在所选小时内接收到的评分请求以及前几个小时的其他记录（如果未满足评估所需的最小记录数）。包含其他扰动/合成的记录，用于在受监视功能部件的值发生更改时测试模型的响应。

   记录以下有效内容和扰动量详细信息：

   - 当前小时内从有效内容表中读取的记录数
   - 从前几个小时内读取的其他记录（例如，如果公平性配置中的 `min_records` 值设置为 1000，并且在下午 2 点到 3 点之间仅添加了 10 个记录，那么要满足最低需求，系统将会从前几个小时内读取另外 990 个记录。）
   - 每个公平性属性的扰动记录数
   - 必须计算偏差的数据帧中的最旧记录时间戳记
   - 必须计算偏差的数据帧中的最新记录时间戳记

  ![有效内容和扰动量的示例](images/payload&perturbed.png)



- **有效内容**：模型在所选小时内接收到的实际评分请求。

   记录以下有效内容详细信息：
   
   - 从有效内容表中读取/对其执行了除偏操作的记录数
   - 必须计算偏差的数据帧中的最旧记录时间戳记
   - 必须计算偏差的数据帧中的最新记录时间戳记


  ![有效内容数据的示例](images/payload.png)

- **训练**：用于训练模型的训练数据记录。

   记录以下训练详细信息：
   
   - 训练数据记录数。系统会读取一次训练数据，并将分布存储在 `subscription/fairness_configuration` 变量中。计算分布时，还应查找训练数据记录数并将其存储在同一分布中。此外，当训练数据更改时，意味着如果再次运行 `POST /data_distribution` 命令，那么将在 `fairness_configuration/training_data_distribution` 变量中更新该值。发送度量时，也应发送该值。
   - 上次处理训练数据的时间（首次和后续更新）

  ![训练数据的示例](images/training.png)
   

   
- **除偏**：处理运行时数据和扰动数据后除偏算法的输出。选择**已除偏**单选按钮会向您显示已除偏模型与生产中模型相比较的更改。图表反映组的结果状态有所改进。


   记录以下除偏详细信息：
   
   - 从有效内容表中读取/对其执行了除偏操作的记录数
   - 所读取的要执行偏差并因此也已除偏的其他记录。数量与`有效内容 + 扰动量`选择中相同
   - 每个公平性属性的扰动记录数
   - 必须计算偏差的数据帧中的最旧记录时间戳记
   - 必须计算偏差的数据帧中的最新记录时间戳记
   - 在已除偏视图的标题部分中会显示“之前”和“之后”公平性值。 
      - 通过采集反馈数据并将其发送到主动除偏 API 来计算**之后**准确性。此 API 返回已除偏预测。反馈数据还包含手动标签。手动标签与已除偏预测进行比较以计算准确性。此 API 返回已除偏预测。反馈表也包含手动标签。手动标签与已除偏预测进行比较以计算准确性。 
      - 通过使用相同反馈数据来计算**之后**准确性。对于“之前”准确性计算，会将反馈数据发送到模型以获取其预测，并将预测值与手动标签进行比较以获取准确性。

  ![除偏数据的示例](images/debiased.png)
  
### 示例
{: #mf-ex1}

假设一个数据点，其中，对于 `Gender=Male`（参考值），模型预测有利结果，但在通过将 `Gender` 更改为 `Female`（受监视值）来扰动记录时，在将所有其他特征值保持相同的情况下，模型预测不利结果。如果有足够的数据点（跨载荷表中的最后 `N` 个记录，加上扰动数据），其中模型行为有偏差，那么会将模型整体视为展现偏差。

### 支持的模型
{: #mf-supmo}

 {{site.data.keyword.aios_short}} 仅支持对在其特征向量中期望某种类型的结构化数据的模型和 Python 函数进行偏差检测。

公平性度量的计算是基于以下信息：

- 载荷数据的评分。

为了进行适当的监视，每个评分请求也应该记录在 {{site.data.keyword.aios_short}} 中。对于 {{site.data.keyword.pm_full}} 引擎，将自动进行载荷数据记录。

对于其他机器学习引擎，可以使用 Python 客户机或 REST API 来提供载荷数据。

对于除 {{site.data.keyword.pm_full}} 以外的机器学习引擎，公平性监视会在受监视的部署上创建其他评分请求。
{: note}

您可以在 {{site.data.keyword.aios_short}} 仪表板上查看一段时间内的所有度量值：

![公平性度量图表，显示了低于设置阈值的漂移](images/fairness_metrics_001.png)

您可以查看相关详细信息，例如有利结果和不利结果：

![公平性详细信息](images/fairness_metrics_002.png)

您可以查看详细事务：

![显示事务列表的公平性图表](images/fairness_metrics_003.png)

您可以查看建议的去偏差评分端点：

![去偏差评分端点详细信息](images/fairness_metrics_004.png)

### 支持的公平性度量
{: #anlz_metrics_supfairmets}

{{site.data.keyword.aios_short}} 支持以下公平性度量：

- [组的公平性](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_group)

{{site.data.keyword.aios_short}} 支持以下受保护属性： 

- [sex](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-sex)
- [ethnicity](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-ethnicity)
- [marital status](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-marital)
- [age](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-age)
- [zip code](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-zip)


### 受支持公平性的详细信息
{: #anlz_metrics_supfairdets}

{{site.data.keyword.aios_short}} 支持以下公平性度量的以下详细信息：

- 每个组的有利百分比
- 所有公平性组的公平性平均值

```
                          (% of favorable outcome in monitored group
Disparate Impact Ratio =  ____________________________________________
                          (% of favorable outcome in reference group)
```

- 每个受监视组的数据分布
- 载荷数据的分布
