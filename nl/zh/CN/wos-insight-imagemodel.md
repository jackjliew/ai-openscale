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

# 解释图像模型
{: #ie-image}

{{site.data.keyword.aios_short}} 支持图像数据的可解释性。
{: shortdesc}

## 使用图像模型
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

## 解释图像模型事务
{: #ie-image-workingviewing}

对于可解释性的图像分类模型示例，您可以查看图像的哪些部分对于预测的结果造成有利影响，哪些部分造成不利影响。在以下示例中，正面窗格中的图像显示对预测具有有利影响的部分，而负面窗格中的图像显示对结果具有不利影响的图像部分。

![显示可解释性图像分类置信度详细信息，其中包含一只狗的图像，该图像另将图片的某些部分突出显示，以说明图像的哪个部分有助于确定该图像是一只狗](images/insight-explain-image.png)

对于 {{site.data.keyword.pm_full}}，为有效内容日志记录发送的图像分类模型的评分输入不能超过 ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling serviceMB。要避免超时问题，图像不得超过 125 x 125 像素，并且必须顺序发送，以便在完成第一个图像后请求对第二个图像的解释。
{: note}


## 图像模型示例
{: #ie-image-working-ntbks}

使用以下两个笔记本来查看详细代码样本并开发您自己的 {{site.data.keyword.aios_short}} 部署：

- [有关生成基于图像的模型的解释的教程](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation.ipynb){: external}
- [有关生成基于图像的二元分类器模型的解释的教程](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation_binary.ipynb){: external}

