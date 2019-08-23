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

# 解释分类模型
{: #ie-class}

此可解释性示例表示用于核准或拒绝保险索赔的二元分类模型。在此情况下，您可以看到对于最终结果 `DENIED` 造成有利或不利影响的因素。
{: shortdesc}

值为 `<ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling serviceyear` 的特征 *POLICY AGE* 在决定 DENIED 结果的模型中具有最大影响。导致此结果的其他特征为 *CLAIM FREQUENCY* (`High`) 和 *AGE* (`18`)，而 *CAR VALUE* (`$50,000`) 仅产生轻微影响。

![显示可解释性二元分类，其中包含有关已拒绝和已核准的声明的详细信息](images/insight-explain-binary.png)

虽然图表有助于显示确定事务结果的最重要因素，但分类模型还可以包含 `Minimum changes for Approved outcome` 和 `Minimum changes for this outcome` 部分中详述的高级解释。

高级解释不适用于回归、图像和非结构化文本模型。
{: note}

`Minimum changes for Approved outcome` 表明如果特征的值更改为此部分中所列的值，那么模型的预测将更改。

同样，`Minimum changes for this outcome` 表明即使特征的值更改为此部分中所列的值，模型的预测也不会更改。

因此，这两个值表明正在为其生成解释的数据点附近的模型行为。

![可解释性二元分类详细信息，其中包含更改结果所需的最少更改](images/insight-explain-binary2.png)
