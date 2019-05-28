---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: explainability, monitoring, explain, explaining, transactions, transaction ID

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# 解释事务
{: #ie-ov}

对于每个部署，您可以查看特定事务的可解释性数据。
{: shortdesc}

## 解释事务
{: #ie-view}

在所选部署磁贴中，选择导航器中的**解释事务**选项卡 (![“解释事务”选项卡](images/insight-transact-tab.png)) 并输入事务标识。

只要将数据发送到模型进行评分，它就会通过设置 `X-Global-Transaction-Id` 字段在 HTTP 头中设置事务标识。此事务标识存储在载荷表中。要针对特定评分查找模型行为的解释，请指定与该评分请求关联的事务标识。请注意，此行为仅适用于 Watson Machine Learning (WML) 事务，不适用于非 WML 事务。
{: note}

### 在 {{site.data.keyword.aios_short}} 中查找事务标识
{: #ie-find}

1.  从部署的时间图表，在图表中滑动标记，然后单击**查看详细信息**链接以[可视化特定小时的数据](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet)。
1.  单击**查看事务**按钮以[查看事务标识列表](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra)。
1.  从列表中复制其中一个事务标识，将其粘贴到**解释事务**页面上的搜索框中，然后按 Enter 键。

    事务标识的列表还可选择仅单击任何事务标识的“操作”列中的**解释**链接，这将在“可解释性”选项卡中打开该事务。
    {: note}

  请参阅以下部分以获取不同类型模型的解释示例。

  ![可解释性事务标识](images/insight-explain-trans-id.png)

## 分类模型示例
{: #ie-class}

此可解释性示例表示用于核准或拒绝保险索赔的二元分类模型。在此情况下，您可以看到对于最终结果 `DENIED` 造成有利或不利影响的因素。

值为 `< 1 year` 的特征 *POLICY AGE* 在决定 DENIED 结果的模型中具有最大影响。导致此结果的其他特征为 *CLAIM FREQUENCY* (`High`) 和 *AGE* (`18`)，而 *CAR VALUE* (`$50,000`) 仅产生轻微影响。

![可解释性二元分类](images/insight-explain-binary.png)

虽然图表有助于显示确定事务结果的最重要因素，但分类模型还可以包含 `Minimum changes for Approved outcome` 和 `Minimum changes for this outcome` 部分中详述的高级解释。

高级解释不适用于回归、图像和非结构化文本模型。
{: note}

`Minimum changes for Approved outcome` 表明如果特征的值更改为此部分中所列的值，那么模型的预测将更改。

同样，`Minimum changes for this outcome` 表明即使特征的值更改为此部分中所列的值，模型的预测也不会更改。

因此，这两个值表明正在为其生成解释的数据点附近的模型行为。

![可解释性二元分类](images/insight-explain-binary2.png)

## 图像模型示例
{: #ie-image}

对于可解释性的图像分类模型示例，您可以查看图像的哪些部分对于预测的结果造成有利影响，哪些部分造成不利影响。在以下示例中，右侧的图像显示对预测具有有利影响的部分，左侧的图像显示对结果具有不利影响的图像部分。

当前，无法为大小超过 1 MB 的图像生成解释。
{: note}

![可解释性图像分类](images/insight-explain-image.png)

## 非结构化文本模型示例
{: #ie-unstruct}

最后，此可解释性示例显示用于评估非结构化文本的分类模型。此解释显示对于模型预测具有有利或不利影响的关键字。我们还会在作为输入馈送到模型的原始文本中显示已识别的关键字的位置。

![可解释性图像分类](images/insight-explain-text.png)
