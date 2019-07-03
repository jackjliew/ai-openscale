---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

随着时间的推移，模型中某些特征的重要性和影响会发生更改。这会影响关联的应用程序和产生的业务结果。通过漂移检测，{{site.data.keyword.aios_short}} 提供了一种方法来跟踪模型度量、模型性能以及特征权重随时间变化的方式。偏移是指由于隐藏的上下文而导致预测性能随时间推移下降。当数据随时间推移发生更改时，模型进行准确预测的能力可能会衰减。{{site.data.keyword.aios_short}} 会检测并突出显示漂移，以便您可以采取纠正行动。
{: shortdesc}

{{site.data.keyword.aios_short}} 分析所有事务以查找造成漂移的事务。然后，它根据在造成漂移的过程中作用显著的属性值对记录进行分组。

## 漂移概览
{: #behavior-drift-glance}




## 解释显示内容
{: #behavior-drift-display}

![公平性度量图表，显示了低于设置阈值的漂移](images/fairness_metrics_001.png)


## 测算
{: #behavior-drift-math}

{{site.data.keyword.aios_short}} 计算漂移 
