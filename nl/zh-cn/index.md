---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

keywords: supported frameworks, models, model types, limitations, limits

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
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

# 关于
{: #in-ov}

{{site.data.keyword.aios_full}} 是注入了 AI 的应用程序的企业级环境，为企业提供有关 AI 如何按照业务规模进行构建、使用和实现投资回报的可视性。
{: shortdesc}

<p>&nbsp;</p>

## 实施
{: #in-imp}

以下介绍如何实施 {{site.data.keyword.aios_short}}：

- **配置 {{site.data.keyword.aios_short}}**：通过易于使用的图形环境，[设置有效内容日志记录数据库](/docs/services/ai-openscale?topic=ai-openscale-connect-db)，以及 AI 模型和部署存储所在的 [Watson Machine Learning 实例](/docs/services/ai-openscale?topic=ai-openscale-wml-connect)。

- **使用监视器**：对于每个部署，请配置 {{site.data.keyword.aios_short}} 将如何监视该部署。您可以监视：

    - [公平性](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)
    - [准确性](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor)

- **查看和编辑受监视数据**：通过 {{site.data.keyword.aios_short}} [仪表板](/docs/services/ai-openscale?topic=ai-openscale-io-ov)，可以轻松查看关键洞察并确定部署的问题。每个受监视特征的个别数据点的可视化提供了其他详细信息。

<p>&nbsp;</p>

## 限制

{: #in-lim}

- 当前发行版仅支持一个数据库、一个 Watson Machine Learning 实例和一个 {{site.data.keyword.aios_short}} 实例

- 数据库和 Watson Machine Learning 实例必须部署在同一 {{site.data.keyword.cloud_notm}} 帐户中。

- Lite（免费）套餐具有以下每月限制：

    - 监视两个已部署的模型
    - 解释 20 个事务
    - 50,000 个有效内容记录（累积）
    - 50,000 个反馈记录（累积）

- {{site.data.keyword.aios_short}} 使用 PostgreSQL 或 Db2 数据库来存储模型部署输出和重新训练数据。当前不支持 Lite Db2 套餐。

- 许可证限制每个 {{site.data.keyword.aios_short}} 实例的已部署的模型数不能超过 20。

- 当前，无法为大小超过 1 MB 的图像生成解释。

<p>&nbsp;</p>

## 支持的模型类型
{: #in-mod}

表 1. 模型支持详细信息

| 算法 | **公平性** | **自动除偏** | **解释** | **准确性** |
|:---|:---:|:---:|:---:|:---:|
| **结构化分类** |是| 是<sup>1</sup> |是|是|
| **结构化回归**     |是|否|是|是|
| **文本分类**       |否|否|是|否|
| **图像分类**       |否|否|是|否||
{: caption="模型支持详细信息" caption-side="top"}

<sup>1</sup> 如果模型/框架输出预测概率

<p>&nbsp;</p>

## 支持的机器学习引擎和框架
{: #in-fram}

{{site.data.keyword.aios_short}} 服务支持以下机器学习引擎。每个运行时支持以下框架中创建的模型，如[支持的模型类型](#in-mod)列表中所述。

- [{{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-wml#frmwrks-wml) 
- [Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure#frmwrks-azure)
- [AWS Sagemaker](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-aws-sage#frmwrks-aws-sage)
- [定制](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-custom#frmwrks-custom)


- [SAS AI Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-sas#frmwrks-sas)
{: download}
- [Google Cloud ML Engine](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-google#frmwrks-google)
{: download}
- [SPSS C&DS（仅 ICP）](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-spss#frmwrks-spss)
{: download}

完全支持包含特定框架、问题和数据类型的以下功能：

- 有效内容日志记录	
- 反馈日志记录	
- 性能准确性	
- 运行时偏差检测	
- 可解释性	
- 自动除偏

<p>&nbsp;</p>

## 浏览器支持
{: #in-brw}

{{site.data.keyword.aios_short}} 服务工具需要的浏览器软件级别与 {{site.data.keyword.cloud_notm}} 所需的相同。请参阅 {{site.data.keyword.cloud_notm}} [先决条件](/docs/overview?topic=overview-prereqs-platform#browsers-platform)主题以获取详细信息。

<p>&nbsp;</p>

## ModelOps CLI 工具
{: #in-mop}

通过 [{{site.data.keyword.aios_short}} CLI 模型操作工具 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/IBM-Watson/aiopenscale-modelops-cli){: new_window}，您可以执行与机器学习模型的生命周期管理相关的任务。此工具与 {{site.data.keyword.cloud_notm}} CLI 工具相辅相成，通过[机器学习插件 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/support/knowledgecenter/DSXDOC/analyze-data/ml_dlaas_environment.html){: new_window} 进行了扩充。

<p>&nbsp;</p>

## Python 客户机
{: #in-pyc}

[{{site.data.keyword.aios_short}} Python 客户机 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://ai-openscale-python-client.mybluemix.net/){: new_window} 是允许您直接使用 {{site.data.keyword.cloud_notm}} 上的 {{site.data.keyword.aios_short}} 服务的 Python 库。您可以使用 Python 客户机而不是 {{site.data.keyword.aios_short}} 客户机 UI 来直接配置日志记录数据库，绑定机器学习引擎以及选择并监视部署。有关以此方式使用 Python 客户机的示例，请参阅 [{{site.data.keyword.aios_short}} 样本笔记本 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks)。

<p>&nbsp;</p>

## 后续步骤
{: #in-next}

- 服务[入门](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted)。
- 查看 [API 参考资料 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/ai-openscale){: new_window}。

仍然有疑问？请[联系 IBM ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: new_window}。
