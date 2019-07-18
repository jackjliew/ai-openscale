---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: ai, getting started, tutorial, understanding, fast start

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

# 交互式设置教程
{: #gs-obj}

在本教程中，您将执行以下步骤：

- [供应 {{site.data.keyword.Bluemix_notm}} 机器学习和存储服务](/docs/services/ai-openscale?topic=ai-openscale-gs-obj&locale=en-US#gs-prps)。
- [设置 Watson Studio 项目，并创建、训练和部署机器学习模型](/docs/services/ai-openscale?topic=ai-openscale-gs-obj&locale=en-US#gs-setup)。
- [配置和探索模型的信任、透明度和可解释性](/docs/services/ai-openscale?topic=ai-openscale-gs-obj&locale=en-US#gs-confaios)。

## 供应 {{site.data.keyword.Bluemix_notm}} 的必备服务
{: #gs-prps}

除 {{site.data.keyword.aios_short}} 以外，要完成本教程，您还需要以下帐户和服务。

**重要事项**：为获取最佳性能，建议在与 {{site.data.keyword.aios_short}} 相同的区域中创建必备服务。要查看 {{site.data.keyword.aios_short}} 的可用位置，请参阅[服务可用性](/docs/resources?topic=resources-services_region)。

1.  使用 {{site.data.keyword.ibmid}} 登录到 [{{site.data.keyword.Bluemix_notm}} 帐户](https://{DomainName}){: external}。
1.  对于您尚未与您的帐户相关联的以下各项服务，请创建一个实例，方法是单击链接，为服务提供名称，选择 **Lite**（免费）套餐，然后单击**创建**按钮：

    - [{{site.data.keyword.DSX}}](https://{DomainName}/catalog/services/watson-studio){: external}

      ![Watson Studio](images/watson_studio.png)

    - [{{site.data.keyword.pm_full}}](https://{DomainName}/catalog/services/machine-learning){: external}

      ![Machine Learning](images/machine_learning.png)

    - [Object Storage](https://{DomainName}/catalog/services/cloud-object-storage){: external}

      ![Object Storage](images/object_storage.png)


## 设置 Watson Studio 项目
{: #gs-setup}

1.  登录到 [Watson Studio account](https://dataplatform.ibm.com/){: external} 并首先创建新项目。单击**创建项目**。

    ![Watson Studio 创建项目](images/studio_create_proj.png)

1.  单击**标准**磁贴。

    ![Watson Studio 选择“标准”项目](images/studio_create_standard.png)

1.  提供项目的名称和描述，确保在**存储**菜单中选择上一步中创建的 Object Storage 服务，然后单击**创建**。

### 将 {{site.data.keyword.Bluemix_notm}} 服务与 Watson 项目关联
{: #gs-assoc}

1.  打开 Watson Studio 项目并选择**设置**选项卡。在**关联服务**部分中，单击**添加服务**，然后单击 **Watson**。

    ![添加 Watson 服务](images/add_watson_service.png)

1.  在**机器学习**磁贴上单击**添加**链接。
2.  在**现有**选项卡上，从**现有服务实例**下拉菜单中单击先前创建的服务。
3. 单击**选择**。

### 添加 `Credit Risk` 模型
{: #gs-addmod}

1.  在 {{site.data.keyword.DSX}} 中，选择项目的**资产**选项卡，滚动到 **Watson Machine Learning 模型**部分，然后单击**新建 Watson Machine Learning 模型**按钮。

1.  从**选择模型类型**部分中，选择**从样本**和 `Credit Risk` 模型，然后单击**创建**。

    ![显示信用风险磁贴](images/credit-sample-model.png)

### 部署 `Credit Risk` 模型
{: #gs-depmod}

1.  从 `Credit Risk` 模型页面中，单击**部署**选项卡，然后单击**添加部署**。
1.  输入 `credit-risk-deploy` 作为部署的名称，然后选择 **Web Service** 部署类型。
1.  单击**保存**。

## 配置 {{site.data.keyword.aios_short}}
{: #gs-confaios}

现在已部署机器学习模型，您可以配置 {{site.data.keyword.aios_short}} 来确保模型的信任和透明度。

### 供应 {{site.data.keyword.aios_short}}
{: #gs-provaios}

1.  [供应新 {{site.data.keyword.aios_short}} 服务实例](https://{DomainName}/catalog/services/watson-openscale){: external}

    ![{{site.data.keyword.aios_short}}](images/wos-cloud-tile.png)

2.  提供服务的名称，选择 **Lite 套餐**，然后单击**创建**。

1.  选择 {{site.data.keyword.aios_short}} 实例的**管理**选项卡，然后单击**启动应用程序**按钮。此时会打开**欢迎使用 {{site.data.keyword.aios_short}}** 演示页面。
2. 对于本教程，请单击**不用，谢谢**。

### 选择数据库
{: #gs-db-choice}

接下来，需要选择数据库。您有两个选项：免费数据库，或者现有数据库或新数据库。

2. 对于本教程，请选择**使用免费 Lite 套餐数据库**磁贴。

   免费数据库存在一些重要限制。免费数据库是一个托管数据库，不允许您单独访问。 免费数据库可以让 {{site.data.keyword.aios_short}} 访问您的数据库和数据。免费数据库不符合 GDPR。请参阅[指定数据库](/docs/services/ai-openscale?topic=ai-openscale-connect-db)主题中有关其中每个选项的更完整详细信息。现有数据库可以是 PostgreSQL 数据库或 Db2 数据库。
    
    {: tip}

   ![选择数据库](images/gs-set-lite-db2.png)

1.  查看摘要数据，然后单击**保存**。确认，并在出现提示时单击**继续配置**按钮。

    此外，还会列出数据集市标识，它与 {{site.data.keyword.aios_short}} 实例标识实质相同。
    {: tip}

    ![摘要查看](images/gs-setup-summary4.png)

1.  您的屏幕可能类似于以下截屏。由于您将使用 GUI 方法对数据进行评分，因此只要选择**配置监视器**按钮即可完成此设置。

    ![评分请求代码](images/gs-config-send-scoring.png)

### 将 {{site.data.keyword.aios_short}} 连接到机器学习模型
{: #gs-ctmod}


1.  单击 **Watson Machine Learning** 磁贴，然后单击**保存**。

1.  对于本教程，请从菜单中选择 {{site.data.keyword.pm_full}} 实例，然后单击**下一步**。

    您还可以选择其他 {{site.data.keyword.pm_short}} 位置。请参阅[指定 {{site.data.keyword.pm_full}} 服务实例](/docs/services/ai-openscale?topic=ai-openscale-wml-connect)以获取其他信息。
    {: note}

    ![设置 {{site.data.keyword.pm_short}} 实例](images/gs-set-wml.png)

1.  现在，您能够选择将由 {{site.data.keyword.aios_short}} 监视的已部署模型。选择已创建并部署的模型，然后单击**下一步**。

    ![选择已部署模型](images/wos-select-model-deployment.png)

### 向模型提供一组样本数据
{: #gs-samp}

您必须先针对模型至少生成一个评分请求，以便生成监视器可以使用的载荷日志记录，然后才能配置监视器。在此部分中，将以 JSON 文件形式提供样本数据，从而生成评分请求。
1.  下载 [credit_payload_data.json](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/credit_payload_data.json) 文件。

1.  从 Watson Studio 项目的**部署**选项卡中，单击 **credit-risk-deploy** 链接，单击**测试**选项卡，然后选择 JSON 输入图标。

    ![JSON 测试](images/json_test02.png)

1.  现在，打开所下载的 `credit_payload_data.json` 文件，并将内容复制到**测试**选项卡中的 JSON 字段。单击**预测**按钮以向模型发送训练载荷并对其进行评分。

    ![JSON 预测](images/json_test03.png)

### 准备监视
{: #gs-prepmon}

1.  现在，在 {{site.data.keyword.aios_short}} 实例中，选择部署并单击**开始**。

    ![选择部署](images/wos-select-model-deployment.png)

1.  指定包含模型将预测的答案的功能部件。 （在您的数据库中，表中的哪个列包含预测值或标签？）在此情况下，模型将预测信用风险，因此请选择**风险**列，然后单击**下一步**。

    ![准备监视](images/wos-select-model-deployment.png)

1.  接下来，您将提供有关模型和训练数据的信息。单击**下一步**。

    ![准备解释](images/config-what-monitor.png)

1.  从**数据类型**菜单中，选择**数字/分类**作为部署分析的数据类型，然后单击**下一步**。

    ![选择输入类型](images/config-input-monitor.png)

1.  对于数字或分类数据，需要提供有关模型的训练数据的信息，以便配置监视器。选择**手动配置监视器**以向训练数据提供连接信息。

    ![选择配置类型](images/config-manual-monitor.png)

1.  算法类型对于监视模型度量（例如“准确性”）非常重要。由于模型可以进行的预测是“风险”或“无风险”，请选择**二元分类**[算法类型](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-understand)，然后单击**下一步**。

    ![二元](images/binary.png)

1.  样本数据的位置信息在以下屏幕上已预填充。选择**下一步**以继续。

    ![“指定训练数据的 Db2 位置”页面](images/gs-config-train-db2-monitor.png)

1.  模式和表也已预填充。单击**下一步**以继续。

    ![指定模式和训练表的 Db2 位置](images/gs-fair-config-table-db2.png)

1.  现在，必须指定包含模型将预测的答案的特征（换句话说，在数据库中，即表中的哪列包含预测值（标签））。在此情况下，模型将预测信用风险，因此请选择**风险**列，然后单击**下一步**。

    训练数据库具有为训练模型而提供的值。
    {: note}

    ![预测标签输入](images/gs-config-label.png)

1.  选择用于训练模型的列。这是模型部署在请求中期望的数据。除 `_training` 以外的所有数据列都是模型的输入。选择所有其他输入，然后单击**下一步**。

    ![可解释性输入](images/explain_inputs1.png)

1.  对于分类数据，必须标识现在包含整数但最初包含文本值的列。选择此处显示的值。

    ![可解释性输入](images/config_categories.png)

1.  查看您的选择摘要，单击**保存**，然后单击**确定**。

### 配置公平性监视
{: #gs-cfgfair}

1.  单击**公平性**。

1.  阅读有关公平性的信息，然后单击**下一步**。有关更多信息，请参阅[公平性](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)。

1.  现在，您可以选择要针对公平性监视哪些特征。对于选择的每个特征，{{site.data.keyword.aios_short}} 将监视已部署模型中一个组相对于另一个组获取有利结果的倾向。在此示例中，我们将监视**性别**和**年龄**特征。

    将单独监视功能部件，但任何去偏差操作都会一起更正所有功能部件的问题。单击**性别**和**年龄**磁贴，然后单击**下一步**。

1.  {{site.data.keyword.aios_short}} 旨在检测受监视组的偏差（与参考组相比）。对于 **Sex** 特征，请将值 `male` 添加到**参考组**，将值 `female` 添加到**受监视组**，然后单击**下一步**。

    如果受监视组的风险预测比率与参考组的比率不同，那么会将模型标记为 **Sex** 有偏差。因此，如果模型在 60% 的时间针对男性客户预测“风险”，在 20% 的时间针对女性客户预测“风险”，那么该模型有偏差。

    ![性别组](images/gender_groups1.png)

1.  为 **Sex** 分配公平性阈值。如果公平性评级超过设置的阈值，那么操作仪表板会显示警报。将阈值设置为 90%，然后单击**下一步**。

1.  对于 **Age** 特征，请将值 `26-74` 添加到**参考组**，将值 `19-25` 添加到**受监视组**，然后单击**下一步**。

    与 **Sex** 一样，如果受监视组的风险预测比率与参考组的比率不同，那么会将模型标记为 **Age** 有偏差。因此，如果年龄在 26 岁到 74 岁之间的客户的风险预测比率与年龄在 19 岁到 25 岁之间的客户的比率不同，那么模型有偏差。

    ![BP 组](images/age_groups.png)

1.  将**年龄**的阈值设置为 90%，然后单击**下一步**。

1.  将值从**来自训练数据的值**字段拖放到**有利值**和**不利值**字段。对于本教程，有利值为**无风险**，不利值为**风险**。单击**下一步**。

    {{site.data.keyword.aios_short}} 自动检测载荷日志记录数据库中的哪列包含预测值，并在**来自训练数据的值**字段中提供这些预测值。请注意，虽然训练数据库具有所提供的用于训练模型的值，但是载荷日志记录数据库包含在模型运行时收集的反馈数据，然后您可以选择性地使用该数据来重新训练和重新部署模型。
    {: note}

    ![正值和负值](images/pos_and_neg2.png)

1.  使用滑块将最小样本大小调整为 100，然后单击**下一步**。

    ![最小大小](images/gs-fair-config-sample.png)

    对于本教程，最小样本大小设置为 100。通常，建议使用更大的样本大小来确保样本大小不会太小，否则会导致结果偏差。
    {: note}

1.  查看您的选择，单击**保存**，然后单击**确定**。

    ![配置摘要](images/fair-summary.png)

    系统将显示以下窗口，其中提供已除偏的评分端点。由于本教程使用 GUI 方法而不是 CLI 对数据进行评分，因此要继续，请单击**确定**。

    ![除偏 API](images/gs-insight-debias-api.png)

### 配置准确性监视
{: #gs-cfgac}

1.  单击**准确性**。

1.  阅读有关准确性的信息，然后单击**下一步**。有关更多信息，请参阅[准确性](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor)。

1.  将准确性警报阈值设置为 90%，然后单击**下一步**。

1.  在下一个屏幕上，使用滑块将最小样本大小调整为 10，然后单击**下一步**。

    对于本教程，最小样本大小已设置为 10。通常，建议使用更大的样本大小来确保样本大小不会太小，否则会导致结果偏差。
    {: note}

1.  对于最大样本大小，请使用 10000。单击**下一步**。

1.  查看您的选择，单击**保存**，然后单击**确定**。

1.  最后，系统会呈现一个用于添加反馈数据的选项，在下一节中将对其进行介绍。现在，请通过单击**确定**关闭窗口，不必单击**添加反馈数据**按钮。

    有关更多详细信息，请参阅[配置准确性监视器](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-config)。

## 向模型提供样本反馈数据集
{: #gs-smpfeed}

要启用对准确性的监视，必须为模型提供反馈数据。在完成此操作之前，仪表板中将不会显示准确性数据。您可以通过将样本反馈数据添加到模型进行评分来一次性生成所有请求。对于此任务，您将下载包含样本反馈数据的 CSV 文件。

1.  下载 [credit_feedback_data.csv](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/credit_feedback_data.csv) 文件。

1.  在 {{site.data.keyword.aios_short}} 中，单击**洞察**选项卡。

    ![洞察](images/insight-dash-tab.png)

1.  单击已部署模型的磁贴。

    ![“洞察”选项卡 - 无数据](images/gs-insight-overview.png)

1.  然后，单击**配置监视器**。

    ![“编辑”图标显示](images/gs-insight-edit-icon.png)

1.  单击**准确性**，然后单击**反馈**。
1.  单击**添加反馈数据**，然后选择所下载的 `credit_feedback_data.csv` 文件并单击**打开**。 
2. 选择**逗号 (,)** 定界符，然后单击**选择**。

    文件大小当前限制为 8 MB。
    {: note}

    ![准确性定界符](images/accuracy-delimit.png)

添加 CSV 文件会向模型提供反馈数据。

## 配置漂移监视器
{: gs-drift-config}

有关如何配置漂移监视的信息，请参阅[配置漂移检测监视器](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-config)。

## 查看结果
{: #gs-viewres}

配置准确性监视后，将在一小时后运行准确性检查。在生产系统中，这有意义，以便仪表板可以累积反馈数据。出于本教程的目的，您可能希望在添加反馈数据后手动触发准确性检查，以便可以在**洞察**仪表板中查看结果。

要立即检查结果，请从**洞察**页面中选择部署，然后单击**立即检查公平性**或**立即检查质量**。

要了解有关解释结果的信息，请参阅[获取洞察](/docs/services/ai-openscale?topic=ai-openscale-io-ov)

## 相关信息
{: #wos-info}

- 要了解偏差，请参阅[公平性](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mf-monitor)。
- 要了解模型预测结果的良好程度，请参阅[准确性](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-acc-monitor)。
- 要了解有关解释图表、数据和事务的信息，请参阅[监视公平性、每分钟的平均请求数以及准确性](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart)。
