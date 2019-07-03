---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: deployment, monitors, data

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

# 为部署准备监视器
{: #mo-config}

为使用 {{site.data.keyword.aios_short}} 跟踪的每个部署设置和启用监视器。
{: shortdesc}

## 配置
{: #io-conf}

**配置**选项卡 (![“配置”选项卡](images/insight-config-tab.png)) 打开所选部署的配置摘要。

  ![配置摘要](images/insight-config-summary.png)

您可以从此处直接编辑部署监视器的配置设置。

## 选择部署
{: #mo-select-deploy}

1.  首先，必须选择部署。

    1. 单击**添加部署**按钮。这将显示可用模型部署的列表。
    2. 单击模型部署，然后单击**配置**。

    如果给定模型有多个部署，那么在配置一个部署时，也会配置同一模型的所有其他部署。
    {: note}

    ![选择部署页面](images/config-select-deploy.png)

1.  单击**配置监视器**按钮。

    ![准备监视](images/config-prep-monitor.png)

## 提供有效内容日志记录详细信息
{: #mo-work-data}

您必须提供有关模型和训练数据的信息。有关训练数据的更多信息，请参阅 [ 为什么 {{site.data.keyword.aios_short}} 需要访问我的培训数据？](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

![准备解释](images/config-what-monitor.png)

- 如果使用与 {{site.data.keyword.aios_short}} 实例位于同一区域中的 {{site.data.keyword.pm_full}} 实例，那么会自动为您配置有效内容日志记录信息。
- 否则，必须从**有效内容日志记录**选项卡和窗口中输入有关数据和算法类型以及有效内容日志记录的信息。 

   根据您的选择，存在特定需求。有关更多信息，请参阅[数字/分类数据](https://test.cloud.ibm.com/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mo-config#mo-datan)。

   您需要复制要运行的其中一个代码片段，然后才能配置监视器。运行 cURL 命令（在客户机应用程序中）或 Python 命令（在数据科学笔记本中）。这提供了一种在有效内容数据中记录模型部署请求和写入响应数据的方法。

## 提供模型详细信息
{: #mo-work-model-dets}

提供有关模型的信息，以便 {{site.data.keyword.aios_short}} 可以访问数据库并了解模型的设置方式。

具体而言，要配置监视器，必须执行以下任务：

1. 指定训练数据的位置。通过输入位置、主机名或 IP 地址、数据库名称以及认证信息来完成此操作。
2. 在数据库中，必须通过选择模式和表来选择训练表。
3. 从训练表中选择标签列。
4. 选择用于训练 AI 部署的特征。
5. 选择文本特征和分类特征。
6. 选择部署预测列。
7. 最后，可以在保存之前复审模型详细信息。

以下部分提供根据模型类型（[数字/分类数据](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mo-config#mo-datan)或[图像和非结构化文本](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mo-config#mo-datai)）所遇到的某些具体信息。


### 数字/分类数据
{: #mo-nuca}

对于数字或分类数据，需要提供有关模型的训练数据的信息，以便配置监视器。

- **手动配置监视器** - 需要向训练数据提供连接信息。

    - 选择[算法类型](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-understand)，然后单击**下一步**：

      训练数据的格式必须与模型匹配。例如，如果模型期望特征 `Gender` 的值为 `M` 和 `F`，那么训练数据应具有 `M` 和 `F`，而不是 `Male` 和 `Female`。{{site.data.keyword.aios_short}} 的当前发行版仅支持 Db2 数据库或 Cloud Object Storage 位置。{: important}

    - 指定位置（`Db2` 或 `Cloud Object Storage`），然后：

        - 对于 Db2 数据库，请输入以下信息：

            - 主机名或 IP 地址
            - 端口
            - 数据库（名称）
            - 用户名
            - 密码

        - 对于 Cloud Object Storage，请输入以下信息：

            - 登录 URL：登录 URL 必须与训练数据所在的存储区的区域设置相匹配。您将在下一步中指定训练数据存储区。
              
            - 资源实例（标识）
            - API 密钥

    - 要确保连接有效，请单击**测试**按钮以连接到训练数据。
    - 在训练数据所在的 Db2 数据库或 Cloud Object Storage 中指定确切位置。

        - 对于 Db2 数据库，请同时选择模式和包含模型期望的列的训练表。
        - 对于 Cloud Object Storage，请选择存储区和数据集。

- **上载配置文件** - 如果首选将训练数据保持专用，请选择此选项。可以使用定制 Python 笔记本为 {{site.data.keyword.aios_short}} 提供用于分析训练数据的信息而不提供对训练数据本身的访问权。

  通过运行 Python 笔记本，可以捕获模式列中的不同值以及列名。此外，还可以使用笔记本来预配置公平性监视器。

   - 下载[定制笔记本](https://github.com/IBM-Watson/aios-data-distribution/blob/master/training_statistics_notebook.ipynb){: external}，并将任何凭证替换为您自己的凭证。
   - 仔细查看笔记本，在适当情况下指定模型的数据。保存笔记本。
   - 运行笔记本以生成 JSON 格式的配置文件。
   - 上载 JSON 配置文件。

     ![上载配置 JSON](images/config-json-monitor.png)

- {{site.data.keyword.aios_short}} 在 {{site.data.keyword.pm_full}} 中从使用模型存储的元数据找到训练数据。选择训练数据中包含预测值的标签列。
- 选择用于训练模型的列 - 这些列是模型部署在请求中期望的特征。
- 最后，选择包含文本并已转换为整数的列。例如，如果原始训练数据针对 `Gender` 包含 `Male` 和 `Female`，并且它们现已分别映射到 `0` 和 `1`，那么训练数据现在针对 `Gender` 列包含值 `0` 和 `1`。标识此类现在包含整数但最初包含文本值的列。

### 图像和非结构化文本
{: #mo-imun}

- **图像**

  对于接受图像作为输入的模型，图像需要表示为 (高度) x (宽度) x (通道数) 格式，其中每个点表示每个像素的单色值或 RGB 值。

- **非结构化文本**

   对于接受文本作为输入的模型，预计模型会接受整个文本，而不是文本的向量化表示。

## 查看并保存配置
{: #mo-save}

查看您的选择的摘要，然后单击**保存**以继续。

  ![选择数据表](images/config-summary-monitor.png)

### 后续步骤
{: #mo-next}

要开始配置监视器，请单击**准确性**选项卡，然后单击**开始**。
