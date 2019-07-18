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

# 配置“准确性”或“质量”监视器
{: #acc-monitor}

通过“质量”监视器（以前称为“准确性”监视器），可以了解模型预测结果的准确度。
{: shortdesc}

## 配置步骤
{: #acc-config}

从**什么是准确性？**页面上的**准确性**选项卡中，单击**开始**以启动配置过程。

![“什么是准确性？”页面](images/accuracy-what-is.png)

在“准确性”配置选项卡的连续页面上配置以下设置：

-  设置准确性警报阈值。选择表示可接受的准确性级别的值。

    准确性是从与每个特定模型类型关联的相关数据科学度量中合成的值。分数是使您能够轻松比较不同模型类型的准确性的标准化测量。在典型情况下，准确性分数为 80 便已足够。{: note}

-  设置最小和最大样本大小。最小大小防止在评估数据集中提供最小数量的记录之前测量准确性；这确保样本大小不会太小而导致结果偏差。最大样本大小帮助更好地管理评估数据集所需的时间和工作；仅当超过此大小时，才会评估最新记录。


系统会呈现您的选择的摘要以供查看。如果要更改任何内容，请单击该部分的**编辑**链接。否则，单击**保存**以完成配置。

### 后续步骤
{: #acc-next}

从**配置监视器**页面中，可以选择其他监视类别。
