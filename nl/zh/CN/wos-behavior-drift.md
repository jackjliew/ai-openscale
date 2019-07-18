---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: drift, behavior, metrics

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

# 漂移检测 ![beta 标记](images/beta.png)
{: #behavior-drift-ovr}

随着时间的推移，模型中某些特征的重要性和影响会发生更改。这会影响关联的应用程序和产生的业务结果。通过漂移检测，{{site.data.keyword.aios_short}} 提供了一种方法来跟踪模型度量、模型性能以及特征权重随时间变化的方式。
{: shortdesc}

## 了解漂移检测
{: #behavior-drift-understand}

漂移是指由于隐藏的上下文而导致预测性能随时间推移下降。当数据随时间推移发生更改时，模型进行准确预测的能力可能会衰退。{{site.data.keyword.aios_short}} 会检测并突出显示漂移，以便您可以采取纠正行动。


### 工作方式
{: #behavior-drift-works}

{{site.data.keyword.aios_short}} 分析所有事务以查找造成漂移的事务。然后，它根据在造成漂移的过程中作用显著的属性值对记录进行分组。

### 测算
{: #behavior-drift-math}

{{site.data.keyword.aios_short}} 每隔三个小时便会通过分析预测模型已经分析的相同训练数据来计算漂移。然后，将结果与模型的预测进行比较。如果有更改或差异，那么 {{site.data.keyword.aios_short}} 将计算漂移的程度，并且根据所设置的阈值，提醒您出现漂移。 


### 漂移可视化
{: #behavior-drift-display}

漂移可视化同时包含图形和数字统计数据：

![公平性度量图表，显示了低于设置阈值的漂移](images/drift-example.png)

通过单击图表，可以显示造成漂移的特定事务。系统会显示检测到漂移的主要原因，并且包括观察的自然语言描述以及意外值列表。

![公平性度量图表，显示了低于设置阈值的漂移](images/drift-detection-example.png)

系统在事务详细信息屏幕中提供漂移事务，可以在该屏幕中单击**解释**来了解特定事务如何划分为漂移类别：

![公平性度量图表，显示了低于设置阈值的漂移](images/drift-detection-transactions.png)


## 后续步骤

- 有关如何解释漂移的信息，请参阅[配置漂移监视器](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-config)
- 通过阅读[使用 IBM Watson OpenScale 了解模型漂移](https://medium.com/@manish.bhide/4c5401aa8da4)来增加漂移 IQ
