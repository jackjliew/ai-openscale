---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

- **配置 {{site.data.keyword.aios_short}}**：通过易于使用的图形环境，[设置载荷日志记录数据库](/docs/services/ai-openscale?topic=ai-openscale-connect-db)，以及 AI 模型和部署存储所在的 [Watson Machine Learning 实例](/docs/services/ai-openscale?topic=ai-openscale-wml-connect)。

- **使用监视器**：对于每个部署，请配置 {{site.data.keyword.aios_short}} 将如何监视该部署。您可以监视：

    - [公平性](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)
    - [准确性](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor)
    - [性能](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics#anlz_metrics_performance)

- **查看和编辑受监视数据**：通过 {{site.data.keyword.aios_short}} [仪表板](/docs/services/ai-openscale?topic=ai-openscale-io-ov)，可以轻松查看关键洞察并确定部署的问题。每个受监视特征的个别数据点的可视化提供了其他详细信息。

<p>&nbsp;</p>

## 限制

{: #in-lim}

- 当前发行版仅支持一个数据库、一个 {{site.data.keyword.pm_full}} 实例和一个 {{site.data.keyword.aios_short}} 实例

- 数据库和 {{site.data.keyword.pm_full}} 实例必须部署在同一 {{site.data.keyword.cloud_notm}} 帐户中。

- Lite（免费）套餐具有以下每月限制：

    - 监视两个已部署的模型
    - 解释 20 个事务
    - 50,000 个载荷记录（累积）
    - 50,000 个反馈记录（累积）

- {{site.data.keyword.aios_short}} 使用 PostgreSQL 或 Db2 数据库来存储模型相关数据（反馈数据或评分有效内容）和计算的度量。当前不支持 Lite Db2 套餐。

- 许可证限制每个 {{site.data.keyword.aios_short}} 实例的已部署的模型数不能超过 20。

- 对于 {{site.data.keyword.pm_full}}，通过 Machine Learning Gateway 发送的扰动图像的有效内容不能超过 1 MB。要避免超时问题，图像不得超过 125 x 125 像素，并且必须顺序发送，以便在完成第一个图像后请求对第二个图像的解释。


<p>&nbsp;</p>

## 已知问题
{: #rn-12ki}

- **Microsoft Azure**

    - 在两种类型的 Azure Machine Learning Web Service 中，{{site.data.keyword.aios_short}} 仅支持 `New` 类型。不支持 `Classic` 类型。

    - __*必须使用缺省输入名称*__：在 Azure Web Service 中，缺省输入名称为 `"input1"`。当前，{{site.data.keyword.aios_short}} 必需此字段，如果缺失，那么 {{site.data.keyword.aios_short}} 将无法正常运作。

      如果 Azure Web Service 不使用缺省名称，请将输入字段名称更改为 `"input1"`，然后代码将正常运作。

- **AWS SageMaker**

    - __*不支持 BlazingText 算法*__：AWS SageMaker BlazingText 算法输入载荷格式在 {{site.data.keyword.aios_short}} 的当前发行版中不受支持。

- **定制 ML 服务实例**

    - [Python 模块](/docs/services/ai-openscale?topic=ai-openscale-as-module)当前不具有适用于定制服务实例的可解释性。这是因为定制服务实例需要在响应数据中进行数字预测，而模块脚本未随附该数据。

<p>&nbsp;</p>

## 支持的机器学习引擎和框架
{: #in-fram}

{{site.data.keyword.aios_short}} 服务支持以下机器学习引擎。每个运行时支持在以下框架中创建的模型：

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

- 载荷日志记录	
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

仍然有疑问？ 

- [新增内容](/docs/services/ai-openscale?topic=ai-openscale-rn-relnotes)
- 请[联系 IBM ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: new_window}。
