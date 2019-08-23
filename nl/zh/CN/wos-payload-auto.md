---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: machine learning engines, frameworks, Microsoft Azure, Amazone SageMaker, custom ML engine 

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

# 自动执行有效内容日志记录
{: #fmrk-workaround-pyld-lg}

在同一 {{site.data.keyword.Bluemix_notm}} 帐户中供应 {{site.data.keyword.aios_full}} 和 {{site.data.keyword.pm_full}} 时，这两者之间存在自动有效内容日志记录。您还可以通过使用以下案例和选项之一对其他机器学习提供程序或对不在同一帐户中的 {{site.data.keyword.pm_full}} 实例自动执行有效内容日志记录：
{: shortdesc}

### 案例 1：保留评分输入和输出的原始格式（与 {{site.data.keyword.aios_short}} 要求的格式不同）
{: #fmrk-workaround-case1}

如果应用程序使用无法更改的原始有效内容格式，请选择以下选项之一：

- 选项 1：定制机器学习引擎评分端点应同时接受这两种有效内容格式。 

   根据有效内容格式：{{site.data.keyword.aios_short}}（类似于 {{site.data.keyword.pm_full}}）或用户的有效内容格式，返回对应格式的输出。如果格式是用户的格式，请将其转换为 {{site.data.keyword.aios_short}} 格式并作为有效内容记录存储有效内容日志记录表中。如果评分输入格式是 {{site.data.keyword.aios_short}} 格式，请勿存储有效内容（此有效内容来自 {{site.data.keyword.aios_short}} 而不是来自用户）。

   有关更多信息，请参阅[使用两种有效内容格式](#fmrk-workaround-notsuppt)。

- 选项 2：如果出于某些原因无法在单个 REST API 端点中嵌入此类逻辑，那么可以定义两个端点。 

   您的应用程序使用其中一个端点，但是，必须添加有效内容日志记录并将其转换为预期格式。第二个端点由 {{site.data.keyword.aios_short}} 用于进行所需的计算，例如偏差和可解释性。此端点无需进行任何有效内容日志记录。在 {{site.data.keyword.aios_short}} 配置期间，应将第二个端点指向具有兼容格式的端点。

   有关更多信息，请参阅[使用两个端点](#fmrk-workaround-opt2-cs1)。

- 选项 3：将有效内容日志记录模块移至原始端点或下游应用程序。 

   如果应用程序支持此选项，那么只需开发定制机器学习引擎上的一个端点：{{site.data.keyword.aios_short}} 的端点。

### 案例 2：使用 {{site.data.keyword.aios_short}} 所需的有效内容的格式
{: #fmrk-workaround-case2}

在此类情况下，无需进行从用户的格式（评分输入/输出）到 {{site.data.keyword.aios_short}} 所需的格式的任何转换。

由于我们不希望将内部评分请求记录为用户有效内容（由 {{site.data.keyword.aios_short}} 执行计算），因此必须开发两个端点，或者必须为单个端点编写额外的逻辑。

- 选项 1：两个端点。它与案例 1 中的选项 2 几乎相同。唯一的区别是无需进行任何格式转换，因为这些格式已一致。

- 选项 2：单个端点。需要检测评分请求是否来自用户的应用程序。这可以通过在评分有效内容（即元数据）中发送一些额外信息来实现。如果检测到此类元数据，那么应记录有效内容。

## 使用两种有效内容格式
{: #fmrk-workaround-notsuppt}

假设我是使用 XYZ 产品来为模型提供服务。在此阶段，{{site.data.keyword.aios_short}} 不支持 XYZ。

我有许多下游应用程序在 XYZ 上使用我的部署，因此无法更改评分有效内容的格式。但是，我可以修改评分端点逻辑。

### 步骤

1. 开发用于包装 XYZ 部署的定制机器学习引擎。
2. 在定制机器学习引擎上实施评分端点，以同时支持 XYZ 和 {{site.data.keyword.aios_short}} 的有效内容格式。
3. 在定制机器学习引擎上的评分端点中添加逻辑以检测有效内容的格式。
4. 如果有效内容来自下游应用程序，请将其转换为 {{site.data.keyword.aios_short}} 格式并将其记录为 {{site.data.keyword.aios_short}} 中的有效内容记录。
5. 将下游应用程序评分端点切换到所创建的新评分端点。

如果评分端点的 URL 需要保持不变，请使用 URL 重定向（也称为代理）。

## 使用两个端点
{: #fmrk-workaround-opt2-cs1}

如果无法更改有效内容的格式，例如，如果它会导致下游应用程序中断，那么必须使用单独的端点。此方法由以下部分组成：

- 评分端点（采用用户的格式），其中原始评分端点对输入和输出均使用用户定义的格式
- 具有扰动端点（{{site.data.keyword.aios_short}} 格式）和发现端点的定制 ML 引擎。扰动端点对原始评分端点进行包装，并从 {{site.data.keyword.aios_short}} 格式转换为用户的格式，以及从用户的输出转换为 {{site.data.keyword.aios_short}} 输出。这对于 {{site.data.keyword.aios_short}} 进行正确的评分请求并理解输出是必需的。
- 具有有效内容日志记录功能的评分端点包装器。此包装器由下游应用程序使用，而不是由原始评分端点使用。其逻辑已通过有效内容日志记录功能进行扩展。每次执行评分请求时，输入和输出会转换为 {{site.data.keyword.aios_short}} 格式并进行记录。

以下流程图显示定制机器学习引擎解决方案，在此解决方案中，定制机器学习引擎会处理扰动和发现端点，并将其转换为您的格式：

![REST API 端点规范](images/woscustommlworkflow.png)

### 步骤
{: #fmrk-workaround-smple-cd}

1. 在 Microsoft Azure 机器学习服务中，使用笔记本为信用风险模型 (scikit-learn) 部署创建评分端点。有关更多信息，请参阅[此样本笔记本](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/azure/Credit%20model%20with%20Azure%20ML%20Service%20and%20scikit-learn.ipynb)。
2. 创建定制机器学习引擎，并将其作为 Flask 应用程序部署在 Microsoft Azure Cloud 上。创建扰动端点和发现端点。有关更多信息，请参阅[这些部署指示信息](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-azure)。
3. 配置 {{site.data.keyword.aios_short}} 以使用定制机器学习引擎。有关更多信息，请参阅[此样本笔记本](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/azure/OpenScale%20and%20Custom%20ML%20Engine%20configuration.ipynb)。
4. 创建用于在 Microsoft Azure Machine Learning Service 上自动执行有效内容日志记录的评分端点包装器。有关更多信息，请参阅[此样本笔记本](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/azure/Credit%20scoring%20endpoint%20wrapper%20with%20payload%20logging.ipynb)。

请特别注意以下各项：

- 凭证：为使教程更易于理解，{{site.data.keyword.aios_short}} 凭证在代码（评分端点包装器）中进行了硬编码。必须将这些值更新为实际凭证。
- Python SDK 与 REST API：本教程使用 Python SDK 来记录有效内容。您还可以使用 REST API 来执行此操作，但是必须自行生成或刷新令牌。 
- {{site.data.keyword.cloud_notm}} 与 Cloud Pak for Data：如果您使用的是 {{site.data.keyword.wos4d_notm}}，那么凭证采用不同格式，[此处为样本笔记本](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine%20-%20ICP.ipynb)。{{site.data.keyword.aios_short}} 客户机类也不同。它使用 `APIClient4ICP` 客户机类。
- 以单独端点/包的形式进行有效内容日志记录 - 将有效内容日志记录和转换方法抽取到单独的包或端点。通过该方式，如果要在评分端点包装器外部注入批量有效内容，那么可以复用此包/端点。

