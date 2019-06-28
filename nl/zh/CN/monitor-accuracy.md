---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: accuracy, 

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# 准确性
{: #acc-monitor}

通过准确性，您可以了解模型预测结果的程度。
{: shortdesc}

## 了解准确性
{: #acc-understand}

根据算法的类型，准确性可以表示不同的事项：

- *多类分类*：准确性测量正确预测任何类的次数，按数据点的数量进行标准化。有关更多详细信息，请参阅 Apache Spark 文档中的 [Multi-class classification ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#multiclass-classification){: new_window}。

- *二元分类*：对于二元分类算法，准确性测量为 ROC 曲线下的面积。有关更多详细信息，请参阅 Apache Spark 文档中的 [Binary classification ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#binary-classification){: new_window}。

- *回归*：回归算法使用决定系数或 R2 进行测量。有关更多详细信息，请参阅 Apache Spark 文档中的 [Regression model evaluation ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#regression-model-evaluation){: new_window}。

### 工作方式
{: #acc-works}

您需要使用 [Python 客户机 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://ai-openscale-python-client.mybluemix.net/#feedbacklogging){: new_window} 或 [Rest API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/apidocs/ai-openscale#post-feedback-payload){: new_window} 通过 {{site.data.keyword.aios_short}} UI 来添加手动标记的反馈数据，如下所示。

请查看[支持的框架](/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-fram)以了解准确性监视限制。

### 已除偏准确性
{: #acc-debias-view}

只要数据支持除偏，模型的准确性即包含原始模型和已除偏模型。{{site.data.keyword.aios_full_notm}} 计算已除偏输出的准确性并将其作为附加列存储在有效内容日志记录表中。

![显示已为原始模型和已除偏模型计算准确性的模型可视化](images/debiased-accuracy.png)

## 配置准确性监视器
{: #acc-config}

1.  从*什么是准确性？*页面中，单击**下一步**以启动配置过程。

    ![“什么是准确性？”页面](images/accuracy-what-is.png)

1.  在*设置准确性阈值*页面上，选择表示可接受的准确性级别的值。

    准确性是从与每个特定模型类型关联的相关数据科学度量中合成的值。分数是使您能够轻松比较不同模型类型的准确性的标准化测量。在典型情况下，准确性分数为 80 便已足够。{: note}

    ![设置准确性限制](images/accuracy-set-limit.png)

    单击**下一步**以继续。

1.  现在，设置最小和最大样本大小。最小大小防止在评估数据集中提供最小数量的记录之前测量准确性；这确保样本大小不会太小而导致结果偏差。最大样本大小帮助更好地管理评估数据集所需的时间和工作；仅当超过此大小时，才会评估最新记录。

     ![配置样本大小](images/accuracy-config-sample.png)

1.  单击**下一步**按钮。

    系统会呈现您的选择的摘要以供查看。如果要更改任何内容，请单击该部分的**编辑**链接。

1.  单击**保存**以完成配置。

现在，系统会呈现一个用于直接向模型提供反馈数据的选项，以评估准确性。

  ![发送反馈数据](images/accuracy-send-feedback0.png)

选择*添加反馈数据*按钮以上载 CSV 格式的数据文件；设置定界符以匹配您的数据。

反馈 CSV 文件预计具有所有特征值以及手动分配的目标/标签值。例如，药品模型训练数据包含特征值 `"AGE"`、`"SEX"`、`"BP"`、`"CHOLESTEROL"`、`"NA"`、`"K"` 以及目标/标签值 `"DRUG"`。反馈 CSV 文件需要包含这些字段的值；例如 `[43, M, HIGH, NORMAL, 0.6345, 1.4587, DrugX]`。如果为反馈 CSV 文件提供了标题，那么将使用该标题来映射字段名称。否则，字段顺序**必须**与训练模式中的顺序完全相同。
有关训练数据的更多信息，请参阅[为什么 {{site.data.keyword.aios_short}} 需要访问我的培训数据？](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)
{: important}

请注意，模型返回的预测类型与反馈数据中的标签/目标列必须匹配。
{: note}

  ![准确性定界符](images/accuracy-delimit.png)

文件大小当前限制为 8 MB。
{: note}

或者，可以使用提供的 `cURL` 或 `Python` 代码片段来发布反馈数据。

需要将代码片段中的字段和值替换为真实值，因为其中提供的值仅作参考之用。
{: important}

您还可以选择**退出**来跳过此可选步骤；您仍将可以稍后上载 CSV 文件以进行评估。

### 后续步骤
{: #acc-next}

从*配置监视器*页面中，可以选择其他监视类别。
