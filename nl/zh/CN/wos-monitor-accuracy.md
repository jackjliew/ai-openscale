---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: accuracy, 

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

# 配置“质量（准确性）”监视器
{: #acc-monitor}

通过“质量”监视器（以前称为“准确性”监视器），可以了解模型预测结果的准确度。
{: shortdesc}

## 配置步骤
{: #acc-config}

从**什么是“质量”监视器？**页面上的**质量**选项卡中，单击**开始**以启动配置过程。

![显示“什么是‘质量’监视器？”页面，其中解释了质量监视器评估模型预测准确结果的程度](images/wos-quality-what-is.png)

在“准确性”配置选项卡的连续页面上配置以下设置：

-  设置准确性警报阈值。选择表示可接受的准确性级别的值。例如，如果针对交互式教程使用的是**德国信用风险模型**，请将警报设置为 **90%**。

    准确性是从与每个特定模型类型关联的相关数据科学度量中合成的值。分数是使您能够轻松比较不同模型类型的准确性的标准化测量。在典型情况下，准确性分数为 80 便已足够。对于本教程，要生成更多数据，建议使用 90。
    {: note}

-  设置最小和最大样本大小。最小大小防止在评估数据集中提供最小数量的记录之前测量准确性；这确保样本大小不会太小而导致结果偏差。最大样本大小帮助更好地管理评估数据集所需的时间和工作；仅当超过此大小时，才会评估最新记录。例如，如果针对交互式教程使用的是**德国信用风险模型**，请将最小样本大小设置为 **100**，并将最大样本大小设置为 **10000**。


系统会呈现您的选择的摘要以供查看。如果要更改任何内容，请单击该部分的**编辑**链接。否则，单击**保存**以完成配置。

### 后续步骤
{: #acc-next}

要继续配置监视器，请单击**公平性**选项卡，然后单击**开始**。有关更多信息，请参阅[配置公平性监视器](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)。
