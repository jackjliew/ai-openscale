---

title: {{site.data.keyword.aios_short}} 的机器学习模型的信任和透明度
description: Monitor your machine learning deployments for bias, accuracy, and explainability
duration: 120
intro: In this extended tutorial, you will provision IBM Cloud machine learning and data services, create and deploy machine learning models in Watson studio, and configure the new IBM {{site.data.keyword.aios_full}} product to monitor your models for trust and transparency.
takeaways:
- See how {{site.data.keyword.aios_short}} provides trust and transparency for AI models
- Understand how IBM Cloud services and Watson Studio technologies can provide a seamless, AI-driven customer experience

copyright:
  years: 2018, 2019
lastupdated: "2019-02-05"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# 教程（高级）
{: #tadv-tutorial-advanced}

## 场景
{: #tadv-scenario}

某车辆租赁公司已收集有关客户满意度的反馈数据。所呈现的模型使用此数据来预测要对客户跟进的操作过程，例如，为其下次租赁提供凭单。

该模型使用客户数据字段标识（标识号）、GENDER、STATUS（单身或已婚）、CHILDREN（数字）、AGE、CUSTOMER STATUS（活跃或不活跃）、CAR OWNER（是或否）、CUSTOMER SERVICE（客户评论）、SATISFACTION（满意或不满意）以及 BUSINESS AREA（相关产品或服务）来为 ACTION 数据字段预测四个值（不适用、凭单、免费升级、按需提车）之一。

## 先决条件
{: #tadv-prereqs}

要完成本教程，您将需要：

- [Watson Studio ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://dataplatform.ibm.com/){: new_window} 帐户。
- [{{site.data.keyword.cloud_notm}} ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}){: new_window} 帐户。

在教程期间，您将供应以下 Lite（免费）{{site.data.keyword.cloud_notm}} 服务：

- Machine Learning
- Apache Spark
- Object Storage

您还将供应以下**付费** {{site.data.keyword.cloud_notm}} 服务：

- PostgreSQL

  通过转换为使用信用卡的付费帐户，可以获取 200 美元 {{site.data.keyword.cloud_notm}} 信贷。如果您已具有付费帐户，那么将针对一个月的首个 1 GB 的存储成本收到一笔 16 美元的一次性退款。
  {: tip}

PostgreSQL  数据库和 {{site.data.keyword.pm_full}} 实例必须部署在同一 {{site.data.keyword.cloud_notm}} 帐户中。
{: important}

如果您已供应必要的服务，例如，如果已完成其他教程，请在下面继续[设置 Watson Studio 项目](#tadv-setup-ws)。

## 简介
{: #tadv-intro}

在本教程中，您将：

- 供应 {{site.data.keyword.cloud_notm}} 机器学习和存储服务
- 设置 Watson Studio 项目，并运行 Python 笔记本以创建、训练和部署机器学习模型
- 运行 Python 笔记本以创建数据集市，配置性能、准确性和公平性监视器，以及创建要监视的数据
- 在 {{site.data.keyword.aios_short}}“洞察”选项卡中查看结果

## 供应 {{site.data.keyword.cloud_notm}} 服务
{: #tadv-svcs}

使用 IBM 标识登录到 [{{site.data.keyword.cloud_notm}} 帐户 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}){: new_window}。供应服务时（尤其在使用 Apache Spark、Object Storage 和 Db2 Warehouse 的情况下），请验证所选组织和空间是否对于所有服务都相同。

### 创建 Watson Studio 帐户
{: #tadv-stac}

- [创建 Watson Studio 实例 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/catalog/services/watson-studio){: new_window}（如果您尚未具有与帐户关联的实例）：

  ![Watson Studio](images/watson_studio.png)

- 指定服务的名称，选择 Lite（免费）套餐，然后单击**创建**按钮。

### 供应 Machine Learning 服务
{: #tadv-pml}

- [供应 Watson Machine Learning 实例 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/catalog/services/machine-learning){: new_window}（如果您尚未具有与帐户关联的实例）：

  ![Machine Learning](images/machine_learning.png)

- 指定服务的名称，选择 Lite（免费）套餐，然后单击**创建**按钮。

- 记下 Machine Learning 服务凭证。在机器学习实例中，单击页面左侧的**服务凭证**链接。对凭证进行命名并单击**添加**。然后，从凭证列表中，单击**查看凭证**并复制凭证以供将来使用。

### 供应 Spark 服务
{: #tadv-ps}

- [供应 Spark 服务 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/catalog/services/apache-spark){: new_window}（如果您尚未具有与帐户关联的服务）：

  ![Apache Spark](images/spark.png)

- 指定服务的名称，选择 Lite（免费）套餐，然后单击**创建**按钮。

- 记下 Spark 实例的服务凭证。打开 Spark 实例，然后单击左侧菜单中的**服务凭证**。单击**新建凭证**按钮，对凭证进行命名，并单击**添加**。然后，单击刚创建的集旁边的**查看凭证**链接，然后复制这些凭证以供将来使用。

### 供应 Object Storage 服务
{: #tadv-pos}

- [供应 Object Storage 服务 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/catalog/services/cloud-object-storage){: new_window}（如果您尚未具有与帐户关联的服务）：

  ![Object Storage](images/object_storage.png)

- 指定服务的名称，选择 Lite（免费）套餐，然后单击**创建**按钮。

### 供应付费 PostgreSQL 服务
{: #tadv-ppgs}

- [供应付费 PostgreSQL 服务 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/catalog/services/compose-for-postgresql){: new_window}（如果您尚未具有与帐户关联的服务）。

  ![Compose for PostgreSQL](images/postgres.png)

- 指定服务的名称，选择 Standard 套餐，然后单击**创建**按钮。

  通过转换为使用信用卡的付费帐户，可以获取 200 美元 {{site.data.keyword.cloud_notm}} 信贷。如果您已具有付费帐户，那么将针对一个月的首个 1 GB 的存储成本收到一笔 16 美元的一次性退款。
  {: tip}

- 记下 PostgreSQL 实例的服务凭证。打开现有（或新创建）的 PostgreSQL 实例，然后单击左侧菜单中的**服务凭证**。单击**新建凭证**按钮，对凭证进行命名，并单击**添加**。然后，单击刚创建的集旁边的**查看凭证**链接，然后复制这些凭证以供将来使用。

<!---

### Provision a Db2 Warehouse service
{: #tadv-pdb2}

- [Provision a Db2 Warehouse service ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/catalog/services/db2-warehouse){: new_window} if you do not already have one associated with your account:

  ![Db2 Warehouse](images/db2_warehouse.png)

- Give your service a name, choose the Entry plan, and click the **Create** button.

- Make note of the service credentials for your Db2 Warehouse instance. Open your existing (or newly-created) Db2 Warehouse instance and click on **Service credentials** in the left-hand menu. Click the **New credential** button, name your credentials, and click **Add**. Then, click the **View credentials** link next to the set you just created, and copy these credentials for later use.

### Upload training and feedback data to Db2 Warehouse
{: #tadv-uptf}

- Download the [car_rental_training_data.csv](https://github.com/watson-developer-cloud/doc-tutorial-downloads/blob/master/ai-openscale/car_rental_training_data.csv){: new_window} file.

- Open your existing (or newly-created) Db2 Warehouse from the [IBM Cloud console ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}){: new_window}, click **Manage** from the left side panel, and then click the green **Open** button.

- If necessary, use your Db2 credentials `username` and `password` to log in to Db2 Warehouse.

- Once Db2 Warehouse has opened, click the **Menu** button and select **Load** from the dropdown:

  ![Load Menu](images/db2_load.png)

- Browse to the training data file, or drag and drop it into the appropriate area on the form. Click **Next**. Select a Schema from the list of load targets; this is usually in a format like `DASH12345`. Then click **New Table** on the right:

  ![New Table](images/new_table.png)

- Name your table CAR\_RENTAL\_TRAINING, and click the **Create** button:

  ![New Table Create](images/new_table_create.png)

- Click **Next** to preview the data. On the preview screen, set the **Separator** field to a semicolon (;) and make sure the **Header in first row** option is checked:

  ![Separator and Header](images/separator.png)

  **NOTE**: By default, the **Detect data types** option is selected.

  ![Data type](images/data-type.png)

  When selected, for columns set with the `VARCHAR` data type, the maximum number of characters allowed for that column is automatically determined by the largest data point uploaded for that column. If you expect that future data for a table column may exceed the automatically-determined maximum, simply unselect the **Detect data types** option, and edit the maximum column value manually.

  ![手动设置数据类型](images/data-type-manual.png)

- 现在，训练数据应在列中正确显示。单击**下一步**以继续，然后单击**开始装入**以装入数据。

--->

## 设置 Watson Studio 项目
{: #tadv-setup-ws}

- 登录到 [Watson Studio 帐户 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://dataplatform.ibm.com/){: new_window}。单击右上方的帐户头像图标，并验证您使用的帐户是否与用于创建 {{site.data.keyword.cloud_notm}} 服务的帐户相同：

  ![相同帐户](images/same_account.png)

- 在 Watson Studio 中，首先创建新项目。选择“创建项目”：

  ![Watson Studio 创建项目](images/studio_create_proj.png)

- 选择**标准**磁贴，以创建项目：

  ![Watson Studio 选择“标准”项目](images/studio_create_standard.png)

- 指定项目的名称和描述，确保在**存储**下拉菜单中选择上一步中创建的 Object Storage 服务，然后单击**创建**。

### 将 {{site.data.keyword.cloud_notm}} 服务与 Watson 项目关联
{: #tadv-acsw}

- 打开 Watson Studio 项目并选择**设置**选项卡。在**关联服务**部分中，单击**添加服务**下拉菜单，然后选择 **Watson**：

  ![添加 Watson 服务](images/add_watson_service.png)

- 单击 **Machine Learning** 磁贴上的**添加**链接，然后选择**现有**选项卡。从**现有服务实例**下拉菜单中选择先前部分中创建的服务，然后单击**选择**。

- 从项目设置选项卡中，再次选择**添加服务**，然后从下拉菜单中选择 **Spark**。从**现有**选项卡中，选择所创建的 Spark 服务，然后单击**选择**。

## 创建和部署机器学习模型
{: #tadv-deploy-ml}

### 将 `CARS4U Action Recommendation - model` 笔记本添加到 Watson Studio 项目

- 下载以下文件：

    - [CARS4U Action Recommendation - model ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/CARS4U%20action%20recommendation%20-%20model.ipynb){: new_window}

- 从 Watson Studio 项目中的**资产**选项卡单击**添加到项目**按钮，然后从下拉菜单中选择**笔记本**：

  ![添加连接](images/add_notebook.png)

- 选择**从文件**：

  ![“新建笔记本”表单](images/new_notebook_name.png)

- 然后，单击**选择文件**按钮，并选择所下载的“CARS4U Action Recommendation - model”：

  ![“新建笔记本”表单](images/new_notebook_name2.png)

- 在**选择运行时**部分中，从下拉列表中选择先前创建的 Spark 实例：

  ![Spark 运行时](images/spark_runtime.png)

- 单击**创建笔记本**。

### 编辑并运行 `CARS4U Action Recommendation - model` 笔记本
{: #tadv-ern}

`CARS4U Action Recommendation - model` 笔记本包含将运行的 python 代码中每个步骤的详细指示信息。在完成笔记本工作时，请花费一些时间来了解每个命令所执行的操作。
{: tip}

- 从 Watson Studio 项目的**资产**选项卡单击 `CARS4U Action Recommendation - model` 笔记本旁边的**编辑**图标以编辑该笔记本。

- 在第 2.2 节“将数据上载到 PostgreSQL 数据库”中，将 Postgres 服务凭证替换为在先前部分中创建的服务凭证。

- 在第 4 节“在存储库中存储模型”中的**提示**下，将 Watson Machine Learning 凭证替换为在先前部分中创建的凭证。

- 一旦输入凭证，笔记本即可运行。单击**内核**菜单项，然后从菜单中选择**全部重新启动并运行**：

  ![重新启动并运行](images/restart_and_run.png)

  这将在项目中创建、训练和部署 **CARS4U - Action Recommendation Model**。您可以通过选择 Watson Studio 项目的**部署**选项卡，然后单击 **CARS4U - Area and Action Model Deployment** 链接来验证模型是否已部署。

## 配置 {{site.data.keyword.aios_short}}
{: #tadv-config-aios}

### 供应 {{site.data.keyword.aios_short}}
{: #tadv-paios}

- 如果您尚未供应 {{site.data.keyword.aios_short}} 的实例，请单击 {{site.data.keyword.cloud_notm}} 帐户中的**目录**链接，然后对“OpenScale”进行过滤。选择 {{site.data.keyword.aios_short}} 的磁贴。

<!---
  ![{{site.data.keyword.aios_short}}](images/wos-cloud-tile.png)
--->

- 指定服务的名称，选择 Lite 套餐，然后单击**创建**。

### 将 {{site.data.keyword.aios_short}} 连接到机器学习模型
{: #tadv-cmlm}

由于已部署机器学习模型，您可以配置 {{site.data.keyword.aios_short}} 来确保模型的信任和透明度。选择 {{site.data.keyword.aios_short}} 实例的**管理**选项卡，然后单击**启动应用程序**按钮。此时将打开“{{site.data.keyword.aios_full}} 入门”页面；单击**开始**。

- 选择“Watson Machine Learning”磁贴，然后单击**下一步**。

  ![设置 WML 实例](images/gs-wml-default.png)

- 从下列菜单中选择 Watson Machine Learning 实例，然后单击**下一步**。

  ![设置 WML 实例](images/gs-set-wml.png)

- 现在，您能够选择 {{site.data.keyword.aios_short}} 将监视哪些已部署的模型。选中已创建并部署的模型；单击**下一步**以接受此选择：

  ![选择已部署的模型](images/gs-set-deploy.png)

- 接下来，需要选择 PostgreSQL 数据库。您有两个选项：免费 Lite 套餐数据库，或者现有数据库或新数据库。对于本教程，请选择**使用现有数据库或购买新数据库**磁贴。

    ![选择数据库](images/gs-set-lite-db1.png)

  请参阅[指定数据库](/docs/services/ai-openscale?topic=ai-openscale-connect-db)主题中有关其中每个选项的更多完整详细信息。
  {: note}

- 一旦选择“使用现有数据库或购买新数据库”选项，{{site.data.keyword.aios_short}} 便会检查 {{site.data.keyword.cloud_notm}} 帐户以查找现有 Compose for PostgreSQL 数据库。

  从**模式**下拉菜单中选择“data_mart”模式。

  ![选择数据库](images/gs-set-schema1.png)

- 选择数据库和模式后，单击**下一步**以查看摘要数据，然后单击**保存**。

  ![选择数据库](images/gs-setup-summary3.png)

  当出现提示时，单击**退出到仪表板**。

## 创建数据集市并配置性能、准确性和公平性监视器
{: #tadv-config-monitors}

### 将 `{{site.data.keyword.aios_short}} and Watson ML engine` 笔记本添加到 Watson Studio 项目
{: #tadv-aomn}

`{{site.data.keyword.aios_short}} and Watson ML engine` 笔记本包含将运行的 python 代码中每个步骤的详细指示信息。在完成笔记本工作时，请花费一些时间来了解每个命令所执行的操作。
{: tip}

- 下载以下文件：

    - [{{site.data.keyword.aios_short}} and Watson ML engine ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Watson%20ML%20Engine.ipynb){: new_window}

- 从 Watson Studio 项目中的**资产**选项卡单击**添加到项目**按钮，然后从下拉菜单中选择**笔记本**：

  ![添加连接](images/add_notebook.png)

- 选择**从文件**：

  ![“新建笔记本”表单](images/new_notebook_name.png)

- 然后，单击**选择文件**按钮，并选择所下载的“{{site.data.keyword.aios_short}} and Watson ML engine”：

  ![“新建笔记本”表单](images/new_notebook_name3.png)

- 在**选择运行时**部分中，从下拉列表中选择先前创建的 Spark 实例：

  ![Spark 运行时](images/spark_runtime.png)

- 单击**创建笔记本**。

### 编辑并运行 `{{site.data.keyword.aios_short}} and Watson ML engine` 笔记本
{: #tadv-eromn}

- 从 Watson Studio 项目的**资产**选项卡单击 `{{site.data.keyword.aios_short}} and Watson ML engine` 笔记本旁边的**编辑**图标以编辑该笔记本。

- 在第 1.1 节“安装和认证”中：

    - 在**操作：获取 instance_id (GUID) 和 apikey** 下，遵循指示信息以获取凭证。将 `aios_credentials` 替换为您自己的凭证。

    - 接下来，在**操作：在此处添加 Watson Machine Learning 凭证**中，将 Watson Machine Learning 凭证替换为先前创建的凭证。

    - 最后，在**操作：在此处添加 PostgreSQL 凭证**中，将 Postgres 凭证替换为先前创建的凭证。

- 一旦输入凭证，笔记本即可运行。单击**内核**菜单项，然后从菜单中选择**全部重新启动并运行**：

  ![重新启动并运行](images/restart_and_run.png)

  这将设置数据集市，启用载荷日志记录，对性能、准确性和公平性监视器进行配置和评分，以及将这些度量提供给 {{site.data.keyword.aios_short}} 实例。

## 查看结果
{: #tadv-results}

### 查看部署的洞察
{: #tadv-vide}

使用 [{{site.data.keyword.aios_short}} 仪表板 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window}，单击**洞察**选项卡：

  ![洞察](images/insight-dash-tab.png)

“洞察”页面提供已部署的模型的度量概述。针对已降至低于在运行笔记本时设置的阈值 (70%) 的“公平性”或“准确性”度量，您可以轻松查看相应警报。本教程中使用的数据和设置将创建与此处显示的值类似的“准确性”和“公平性”度量。

  ![洞察概述](images/insight-overview-adv-tutorial.png)

### 查看部署的监视数据
{: #tadv-vmdd}

通过单击“洞察”页面上的磁贴来选择部署。此时将显示该部署的监视数据。在图表中滑动标记，以选择期间运行了笔记本的时间范围的数据。然后，选择**查看详细信息**链接。

  ![监视数据](images/insight-monitor-data1.png)

现在，您可以查看所监视数据的图表。对于此示例，可以使用**特征**下拉菜单选择“Children”或“Gender”，以便查看有关受监视数据的详细信息。

  ![洞察概述](images/insight-review-charts1.png)

<!---

### 查看模型事务的可解释性
{: #tadv-vemt}

从所监视数据的图表中选择**查看事务**按钮。

  ![查看事务](images/view_transactions.png)

  此时将列出过去一小时的事务的列表。复制其中一个事务标识。

  ![事务列表](images/transaction_list.png)

使用 [{{site.data.keyword.aios_short}} 仪表板 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window}，单击**可解释性**选项卡：

  ![可解释性](images/explainability.png)

将复制的事务标识值粘贴到搜索框中，然后按键盘上的**回车**键。现在，您将看到模型如何得出结论的解释，包括模型的置信度、造成该置信度级别的因素，以及已馈送到模型的属性。

  ![查看事务](images/view_transaction1.png)

--->

## 后续步骤
{: #tadv-next}

- 了解有关[查看和解释数据](/docs/services/ai-openscale?topic=ai-openscale-it-ov)以及[监视可解释性](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)的更多信息。
