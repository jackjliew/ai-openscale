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

# 质量度量概述 ![beta 标记](images/beta.png)
{: #anlz_metrics}

使用质量监视来确定模型预测结果的精确程度。启用了质量监视时，缺省情况下，每小时生成一组度量。您也可以通过单击**立即检查质量**按钮或使用 Python 客户机，根据需要来生成这些度量。

质量度量的计算是基于以下信息：

- 手动标注的反馈数据，
- 针对这些数据所监视的部署响应

为了进行适当的监视，必须定期将反馈数据记录到 {{site.data.keyword.aios_short}} 中。可使用“添加反馈数据”选项或使用 Python 客户机或 REST API 来提供反馈数据。

对于除 {{site.data.keyword.aios_short}} 以外的机器学习引擎（如 Microsoft Azure ML Studio、Microsoft Azure ML Service 或 Amazon Sagemaker ML），质量监视会在受监视的部署上创建其他评分请求。
{: note}

您可以在 {{site.data.keyword.aios_short}} 仪表板上查看一段时间内的所有度量值：

![显示 ROC 下面积漂移的质量度量图表](images/quality_metrics_001.png)


要复审适用于某些度量的相关详细信息（例如用于二元和多类分类的混淆矩阵），请单击图表。

![质量度量的详细信息表](images/quality_metrics_002.png)

## 支持的质量度量
{: #anlz_metrics_supqualdets}

{{site.data.keyword.aios_short}} 支持以下质量度量：

- [ROC 下的面积](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_roc)
- [PR 下的面积](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality-area-pr)
- [准确性](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-accuracy-opener)
- [真正率 (TPR)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_tpr)
- [误报率 (FPR)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_fpr_false)
- [查全率](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_recall)
- [查准率](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_precision)
- [F1 度量](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_f1-measr)
- [对数损失](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_log_loss)

## 支持的质量详细信息
{: #anlz_metrics_supqualdets_suppr_dets}

{{site.data.keyword.aios_short}} 支持以下质量度量的以下详细信息：

### 混淆矩阵
{: #anlz_metrics_supqualdets_confusion-quickovr}

混淆矩阵可帮助您了解受监视部署响应对于哪些反馈数据来说正确，以及对于哪些反馈数据不正确。

有关更多信息，请参阅[混淆矩阵](/docs/services/ai-openscale?topic=ai-openscale-it-conf-mtx)。
