---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, Fairness for a group, sex, age, race

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

# 组的公平性
{: #quality_group}

组度量的“公平性”使模型倾向于传递一个组相对于另一个组更有利的结果。组可以是任意组，例如年龄、性别或种族。
{: shortdesc}


## 组的公平性概览
{: #quality_group-glance}

- **描述**：模型倾向于在组之间传递有利结果。
- **缺省阈值**：下限 = 80%
- **缺省建议**：去偏差评分端点，可供在您的业务应用程序中用于从部署模型中接收去偏差响应。
- **问题类型**：全部
- **数据类型**：结构化
- **图表值**：时间范围内的最后一个值
- **度量详细信息是否可用**：可用

## 受保护属性
{: #quality_group-atts}

{{site.data.keyword.aios_short}} 自动识别模型中是否存在任何已知的受保护属性。当 {{site.data.keyword.aios_short}} 检测到这些属性时，它会自动建议为存在的每个属性配置偏差监视器，以确保在生产中跟踪针对这些潜在敏感属性的偏差。 

### sex
{: #quality_group-sex}

{{site.data.keyword.aios_short}} 建议在 **Sex** 属性中配置偏差监视器，以便 `Woman` 和 `Non-Binary` 为受监视值，`Male` 为参考值。 

### ethnicity
{: #quality_group-ethnicity}

{{site.data.keyword.aios_short}} 建议在 **ethnicity** 属性中配置偏差监视器，以便 `White-caucasian` 为参考值，而其他种族为受监视值。

### marital status
{: #quality_group-marital}

{{site.data.keyword.aios_short}} 建议在 **marital status** 属性中配置偏差监视器，以便 `married` 为参考值，`single` 为受监视值。

### age
{: #quality_group-age}

{{site.data.keyword.aios_short}} 建议在 **age** 属性中配置偏差监视器，以便年龄范围产生可行除偏。

### zip code
{: #quality_group-zip}

{{site.data.keyword.aios_short}} 建议在 **zip code** 属性中配置偏差监视器，以便对个别邮政编码进行评分。
