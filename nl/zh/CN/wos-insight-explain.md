---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: explainability, monitoring, explain, explaining, transactions, transaction ID

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# 解释事务
{: #ie-ov}

对于每个部署，您可以查看特定事务的可解释性数据。
仅当存在支持监视器且基于所设置的阈值的数据、监视器计划运行的时间，并且来自 {{site.data.keyword.pm_full}} 的有效内容数据可用时，才会显示事务。
{: shortdesc}

## 按事务标识查看解释
{: #ie-view}

1. 单击部署磁贴。
2. 单击导航器中的**解释事务**选项卡 (![“解释事务”选项卡](images/insight-transact-tab.png))。
3. 输入事务标识。

只要将数据发送到模型进行评分，它就会通过设置 `X-Global-Transaction-Id` 字段在 HTTP 头中设置事务标识。此事务标识存储在载荷表中。要针对特定评分查找模型行为的解释，请指定与该评分请求关联的事务标识。请注意，此行为仅适用于 {{site.data.keyword.pm_full}} 事务，不适用于非 WML 事务。
{: note}

## 在 {{site.data.keyword.aios_short}} 中查找事务标识
{: #ie-find}

1.  从部署的时间图表，在图表中滑动标记，然后单击**查看详细信息**链接以[可视化特定小时的数据](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet)。
1.  单击**查看事务**按钮以[查看事务标识列表](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra)。
1.  从列表中复制其中一个事务标识，将其粘贴到**解释事务**页面上的搜索框中，然后按 Enter 键。

    事务标识的列表还可选择仅单击任何事务标识的“操作”列中的**解释**链接，这将在“可解释性”选项卡中打开该事务。
    {: note}

  请参阅以下部分以获取不同类型模型的解释示例。

  ![可解释性事务标识](images/insight-explain-trans-id.png)

## 通过图表详细信息查找解释
{: #ie-view-ui}

由于存在针对公平性和漂移度量的解释，因此可以单击图表来获取数据集的详细视图，然后单击**查看事务**按钮以获取公平性度量，或者单击漂移事务磁贴以查看事务解释。

- 对于其中一个公平性属性（如性别或年龄），请单击该属性，再单击图表，然后单击**查看事务**按钮。
- 对于漂移监视器，请单击**漂移量级**，再单击图表，然后单击磁贴以查看与特定漂移组关联的事务。

## 后续步骤
{: #ie-trans-id-next}

- [解释分类模型](/docs/services/ai-openscale?topic=ai-openscale-ie-class)
- [解释图像模型](/docs/services/ai-openscale?topic=ai-openscale-ie-image)
- [解释非结构化文本模型](/docs/services/ai-openscale?topic=ai-openscale-ie-unstruct)
- [对比解释](/docs/services/ai-openscale?topic=ai-openscale-ie-pp-pn)
