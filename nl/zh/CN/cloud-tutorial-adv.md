---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: tutorial, Jupyter notebooks, Watson Studio projects, projects, models, deploy, 

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

# Python SDK 教程（高级）
{: #crt-ov}

在本教程中，您将学习执行以下任务：

- 运行 Python 笔记本以创建、训练和部署机器学习模型。
- 创建数据集市，配置性能、准确性和公平性监视器，以及创建要监视的数据。
- 在 {{site.data.keyword.aios_short}}“洞察”选项卡中查看结果。


## Python 客户机
{: #in-pyc}

[{{site.data.keyword.aios_short}} Python 客户机](http://ai-openscale-python-client.mybluemix.net/){: external}是一个 Python 库，允许您直接使用 {{site.data.keyword.cloud_notm}} 上的 {{site.data.keyword.aios_short}} 服务。您可以使用 Python 客户机而不是 {{site.data.keyword.aios_short}} 客户机 UI 来直接配置日志记录数据库，绑定机器学习引擎以及选择并监视部署。有关以此方式使用 Python 客户机的示例，请参阅 [{{site.data.keyword.aios_short}} 样本笔记本](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks){: external}。

## 场景
{: #crt-scenario}

传统贷款人面临着将其金融服务的数字产品服务组合扩展到更大且更多样化的受众的压力，这需要采取新的方法进行信用风险建模。其数据科学团队目前依靠非常适合中等数据集的标准建模方法（例如决策树和逻辑回归），并且做出可以轻松解释的建议。这满足了信贷决策必须透明且可解释的法规需求。

为了向更广泛和风险更高的群体提供信贷，申请人的信用记录必须从传统信贷（例如抵押贷款和汽车贷款）扩展至替代信贷来源（例如公用事业和手机套餐付费记录，以及教育程度和职位）。这些新数据源带来了希望，但也通过增加意外关联的可能性产生风险，这些关联会基于申请人的年龄、性别或其他个人特质造成偏差。

最适合这些多样化数据集的数据科学方法（例如梯度提升树和神经网络）可以生成高度精确的风险模型，但是存在相应的代价。此类“黑匣”模型生成的是不透明的预测，这些预测必须以某种方式变为透明，以确保获得监管批准，例如通用数据保护条例 (GDPR) 第 22 条，或由消费者金融保护局管理的联邦公平信用报告法案 (FCRA)。

本教程中提供的信用风险模型使用训练数据集，其中包含有关每个贷款申请人的 20 个属性。其中两个属性（年龄和性别）可以测试有无偏差。对于本教程，重点将在于针对性别和年龄的偏差。有关训练数据的更多信息，请参阅 [ 为什么 {{site.data.keyword.aios_short}} 需要访问我的培训数据？](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

{{site.data.keyword.aios_short}} 将监视已部署模型中一个组（参考组）相对于另一个组（受监视组）获取有利结果（“无风险”）的倾向。在本教程中，性别的受监视组为 `female`，而年龄的受监视组为 `18 to 25`。

## 先决条件
{: #crt-prereqs}

本教程使用 Jupyter 笔记本，该笔记本应使用“Python 3.5 with Spark”运行时环境在 Watson Studio 项目中运行。它需要以下 {{site.data.keyword.cloud_notm}} 服务的服务凭证：

- Cloud Object Storage（用于存储 {{site.data.keyword.DSX}} 项目）
- {{site.data.keyword.aios_short}}
- {{site.data.keyword.pm_full}}
- （可选）Databases for PostgreSQL 或 Db2 Warehouse

Jupyter 笔记本将训练、创建和部署“德国信用风险”模型，配置 {{site.data.keyword.aios_short}} 以监视该部署，并提供七天的历史记录和度量值以供在 {{site.data.keyword.aios_short}}“洞察”仪表板中进行查看。您还可以选择配置模型以使用 Watson Studio 和 Spark 进行持续学习。

## 简介
{: #crt-intro}

在本教程中，您将执行以下任务：

- [供应 {{site.data.keyword.cloud_notm}} 机器学习和存储服务](/docs/services/ai-openscale?topic=ai-openscale-crt-ov#crt-services)。
- [设置 Watson Studio 项目，并运行 Python 笔记本以创建、训练和部署机器学习模型](/docs/services/ai-openscale?topic=ai-openscale-crt-ov#crt-set-wstudio)。
- [供应 {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-crt-ov#crt-wos-adv)。
- [运行 Python 笔记本以创建数据集市，配置性能、准确性和公平性监视器，以及创建要监视的数据](/docs/services/ai-openscale?topic=ai-openscale-crt-ov#crt-edit-notebook)。
- [在 {{site.data.keyword.aios_short}}“洞察”选项卡中查看结果](/docs/services/ai-openscale?topic=ai-openscale-crt-ov#crt-view-results)。

## 供应 {{site.data.keyword.cloud_notm}} 服务
{: #crt-services}

使用 {{site.data.keyword.ibmid}} 登录到 [{{site.data.keyword.cloud_notm}} 帐户](https://{DomainName}){: external}。供应服务时（尤其在使用 Db2 Warehouse 的情况下），请验证所选组织和空间是否对于所有服务都相同。

### 创建 {{site.data.keyword.DSX}} 帐户
{: #crt-wstudio}

- [创建 {{site.data.keyword.DSX}} 实例](https://{DomainName}/catalog/services/watson-studio){: external}（如果您还没有与帐户关联的实例）：

  ![显示 Watson Studio 磁贴](images/watson_studio.png)

- 指定服务的名称，选择 Lite（免费）套餐，然后单击**创建**按钮。

### 供应 {{site.data.keyword.cos_full_notm}} 服务
{: #crt-cos}

- [供应 {{site.data.keyword.cos_short}} 服务](https://{DomainName}/catalog/services/cloud-object-storage){: external}（如果您还没有与帐户关联的服务）：

  ![显示 Object Storage 磁贴](images/object_storage.png)

- 指定服务的名称，选择 Lite（免费）套餐，然后单击**创建**按钮。

### 供应 {{site.data.keyword.pm_full}} 服务
{: #crt-wml}

- [供应 {{site.data.keyword.pm_short}} 实例](https://{DomainName}/catalog/services/machine-learning){: external}（如果您还没有与帐户关联的实例）：

  ![显示 Machine Learning 磁贴](images/machine_learning.png)

- 指定服务的名称，选择 Lite（免费）套餐，然后单击**创建**按钮。

### 供应 {{site.data.keyword.aios_full}} 服务
{: #crt-wos-adv}

如果您尚未供应，请确保供应 {{site.data.keyword.aios_full}}。 

- [供应 {{site.data.keyword.aios_short}} 实例](https://{DomainName}/catalog/services/watson-openscale){: external}（如果您还没有与帐户关联的实例）：

  ![显示 {{site.data.keyword.aios_short}} 磁贴](images/wos-cloud-tile.png)

1. 单击**目录** > **AI** > **{{site.data.keyword.aios_short}}**。
2. 指定服务的名称，选择套餐，然后单击**创建**按钮。
3. 要启动 {{site.data.keyword.aios_short}}，请单击**入门**按钮。

### （可选）供应 Databases for PostgreSQL 或 Db2 Warehouse 服务
{: #crt-db2}

如果您具有付费的 {{site.data.keyword.cloud_notm}} 帐户，那么可以供应 `Databases for PostgreSQL` 或 `Db2 Warehouse` 服务来充分利用与 {{site.data.keyword.DSX}} 和持续学习服务的集成。如果选择不供应付费服务，那么可以将免费内部 PostgreSQL 存储与 {{site.data.keyword.aios_short}} 配合使用，但是将无法为模型配置持续学习。

- [供应 Databases for PostgreSQL 服务](https://{DomainName}/catalog/services/databases-for-postgresql){: external}或 [Db2 Warehouse 服务](https://{DomainName}/catalog/services/db2-warehouse){: external}（如果您还没有与帐户关联的服务）：

  ![显示 DB for Postgres 磁贴](images/dbpostgres.png)

  ![显示 Db2 Warehouse 磁贴](images/db2_warehouse.png)

- 指定服务的名称，选择 Standard 套餐 (Databases for PostgreSQL) 或 Entry 套餐 (Db2 Warehouse)，然后单击**创建**按钮。

## 设置 {{site.data.keyword.DSX}} 项目
{: #crt-set-wstudio}

- 登录到 [{{site.data.keyword.DSX}} 帐户](https://dataplatform.ibm.com/){: external}。单击 {{site.data.keyword.avatar}} 并验证您使用的帐户是否与用于创建 {{site.data.keyword.cloud_notm}} 服务的帐户相同：

  ![相同帐户](images/same_account.png)

- 在 {{site.data.keyword.DSX}} 中，首先创建一个新项目。 选择“创建项目”：

  ![Watson Studio 创建项目](images/studio_create_proj.png)

- 选择**标准**磁贴，以创建项目：

  ![显示 Watson Studio“选择标准项目”磁贴](images/studio_create_standard.png)

- 指定项目的名称和描述，确保在**存储**下拉菜单中选择所创建的 Cloud Object Storage 服务，然后单击**创建**。

## 创建和部署 {{site.data.keyword.pm_short}} 模型
{: #crt-make-model}

### 将 `Working with Watson Machine Learning` 笔记本添加到 {{site.data.keyword.DSX}} 项目
{: #crt-add-notebook}

- 访问以下文件。如果您具有 GitHub 帐户，那么可登录以克隆和下载文件。否则，可以通过单击**原始**按钮来查看原始版本，并将文件的文本复制到扩展名为 .ipynb 的新文件中。

    - [使用 Watson Machine Learning](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb){: external}

- 从 {{site.data.keyword.DSX}} 项目中的**资产**选项卡单击**添加到项目**按钮，然后从下拉菜单中选择**笔记本**：

  ![显示“选择资产类型”，其中笔记本磁贴突出显示](images/add_notebook.png)

- 选择**从文件**：

  ![“新建笔记本”表单](images/new_notebook_name.png)

- 然后，单击**选择文件**按钮，并选择所下载的“german_credit_lab.ipynb”笔记本文件：

  ![“新建笔记本”表单](images/new_notebook_name2a.png)

- 在**选择运行时**部分中，选择最新的 Python with Spark 选项：

- 单击**创建笔记本**。

### 编辑并运行 `Working with Watson Machine Learning` 笔记本
{: #crt-edit-notebook}

`Working with Watson Machine Learning` 笔记本包含将运行的 Python 代码中每个步骤的详细指示信息。在完成笔记本工作时，请花费一些时间来了解每个命令所执行的操作。
{: tip}

- 从 Watson Studio 项目的**资产**选项卡单击 `Working with Watson Machine Learning` 笔记本旁边的**编辑**图标以编辑该笔记本。

- 在“供应服务并配置凭证”部分中，进行以下更改：

    - 遵循笔记本中的指示信息来创建、复制和粘贴 {{site.data.keyword.cloud_notm}} API 密钥。

    - 将 {{site.data.keyword.pm_full}} 服务凭证替换为先前创建的凭证。

    - 将数据库凭证替换为您为 Databases for PostgreSQL 创建的凭证。

    - 如果先前将 {{site.data.keyword.aios_short}} 配置为使用免费内部 PostgreSQL 数据库作为数据集市，那么可以切换到使用 Databases for PostgreSQL 服务的新数据集市。要删除旧 PostgreSQL 配置并创建新配置，请将 KEEP_MY_INTERNAL_POSTGRES 变量设置为 `False`。

        该笔记本将移除现有内部 PostgreSQL 数据集市，并使用所提供的 DB 凭证创建新数据集市。**不会发生任何数据迁移**。
        {: important}

- 一旦供应服务并输入凭证，笔记本即可运行。单击**内核**菜单项，然后从菜单中选择**重新启动并清除输出**：

  ![重新启动并清除](images/restart_and_clear.png)

- 现在，按顺序运行笔记本的每个步骤。请按照所述注意每个步骤中发生的情况。逐步完成所有步骤，包括“用于帮助调试的其他数据”部分中的步骤。

最终结果是已创建、训练 **Spark 德国风险部署**模型并将其部署到 {{site.data.keyword.aios_short}} 服务实例。{{site.data.keyword.aios_short}} 将配置为检查模型是否存在针对性别（在本例中为 Female）或年龄（在本例中为 18-25 岁）的偏差。

## 查看结果
{: #crt-view-results}

### 查看部署的洞察
{: #crt-view-insights}

使用 [{{site.data.keyword.aios_short}} 仪表板](https://aiopenscale.cloud.ibm.com/aiopenscale/){: external}，单击**洞察**选项卡：

  ![显示“洞察”图标](images/insight-dash-tab.png)

“洞察”页面提供已部署模型的度量概述。针对超过在运行笔记本时设置阈值的“公平性”或“准确性”度量，您可以轻松查看相应的警报。本教程中使用的数据和设置将创建与此处显示的值类似的“准确性”和“公平性”度量。

  ![显示“洞察概述”仪表板，其中包含“德国信用风险模型”磁贴](images/insight-overview-adv-tutorial-2.png)

### 查看部署的监视数据
{: #crt-view-mon-data}

1. 要查看监视详细信息，请从**洞察**页面中，单击对应于部署的磁贴。此时将显示该部署的监视数据。 
2. 在图表中滑动标记，以选择特定一小时时间范围的数据。 
3. 单击**查看详细信息**链接。

  ![监视数据](images/insight-monitor-data2.png)

现在，您可以查看所监视数据的图表。对于此示例，您可以看到针对“Sex”特征，组 `female` 接收到的有利结果“无风险”(68%) 少于组 `male` (78%)。
  ![洞察概述](images/insight-review-charts2.png)

### 查看模型事务的可解释性
{: #crt-view-explain}

对于每个部署，您可以查看特定事务的可解释性数据。

如果您已知道要查看的事务，那么可以使用事务标识快速查找该事务。单击部署磁贴后，请从导航器中单击**解释事务** ![“解释事务”选项卡](images/insight-transact-tab.png) 图标，输入事务标识，然后按 **Enter** 键。
{: tip}

如果使用 PostgreSQL 的内部 Lite 版本，那么可能无法检索数据库凭证。这可能会阻止您查看事务。
{: note}

1. 从最新偏差数据的图表中，单击**查看事务**按钮。

  ![查看事务](images/view_transactions.png)

  此时将显示部署行为有偏差的事务的列表。 
  
2. 选择其中一个事务，然后从**操作**列中单击**解释**链接。

  ![事务列表](images/transaction_list_cr.png)

现在，您将看到模型如何得出结论的解释，包括模型的置信度、造成该置信度级别的因素，以及已馈送到模型的属性。

  ![查看事务](images/view_transaction_cr.png)
  
## 后续步骤
{: #crt-next-steps}

- 了解有关[查看和解释数据](/docs/services/ai-openscale?topic=ai-openscale-it-ov)以及[监视可解释性](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)的更多信息。
