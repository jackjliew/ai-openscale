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

在本教程中，您将学习如何供应所需的 {{site.data.keyword.Bluemix_notm}} 服务，在 Watson Studio 中设置项目并部署样本模型，以及在 {{site.data.keyword.aios_short}} 中配置监视器。
{: shortdesc}

1. [供应 {{site.data.keyword.Bluemix_notm}} 机器学习和存储服务](/docs/services/ai-openscale?topic=ai-openscale-gs-obj#gs-prps)。
2. [设置 Watson Studio 项目，并创建、训练和部署机器学习模型](/docs/services/ai-openscale?topic=ai-openscale-gs-obj#gs-setup)。
3. [配置和探索模型的信任、透明度和可解释性](/docs/services/ai-openscale?topic=ai-openscale-gs-obj#gs-confaios)。

## 供应 {{site.data.keyword.Bluemix_notm}} 的必备服务
{: #gs-prps}

除 {{site.data.keyword.aios_short}} 以外，要完成本教程，您还需要以下帐户和服务。

**重要事项**：为获取最佳性能，建议在与 {{site.data.keyword.aios_short}} 相同的区域中创建必备服务。要查看 {{site.data.keyword.aios_short}} 的可用位置，请参阅[服务可用性](/docs/resources?topic=resources-services_region){: external}。

1.  使用 {{site.data.keyword.ibmid}} 登录到 [{{site.data.keyword.Bluemix_notm}} 帐户](https://{DomainName}){: external}。
1.  对于您尚未与您的帐户相关联的以下各项服务，请创建一个实例，方法是单击链接，为服务提供名称，选择 **Lite**（免费）套餐，然后单击**创建**按钮：

    - [{{site.data.keyword.DSX}}](https://{DomainName}/catalog/services/watson-studio){: external}

      ![Watson Studio](images/wos-watson_studio.png)

    - [{{site.data.keyword.pm_full}}](https://{DomainName}/catalog/services/machine-learning){: external}

      ![Machine Learning](images/machine_learning.png)

    - [Object Storage](https://{DomainName}/catalog/services/cloud-object-storage){: external}

      ![Object Storage](images/object_storage.png)


## 设置 Watson Studio 项目
{: #gs-setup}

1.  登录到 [Watson Studio account](https://dataplatform.ibm.com/){: external} 并首先创建新项目。单击**创建项目**。

    ![Watson Studio 创建项目](images/studio_create_proj.png)

1.  单击**创建空项目**磁贴。
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

现在，您能够选择将由 {{site.data.keyword.aios_short}} 监视的已部署模型。


### 向模型提供一组样本数据
{: #gs-samp}

您必须先针对模型至少生成一个评分请求，以便生成监视器可以使用的载荷日志记录，然后才能配置监视器。在此部分中，您将以 JSON 文件形式向 Watson Studio 提供样本数据，从而生成评分请求。

1.  下载 [credit_payload_data.json](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/credit_payload_data.json) 文件。

1.  从 Watson Studio 项目的**部署**选项卡中，单击 **credit-risk-deploy** 链接，单击**测试**选项卡，然后选择 JSON 输入图标。

    ![JSON 测试](images/json_test02.png)

1.  现在，打开所下载的 `credit_payload_data.json` 文件，并将内容复制到**测试**选项卡中的 JSON 字段。单击**预测**按钮以向模型发送训练载荷并对其进行评分。

    ![JSON 预测](images/json_test03.png)

## 后续步骤
{: #gs-next-steps-config}

通过完成以下步骤继续执行本教程：

1. [为部署准备监视器](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-select-deploy).

   要准备监视器，必须选择其中一个已部署的模型并将其添加到仪表板。从**洞察**选项卡中，单击部署磁贴，或者单击**添加到仪表板**按钮来选择已部署的模型，然后单击**配置**。

2. [设置有效内容日志记录](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-work-data)。

   在**有效内容日志记录**部分中，必须指定输入类型。

3. [设置模型详细信息](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-work-model-dets)。

   在**模型详细信息**部分中，必须记录模型详细信息。对于本教程，请选择**手动配置监视器**。

4. [配置质量监视](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor)。

   在**质量**部分中，设置质量警报阈值和样本大小。

5. [配置公平性监视](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)。

   在**公平性**部分中，选择要监视哪种特征的公平性。对于选择的每个特征，{{site.data.keyword.aios_short}} 将监视已部署模型中一个组相对于另一个组获取有利结果的倾向。虽然特征单独受监视，但是除偏会一起更正所有特征的问题。

6. [配置漂移检测监视器](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-config)。

   在**漂移**部分中，设置漂移检测模型。
   
5. [向模型提供样本反馈数据集](/docs/services/ai-openscale?topic=ai-openscale-fmt-upld-fdbk-data#fmt-upld-fdbk-data-upld-csv)。

   要启用对质量的监视，必须为模型提供反馈数据。在完成此操作之前，仪表板中将不会显示质量数据。您可以通过将样本反馈数据添加到模型进行评分来一次性生成所有请求。对于此任务，您将下载包含样本反馈数据的 CSV 文件。

6. [获取洞察](/docs/services/ai-openscale?topic=ai-openscale-io-ov)。

   配置准确性监视后，将在一小时后运行准确性检查。在生产系统中，这有意义，以便仪表板可以累积反馈数据。出于本教程的目的，您可能希望在添加反馈数据后手动触发准确性检查，以便可以在**洞察**仪表板中查看结果。

   要立即检查结果，请从**洞察**页面中选择部署，再单击其中一个**质量**度量，然后单击**立即检查质量**。
