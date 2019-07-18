---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: release notes, what's new 

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

# 新增内容
{: #rn-relnotes}

本文档概述 {{site.data.keyword.aios_full_notm}} 的新功能。
{: shortdesc}

## 2019 年 7 月 2 日
{: #rn-2jul2019}

为 {{site.data.keyword.aios_short}} 提供了以下新功能和更改。

- __*漂移检测*__：![beta 标记](images/beta.png)

  {{site.data.keyword.aios_short}} 现在支持漂移检测。

   有关更多信息，请参阅 [漂移检测](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-ovr)。

- __*Microsoft Azure ML Service 支持*__：{{site.data.keyword.aios_short}} 现在支持 Microsoft Azure ML Service，它提供用于将 Azure ML Service AI 模型与 {{site.data.keyword.aios_short}} 的公平性、准确性和可解释性集成的方法。

   有关更多信息，请参阅 [Microsoft Azure ML Service 框架](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-frmwrks-azure-service)。

- __*改进工作流程*__：{{site.data.keyword.aios_short}} 致力于改进工作流程，以便您可以通过减少单击数和提高可解释性来加速完成工作。通过导航面板，您可以查看所处的位置并轻松地在配置任务之间前后跳跃。

   有关更多信息，请参阅[为部署准备监视器](/docs/services/ai-openscale?topic=ai-openscale-mo-config)。

- __*多个机器学习提供程序*__：为什么仅局限于一个机器学习提供程序或引擎？通过最新版本的 {{site.data.keyword.aios_short}}，可以添加多个提供程序，以便能够利用其特有功能或提供与旧应用程序的连续性。

   有关更多信息，请参阅[支持多个机器学习引擎](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-multmleng)。

- __*更多现成可用的度量*__：通过此版本的 {{site.data.keyword.aios_short}}，有许多新的公平性、质量、行为、性能和分析度量。我们将需要增大范围！

   有关更多信息，请参阅[质量度量概述](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics)，然后开始四处单击以访问其他内容：[公平性](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_fairness)、[性能](/docs/services/ai-openscale?topic=ai-openscale-performance_mets_through)、[分析](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_payload)和[行为](/docs/services/ai-openscale?topic=ai-openscale-behavior-ovr)。

- __*迅速处理偏差*__：通过使用建议公平性属性和自动值进行偏差配置，可以轻松查看 {{site.data.keyword.aios_short}} 在已部署模型中检测到公平性阈值可能违例的位置。您可以选择接受建议功能以监视和更改这些值。

   有关更多信息，请参阅[公平性度量概述](/docs/services/ai-openscale?topic=ai-openscale-anlz_metrics_fairness)。

## 2019 年 6 月 11 日
{: #rn-11June2019}

提供了以下新功能和对服务的更改。

- __*更新的仪表板功能*__：{{site.data.keyword.aios_short}} 仪表板已经过多次修订。此新版本包含以下改进：

    - 通过新的帮助面板，可更轻松地查找资源，例如 StackOverflow、IBM 支持， 
    - 并且仪表板支持全球化
    - 易用性增强功能

## 2019 年 6 月 7 日
{: #rn-7June2019}

提供了以下新功能和对服务的更改。

- __*增强的命令行界面*__：命令行界面 ibm-ai-openscale-cli 已更新，现已发行版本 0.2.148。此新版本包含以下改进：

    - 更新了质量度量历史记录，以包含 OpenScale 支持的新质量度量的完整范围
    - 支持在使用 IBM Db2 时直接指定 SSL 证书
    - 支持新的 ibm-ai-openscale 2.1.8 Python SDK
    - 其他错误修订和稳定性改进

   通过运行 `pip install -U ibm-ai-openscale-cli` 命令从 PyPI 进行安装，并通过运行   `ibm-ai-openscale-cli --help` 命令获取用法帮助。有关更多信息，请参阅 [PyPI 项目页面](https://pypi.org/project/ibm-ai-openscale-cli)。

## 2019 年 5 月 29 日
{: #rn-29May2019}

提供了以下新功能和对服务的更改。

- __*偏差可视化增强功能*__：![beta 标记](images/beta.png) 偏差可视化包含以下视图： 

    - 有效内容 + 扰动量：包括在所选小时内接收到的评分请求以及前几个小时的其他记录（如果未满足评估所需的最小记录数）。包含其他扰动/合成的记录，用于在受监视功能部件的值发生更改时测试模型的响应。
    - 有效内容：模型在所选小时内接收到的实际评分请求。
    - 训练：用于训练模型的训练数据记录。
    - 除偏：处理运行时数据和扰动数据后除偏算法的输出。

   有关更多信息，请参阅[偏差可视化](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-monitor-bias-viz)。

- __*已除偏输出的准确性计算*__：准确性计算包括已除偏输出。可以将已除偏模型的准确性与生产模型的准确性进行比较

   有关更多信息，请参阅[准确性](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-debias-view)。

- __*支持多个机器学习引擎*__：{{site.data.keyword.aios_short}} 在单个实例中支持多个机器学习引擎，前提是通过 [Python SDK](http://ai-openscale-python-client.mybluemix.net/?cm_mc_uid=70732728440115575086192&cm_mc_sid_50200000=62539451560175957820) 来执行供应。

   有关更多信息，请参阅[支持多个机器学习引擎](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-multmleng)。

- __*国际化支持*__：{{site.data.keyword.aios_short}} 支持本地化版本并包含受支持语言形式的处理数据。{{site.data.keyword.aios_short}} 用户界面、文档和错误消息当前翻译为以下语言： 
    - 德语
    - 法语
    - 意大利语
    - 西班牙语
    - 巴西葡萄牙语
    - 日语
    - 简体中文
    - 繁体中文
    - 朝鲜语

   有关更多信息（包括限制），请参阅 [{{site.data.keyword.aios_short}} 的受支持语言](/docs/services/ai-openscale?topic=ai-openscale-sl-langs)。

- __*{{site.data.keyword.pm_full}} 框架增强功能*__：现在，{{site.data.keyword.aios_short}} 在 {{site.data.keyword.pm_full}} 引擎上支持 scikit-learn 和 XGBoost 框架。

   有关更多信息，请参阅 [{{site.data.keyword.pm_full}} 框架](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-wml)。

## 2019 年 4 月 25 日
{: #rn-25April2019}

提供了以下新功能和对服务的更改。

除了易用性改进和安全性更新外，我们的开发者还一直在忙着增加新功能。在前几周内已经增加或增强的 {{site.data.keyword.aios_short}} 功能包括：

- __*自动化设置导览*__：一种全新的导览方法，用于设置 {{site.data.keyword.aios_short}} 环境。使用[自动化设置](/docs/services/ai-openscale?topic=ai-openscale-wos-fast-start)可供应服务以及下载和配置模型。当您具有 {{site.data.keyword.aios_short}} 的新实例时，您会注意到此选项。
- __*切换到 beta 版本*__：![beta 标记](images/beta.png)一个新的切换开关**浏览新 beta 版本**让您能够使用我们的 beta 版本环境，在此环境中，您可以了解所有最新特性和新功能。不喜欢您看到的东西？只需要单击**返回到原始版本**便可以切换回来。您的配置和监视器不受影响。当前 beta 程序包含以下功能：
    - __*混淆矩阵*__：[混淆矩阵显示](/docs/services/ai-openscale?topic=ai-openscale-it-conf-mtx)误报和漏报。单击单元格可查看反馈记录的子集。

## 2019 年 4 月 10 日
{: #rn-10April2019}

- __*Express Path 工具现在支持客户模型*__：自动执行 {{site.data.keyword.aios_short}} 的上线程序。

   有关更多信息，请参阅 [ibm-ai-openscale-cli](https://pypi.org/project/ibm-ai-openscale-cli/)。


## 2019 年 3 月 5 日
{: #rn-5March2019}

提供了以下新功能和对服务的更改。

自前发行版以来添加或增强的 {{site.data.keyword.aios_short}} 功能包括：

- __*新信用风险模型*__：所有评分引擎都支持新的信用风险模型示例/教程。有关更多信息，请参阅[入门](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted#gettingstarted)和[其他资源](/docs/services/ai-openscale?topic=ai-openscale-arsc-ov#arsc-ov)主题。

- __*计算偏差*__：您可以在生产模型和 {{site.data.keyword.aios_short}} 所创建的已除偏模型之间进行切换。请参阅[生产模型和已除偏模型](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-prdb)以及[了解除偏的工作方式](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-debias)以获取更多信息。

## 2019 年 2 月 22 日
{: #rn-22February2019}

提供了以下新功能和对服务的更改。

自前发行版以来添加或增强的 {{site.data.keyword.aios_short}} 功能包括：

- __*UI 更新*__：您可以导入 JSON 文件以在创建预订期间以编程方式配置所有监视器和功能。您还可以导出配置文件。请参阅[使用 JSON 文件配置部署预订](/docs/services/ai-openscale?topic=ai-openscale-cf-ov)主题以获取更多信息。

## 2019 年 2 月 7 日
{: #rn-7February2019}

提供了以下新功能和对服务的更改。

自前发行版以来添加或增强的 {{site.data.keyword.aios_short}} 功能包括：

- __*UI 更新*__：已对 {{site.data.keyword.aios_short}} 用户界面进行多项改进，包括[按需检查公平性和准确性](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdep)的方式，以及能够从[公平性详细信息图表](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra)中查看事务列表。

- __*可解释性增强功能*__：现在，所有数字在相关肯定 (PP) 值和相关否定 (PN) 值中都具有相同的精度/小数位。

- __*Db2 SSL 支持*__：{{site.data.keyword.aios_short}} 支持通过 Db2 凭证传递自签名证书（Base-64 编码）。

- __*{{site.data.keyword.Bluemix}} 数据库支持*__：{{site.data.keyword.aios_short}} 现在支持 Databases for PostgreSQL（除 Compose for PostgreSQL 和 Db2 以外）

## 2018 年 12 月 14 日
{: #rn-14December2018}

提供了服务的下列新功能、更改和已知问题。

自 Beta 发行版以来添加或增强的 {{site.data.keyword.aios_short}} 功能包括：

- __*一般可用性*__：作为 {{site.data.keyword.Bluemix}} Standard（付费）套餐的 {{site.data.keyword.aios_full_notm}} 的一般可用性 (GA) 发行版。

- __*{{site.data.keyword.icp4dfull_notm}} V1.2*__：如果使用的是 {{site.data.keyword.wos4d_full}} V1.2，请参阅此处的文档，包括安装指示信息：[安装核对表](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-inst-install-icp#install)

- __*对模型类型的支持*__：除 {{site.data.keyword.pm_full}} 中的 AI 模型部署以外，{{site.data.keyword.aios_short}} 还支持在 Microsoft Azure、Amazon SageMaker 和定制环境中部署模型。请参阅[支持的模型类型](/docs/services/ai-openscale?topic=ai-openscale-in-ov)以获取更多信息。

- __*免费“lite”数据库*__：免费“lite”受管数据库提供开始使用 {{site.data.keyword.aios_short}} 所需的所有内容。请参阅 [{{site.data.keyword.aios_short}} 定价计划](https://{DomainName}/catalog/services/watson-openscale){: external}以获取详细信息。

- __*偏差监视*__：支持类型为 `float` 和 `double` 的受保护属性，以及对线性回归模型的偏差检测。并且，{{site.data.keyword.aios_short}} 可以自动为您对 AI 模型进行除偏。请参阅[了解公平性](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)以获取更多信息。

- __*可解释性*__：支持回归模型、Python 函数和补充性对比解释。请参阅[监视可解释性](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)以获取更多信息。

- __*数据存储*__：在不依靠 {{site.data.keyword.pm_full}} 的情况下进行质量监视，并且能够使用您自己的数据库，无论是 Db2、Postgres 还是 Db2 on Cloud 都如此。

- __*增强的 UI*__：{{site.data.keyword.aios_short}} UI 已改进为包含运行时直方图分布，其中可在训练数据、模型标识与版本控制以及直方图中的事务标识表之间进行切换。请参阅[可视化特定小时的数据](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet)以获取更多信息。

- __*备用教程设置选项*__：要自动供应和配置必需的 {{site.data.keyword.Bluemix}} 服务，以及要查看 IBM {{site.data.keyword.aios_full}} 应用程序（包括样本数据），可以安装并运行 Python 模块。请参阅[安装 Python 模块以设置 {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-as-module)

## 2018 年 9 月 17 日
{: #rn-17September2018}

- **Beta 预览发行版** - 欢迎使用 {{site.data.keyword.aios_full_notm}} 的 Beta 预览发行版。

<p>&nbsp;</p>

## 后续步骤
{: #relnotes-in-next}

仍然有疑问？

- [限制
](/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-lim)
- [已知问题](/docs/services/ai-openscale?topic=ai-openscale-in-ov#rn-12ki)
