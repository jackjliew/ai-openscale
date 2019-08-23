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

# 对比解释使用准正和准负
{: #ie-pp-pn}

对于对比解释，{{site.data.keyword.aios_short}} 显示准正值和准负值。
{: shortdesc}

- 准正是指对于确定事物性质至关重要的发现结果。
- 准负是指不可或缺的非发现结果。

{{site.data.keyword.aios_short}} 始终显示准正，但是，有时没有任何要显示的准负。在此情况下，此特征的值已处于中值，或者预测尚未由于这些值偏离中值而发生更改。

为了更好地对此加以理解，假设在 {{site.data.keyword.aios_short}} 计算准负值时，它偏离所有特征的中值对特征值进行更改。对于准负，这表示距离中值最远的特征值。如果某个数据点的值已处于中值，或者即使在偏离中值来更改这些值后，预测没有更改，那么没有任何要显示的准负。在准正情况下，{{site.data.keyword.aios_short}} 发现趋向中值的特征值变化最大，致使预测不会发生更改。实际上，这意味着几乎始终存在用于解释事务的准正。

