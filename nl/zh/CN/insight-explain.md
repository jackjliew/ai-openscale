---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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
{: shortdesc}

## 解释事务
{: #ie-view}

在所选部署磁贴中，选择导航器中的**解释事务**选项卡 (![“解释事务”选项卡](images/insight-transact-tab.png)) 并输入事务标识。

只要将数据发送到模型进行评分，它就会通过设置 `X-Global-Transaction-Id` 字段在 HTTP 头中设置事务标识。此事务标识存储在载荷表中。要针对特定评分查找模型行为的解释，请指定与该评分请求关联的事务标识。请注意，此行为仅适用于 {{site.data.keyword.pm_full}} 事务，不适用于非 WML 事务。
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

## 图像模型
{: #ie-image}

{{site.data.keyword.aios_short}} 支持图像数据的可解释性。

### 使用图像模型
{: #ie-image-working}

1. 设置环境。
   2. 安装 {{site.data.keyword.aios_short}} 和 {{site.data.keyword.pm_full}} 软件包。
   3. 配置凭证。
   4. 安装创建模型和执行分析所需的库。其中包括以下库：
      - `keras`
      - `tensorflow`
      - `keras_sequential_ascii`
      - `numpy`
      - `pillow`

1. 创建并部署基于图像的模型。
   2. 根据对图像进行分类的方式为这些图像创建文件夹。
       - 在 `data` 主目录中，必须具有 `train` 和 `validation` 子目录。
       - 在每个子目录中，必须具有分类目录。
  2. 将图像大小标准化，然后设置要用于训练和验证的子目录。
  3. 预处理数据以重定比例并检索图像及其类。
  4. 定义并训练模型。
  5. 存储模型。
  6. 部署模型。

7. 通过分配 `APIClient`、预订资产并对模型进行评分来配置 {{site.data.keyword.aios_short}}。
8. 配置可解释性。
   9. 启用可解释性。
   10. 获取事务的可解释性。
   11. 显示所解释的图像。 

### 解释图像模型事务
{: #ie-image-workingviewing}

对于可解释性的图像分类模型示例，您可以查看图像的哪些部分对于预测的结果造成有利影响，哪些部分造成不利影响。在以下示例中，正面窗格中的图像显示对预测具有有利影响的部分，而负面窗格中的图像显示对结果具有不利影响的图像部分。

![可解释性图像分类](images/insight-explain-image.png)

对于 {{site.data.keyword.pm_full}}，所发送的用于有效内容日志记录的图像分类模型的评分输入不能超过 1 MB。要避免超时问题，图像不得超过 125 x 125 像素，并且必须顺序发送，以便在完成第一个图像后请求对第二个图像的解释。
{: note}


### 图像模型示例
{: #ie-image-working-ntbks}

使用以下两个笔记本来查看详细代码样本并开发您自己的 {{site.data.keyword.aios_short}} 部署：

- [有关生成基于图像的模型的解释的教程](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation.ipynb){: external}
- [有关生成基于图像的二元分类器模型的解释的教程](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation_binary.ipynb){: external}


## 非结构化文本模型
{: #ie-unstruct}

{{site.data.keyword.aios_short}} 支持非结构化文本数据的可解释性。

### 使用非结构化文本模型
{: #ie-unstruct-steps}

1. 设置环境。
   2. 安装 {{site.data.keyword.aios_short}} 和 {{site.data.keyword.pm_full}} 软件包。
   3. 配置凭证。
   4. 安装创建模型和执行分析所需的库。其中包括以下库：
      - `pandas`
      - `pyspark`（如果使用的不是 {{site.data.keyword.DSX}}）

1. 创建并部署基于图像的模型。
   2. 将训练数据装入到 pandas 框架中。
   2. 按照数据对模型进行训练。
   3. 发布模型。
   4. 部署模型并对其进行评分。

7. 通过分配 `APIClient`、预订资产并对模型进行评分来配置 {{site.data.keyword.aios_short}}。
8. 配置可解释性。
   9. 启用可解释性。
   10. 获取事务的可解释性。

### 解释非结构化文本事务
{: #ie-unstruct-xplan}

以下可解释性示例显示用于评估非结构化文本的分类模型。此解释显示对于模型预测具有有利或不利影响的关键字。我们还会在作为输入馈送到模型的原始文本中显示已识别的关键字的位置。

![可解释性图像分类](images/insight-explain-text.png)

### 非结构化文本模型示例
{: #ie-unstruct-ntbkssample}

使用以下笔记本来查看详细代码样本并开发您自己的 {{site.data.keyword.aios_short}} 部署：

- [有关生成基于文本的模型的解释的教程](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/text_explanation.ipynb){: external}
