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

# 图表构建器 ![beta 标记](images/beta.png)
{: #chart_builder}

使用 {{site.data.keyword.aios_short}} 图表构建器来创建定制可视化，以便您可以在运行时更好地理解模型预测和输入。图表构建器能够根据业务认为重要的特征或数据范围来查看模型预测的输出。它有助于发现数据的新趋势，这可能会促使业务和数据科学团队考虑对 AI 模型进行更改。
{: shortdesc}

例如，如果您熟悉教程中的信用风险模型，那么可以针对属性“信用历史记录”的不同范围查看预测类的差异。 

   ![此图表按特征年龄显示性别的特征预测](images/by_custom_chart.png)
      
   您还可以在针对“信用历史记录”的这些范围进行预测时查看模型的置信度。您可以通过定制图表（在特征、预测类和置信度之间进行选择）来分析在所选数据范围内发送到部署的评分有效内容。

   ![此图表按特征年龄显示性别的特征预测](images/by_custom_chart002.png)
   
