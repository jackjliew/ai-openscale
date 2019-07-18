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

# 准确性
{: #accuracy-opener}

准确性用于度量模型中包含的正确预测的比例。
{: shortdesc}

## 准确性概览
{: #anlz_metrics_supqualdets_acc}

- **描述**：正确预测的比例
- **缺省阈值**：下限 = 80%
- **缺省建议**：
   - **上升趋势**：上升趋势表明度量正在改善。这意味着，模型再训练是有效的。
   - **下降趋势**：下降趋势表明度量正在恶化。 反馈数据正在变得明显不同于训练数据。
   - **错误或不规则的变体**：错误或不规则的变体表明反馈数据在不同求值期间不一致。 此时请增大质量监视器的最小样本大小。
- **问题类型**：二元分类和多类分类
- **图表值**：时间范围内的最后一个值
- **度量详细信息是否可用**：混淆矩阵


## 了解准确性
{: #acc-understand}

根据算法的类型，准确性可以表示不同的事项：

- *多类分类*：准确性测量正确预测任何类的次数，按数据点的数量进行标准化。有关更多详细信息，请参阅 Apache Spark 文档中的[多类分类](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#multiclass-classification){: external}。

- *二元分类*：对于二元分类算法，准确性测量为 ROC 曲线下的面积。有关更多详细信息，请参阅 Apache Spark 文档中的[二元分类](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#binary-classification){: external}。

- *回归*：回归算法使用决定系数或 R2 进行测量。有关更多详细信息，请参阅 Apache Spark 文档中的[回归模型评估](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#regression-model-evaluation){: external}。

### 工作方式
{: #acc-works}

您需要使用 [Python 客户机](http://ai-openscale-python-client.mybluemix.net/#feedbacklogging){: external}或 [Rest API](https://cloud.ibm.com/apidocs/ai-openscale#post-feedback-payload){: external} 通过 {{site.data.keyword.aios_short}} UI 来添加手动标记的反馈数据，如以下示例中所示。

请查看[支持的框架](/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-fram)以了解准确性监视限制。

### 已除偏准确性
{: #acc-debias-view}

在有数据可支持计算的情况下，会在原始模型和已除偏模型上计算准确性。{{site.data.keyword.aios_full_notm}} 计算已除偏输出的准确性并将其作为附加列存储在有效内容日志记录表中。

![显示已为原始模型和已除偏模型计算准确性的模型可视化](images/debiased-accuracy.png)
