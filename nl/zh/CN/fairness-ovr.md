---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

# 公平性度量概述
{: #anlz_metrics_fairness}

使用 {{site.data.keyword.aios_full}} 公平性监视来确定模型生成的结果对于受监视组是否公平。启用了公平性监视时，缺省情况下，每小时生成一组度量。您也可以通过单击**立即检查质量**按钮或使用 Python 客户机，根据需要来生成这些度量。
{: shortdesc}

{{site.data.keyword.aios_short}} 自动识别模型中是否存在任何已知的受保护属性。当 {{site.data.keyword.aios_short}} 检测到这些属性时，它会自动建议为存在的每个属性配置偏差监视器，以确保在生产中跟踪针对这些潜在敏感属性的偏差。 

目前，{{site.data.keyword.aios_short}} 检测以下受保护属性并为其建议监视器： 

- sex
- ethnicity
- marital status
- age
- zip code

除检测受保护属性以外，{{site.data.keyword.aios_short}} 还建议应将每个属性中的哪些值设置为受监视值和参考值。因此，例如，{{site.data.keyword.aios_short}} 建议在“Sex”属性中配置偏差监视器，以便“Woman”和“Non-Binary”为受监视值，“Male”为参考值。如果要更改任何建议，那么可以通过偏差配置面板对其进行编辑。 

建议的偏差监视器有助于加速配置，并确保您正在检查 AI 模型以了解针对敏感属性的公平性。随着监管者开始对算法偏差更加密切关注，各组织清楚了解其模型的性能及其是否针对特定组生成不公平结果变得日益重要。 

公平性度量的计算是基于以下信息：

- 载荷数据的评分。

为了进行适当的监视，每个评分请求也应该记录在 {{site.data.keyword.aios_short}} 中。对于 {{site.data.keyword.pm_full}} 引擎，将自动进行载荷数据记录。

对于其他机器学习引擎，可以使用 Python 客户机或 REST API 来提供载荷数据。

对于除 {{site.data.keyword.pm_full}} 以外的机器学习引擎，公平性监视会在受监视的部署上创建其他评分请求。
{: note}

您可以在 {{site.data.keyword.aios_short}} 仪表板上查看一段时间内的所有度量值：

![公平性度量图表，显示了低于设置阈值的漂移](images/fairness_metrics_001.png)

您可以查看相关详细信息，例如有利结果和不利结果：

![公平性详细信息](images/fairness_metrics_002.png)

您可以查看详细事务：

![显示事务列表的公平性图表](images/fairness_metrics_003.png)

您可以查看建议的去偏差评分端点：

![去偏差评分端点详细信息](images/fairness_metrics_004.png)

### 支持的公平性度量
{: #anlz_metrics_supfairmets}

{{site.data.keyword.aios_short}} 支持以下公平性度量：

- [组的公平性](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_group)

{{site.data.keyword.aios_short}} 支持以下受保护属性： 

- [sex](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-sex)
- [ethnicity](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-ethnicity)
- [marital status](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-marital)
- [age](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-age)
- [zip code](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-zip)


### 受支持公平性的详细信息
{: #anlz_metrics_supfairdets}

{{site.data.keyword.aios_short}} 支持以下公平性度量的以下详细信息：

- 每个组的有利百分比
- 所有公平性组的公平性平均值

```
                          (% of favorable outcome in monitored group
Disparate Impact Ratio =  ____________________________________________
                          (% of favorable outcome in reference group)
```

- 每个受监视组的数据分布
- 载荷数据的分布
