---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits

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

# {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}}
{: #frmwrks-wml}

您可以使用 {{site.data.keyword.pm_full}} 在 {{site.data.keyword.aios_full}} 中执行有效内容日志记录、反馈日志记录以及度量性能准确性、运行时偏差检测、可解释性和自动除偏功能。

{{site.data.keyword.aios_full}} 完全支持以下 {{site.data.keyword.pm_full}} 框架：
{: shortdesc}

表 1. 框架支持详细信息

| 框架 | 问题类型 | 数据类型 |
|:---|:---:|:---:|
| Apache Spark MLlib |分类| 结构化 |
| Apache Spark MLLib | 回归 | 结构化 |
| Keras with TensorFlow<sup>1</sup><sup>&</sup><sup>2</sup> |分类| 非结构化（图像，文本）|
| Keras with TensorFlow<sup>1</sup><sup>&</sup><sup>2</sup> | 回归 | 非结构化（图像，文本）|
| Python 函数 |分类| 结构化 |
| Python 函数 | 回归 | 结构化 |
| scikit-learn |分类| 结构化 |
| scikit-learn | 回归 | 结构化 |
| XGBoost |分类| 结构化 |
| XGBoost | 回归 | 结构化 |
{: caption="框架支持详细信息" caption-side="top"}

<sup>1</sup>Keras 支持不包括对公平性的支持。
{: note}

<sup>2</sup>如果模型/框架输出预测概率，那么支持可解释性。
{: note}

## 指定 {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}} 服务实例
{: #wml-connect}

您在 {{site.data.keyword.aios_short}} 工具中的第一步是指定 {{site.data.keyword.pm_full}} 实例。{{site.data.keyword.pm_short}} 实例是存储 AI 模型和部署的位置。
{: shortdesc}

### 先决条件
{: #wml-prereq}

您应该已在 {{site.data.keyword.aios_short}} 服务实例所在的 {{site.data.keyword.Bluemix_notm}} 帐户中供应 {{site.data.keyword.pm_full}} 实例。如果您已在其他某个帐户中供应 {{site.data.keyword.pm_full}} 实例，那么将无法使用 {{site.data.keyword.aios_short}} 通过自动有效内容日志记录来配置该实例。

### 连接 {{site.data.keyword.pm_short}} 服务实例
{: #wml-config}

{{site.data.keyword.aios_short}} 连接到 {{site.data.keyword.pm_full}} 实例中的 AI 模型和部署。

1.  从导航窗格的**配置**选项卡中，单击**机器学习提供程序**。

    ![显示“选择机器学习服务提供程序”屏幕，其中包含受支持的机器学习引擎的磁贴](images/wos-machine-learning-providers-selection.png)

2.  单击**添加机器学习提供程序**按钮，然后单击 {{site.data.keyword.pm_full}} 磁贴。{{site.data.keyword.aios_short}} 检查 {{site.data.keyword.Bluemix_notm}} 帐户以查找任何现有 {{site.data.keyword.pm_full}} 实例。 
3. 从 **Watson Machine Learning 服务**下拉菜单中选择实例。

    ![选择 {{site.data.keyword.pm_short}} 服务](images/gs-set-wml.png)

4.  （可选）您还可以**选择其他位置**，以在 {{site.data.keyword.Bluemix_notm}} 帐户外指定 Machine Learning 位置。以有效的 JSON 形式提供位置的凭证：

    ![设置 {{site.data.keyword.pm_short}} 实例](images/gs-get-wml.png)

    单击**保存**。

1.  {{site.data.keyword.aios_short}} 列出已部署模型；选择要监视的模型，然后单击**配置**。

## 后续步骤
{: #wml-next}

{{site.data.keyword.aios_short}} 现在可供您用于[配置监视器](/docs/services/ai-openscale?topic=ai-openscale-mo-config)。
