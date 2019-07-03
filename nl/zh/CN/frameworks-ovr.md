---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

# 受支持的机器学习引擎、框架和模型
{: #in-fram}

{{site.data.keyword.aios_short}} 服务支持以下机器学习引擎。每个运行时支持在以下框架中创建的模型：

- [{{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-wml#frmwrks-wml) 
- [Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure#frmwrks-azure)
- [AWS SageMaker](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-aws-sage#frmwrks-aws-sage)
- [定制](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-custom#frmwrks-custom)
- [SPSS C&DS](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-spss#frmwrks-spss)（仅在 {{site.data.keyword.wos4d_full}} 中可用）

- [SAS AI Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-sas#frmwrks-sas)
{: download}
- [Google Cloud ML Engine](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-google#frmwrks-google)
{: download}

完全支持包含特定框架、问题和数据类型的以下功能：

- 载荷日志记录	
- 反馈日志记录	
- 性能准确性	
- 运行时偏差检测	
- 可解释性	
- 自动除偏

<p>&nbsp;</p>


## 支持的模型类型
{: #abt-models}

表 1. 模型支持详细信息

| 算法 | **公平性** | **自动除偏** | **解释** | **准确性** |
|:---|:---:|:---:|:---:|:---:|
| **结构化分类** |是| 是<sup>1</sup> | 是<sup>1</sup> |是|
| **结构化回归**     |是| 即将推出 |是|是|
| **文本分类**       | 否 - 活动研究主题 | 否 - 活动研究主题 | 是<sup>1</sup> |否|
| **图像分类**       | 否 - 活动研究主题 | 否 - 活动研究主题 | 是<sup>1</sup> |否||
{: caption="模型支持详细信息" caption-side="top"}

<sup>1</sup> 如果模型/框架输出预测概率

<p>&nbsp;</p>

## 浏览器支持
{: #in-brw}

{{site.data.keyword.aios_short}} 服务工具需要的浏览器软件级别与 {{site.data.keyword.cloud_notm}} 所需的相同。请参阅 {{site.data.keyword.cloud_notm}} [先决条件](/docs/overview?topic=overview-prereqs-platform#browsers-platform)主题以获取详细信息。

<p>&nbsp;</p>

## ModelOps CLI 工具
{: #in-mop}

通过 [{{site.data.keyword.aios_short}} CLI 模型操作工具](https://github.com/IBM-Watson/aiopenscale-modelops-cli){: external}，您可以执行与机器学习模型的生命周期管理相关的任务。此工具与 {{site.data.keyword.cloud_notm}} CLI 工具相辅相成，通过[机器学习插件](https://www.ibm.com/support/knowledgecenter/DSXDOC/analyze-data/ml_dlaas_environment.html){: external}进行了扩充。

<p>&nbsp;</p>

## Python 客户机
{: #in-pyc}

[{{site.data.keyword.aios_short}} Python 客户机](http://ai-openscale-python-client.mybluemix.net/){: external}是一个 Python 库，允许您直接使用 {{site.data.keyword.cloud_notm}} 上的 {{site.data.keyword.aios_short}} 服务。您可以使用 Python 客户机而不是 {{site.data.keyword.aios_short}} 客户机 UI 来直接配置日志记录数据库，绑定机器学习引擎以及选择并监视部署。有关以此方式使用 Python 客户机的示例，请参阅 [{{site.data.keyword.aios_short}} 样本笔记本](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks)。

<p>&nbsp;</p>

## 后续步骤
{: #in-next}

- 服务[入门](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted)。
- 查看 [API 参考资料](https://{DomainName}/apidocs/ai-openscale){: external}。

仍然有疑问？ 

- [新增内容](/docs/services/ai-openscale?topic=ai-openscale-rn-relnotes)
- [联系 IBM](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: external}。
