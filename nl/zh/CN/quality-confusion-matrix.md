---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, confusion matrix

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

# 混淆矩阵 ![beta 标签](images/beta.png)
{: #it-conf-mtx}

作为质量度量的详细信息，您可以查看模型未正确分析的记录。对于二元分类模型，此类异常可能表示误报或漏报，对于多类模型，则可能表示类赋值不正确。您还可以查看模型未正确分析的反馈记录的列表。
{: shortdesc}

要复审适用于某些度量的相关详细信息（例如用于二元和多类分类的混淆矩阵），请单击图表。

![质量度量的详细信息表](images/quality_metrics_002.png)

## 步骤
{: #it-conf-mtx-steps}

1. 从任何**质量**图表（例如**准确性**）中，单击图表中的小时/天。
    
    ![事务列表 - 有偏差](images/Confusion_Matrix_040819.004.png)

1. 混淆矩阵显示误报和漏报。 单击单元格可查看反馈记录的子集。

    ![事务列表 - 有偏差](images/Confusion_Matrix_040819.005.png)

1. 查看反馈记录并请求对反馈记录的分析结果进行说明。

    ![事务列表 - 有偏差](images/Confusion_Matrix_040819.006.png)

1. 事务以内联方式显示。

    ![事务列表 - 有偏差](images/Confusion_Matrix_040819.007.png)

