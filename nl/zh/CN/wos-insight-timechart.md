---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, monitoring, charts, de-biasing, bias, accuracy

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

# 查看部署的数据
{: #it-vdep}

从仪表板中选择部署以查看该部署的监视数据。标题显示有关已部署模型的信息，例如**模型标识**和**创建日期**字段。
{: shortdesc}

![显示时间序列图表，其中包含一天的各个小时和公平性分数](images/insight-time-chart.png)

由于算法检查仅每小时运行一次，因此还提供了链接以按需检查公平性和质量。从**调度**面板中，可单击以下链接来对数据进行立即检查：

![显示“检查公平性”按钮](images/wos-fairness-button.png)


![显示“检查质量”按钮](images/wos-quality-button.png)

接下来，单击图表并在图表中移动标记以查看单个小时的统计信息：

![显示时间序列图表，其中选择了图表中的特定数据点，并带有工具提示，指示要单击以查看详细信息](images/wos-insight-time-detail.png)

- ***公平性***：两个公平性特征（Sex 和 Age）达到其设置的要进行核准的阈值。
- ***质量***：**ROC 下的面积**度量显示警报，因为它不在所配置的阈值范围内。
- ***每分钟平均请求数***：单击**吞吐量**度量可查看期间每分钟处理的记录数。吞吐量每分钟计算一次，并且在图表中报告了其一小时内的平均值。


## 查看事务
{: #it-tra}

通过此选项，您可以在单击**查看事务**按钮时查看导致偏差的个别事务。

![显示“查看事务”按钮](images/view_transactions.png)

系统将列出部署行为有偏差的事务的列表。单击任何事务标识的**解释**链接，以在“可解释性”选项卡中获取有关该事务的详细信息。有关更多信息，请参阅[监视可解释性](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)。

选择**所有事务**视图以查看所选特征（在此示例中为“AGE”）和所选时间段（在此示例中为“September 15, 2018 1:00 PM”）中的所有事务：

![“事务”列出特定数据点的所有事务](images/transaction_list1.png)

选择**有偏差事务**视图以仅查看事务中接收到有偏差结果的子集。每个有偏差事务与类似但略有更改（扰动）的事务进行比较，从而显示更改受监视特征 (AGE) 的值将如何导致有偏差事务产生有利结果：

![“事务”仅列出有偏差事务](images/transaction_list2.png)


