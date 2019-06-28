---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: Python, install, python module, setup, set up, insights, explainability

subcollection: ai-openscale

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

# 安装 Python 模块以设置 {{site.data.keyword.aios_short}}
{: #as-module}

要自动供应和配置必需的 {{site.data.keyword.cloud_notm}} 服务并查看 {{site.data.keyword.aios_full}} 应用程序（包括样本数据），您可以安装 Python 模块。
{: shortdesc}

## 关于此模块
{: #as-about}

- 该模块为技术用户提供一种备用方式来查看正常运行的 {{site.data.keyword.aios_short}} 实例，而无需自行供应和配置服务，如[入门](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted)教程中所述。
- Python 模块通过检查您拥有的服务并创建必需的服务（包括 {{site.data.keyword.aios_short}}）来运行。在该模块成功运行后，可从 {{site.data.keyword.cloud_notm}} 仪表板启动 {{site.data.keyword.aios_short}} 来查看其监视模型的方式。

## 开始之前
{: #as-prereqs}

1. [创建 {{site.data.keyword.cloud_notm}} API 密钥并将其下载](/docs/iam?topic=iam-userapikey#create_user_key)。您将需要在稍后的步骤中输入该 API 密钥。

2. [安装 Python 3 的任何发行版 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.python.org/downloads/){: new_window}。

  Python 3 包含必需的 pip 软件包管理系统。
  {: note}

3. 通过运行以下命令来安装 `ibm-ai-openscale-cli` 软件包：

    ```
    pip install -U ibm-ai-openscale-cli
    ```
    {: codeblock}

    如果在系统上安装了多个版本的 pip，那么可能需要运行 `pip3` 而不是 `pip`，例如 `pip3 install -U ibm-ai-openscale-cli`。
    {: tip}

4. 如果您具有现有 {{site.data.keyword.pm_short}} 服务实例，请检查 [{{site.data.keyword.cloud_notm}} 仪表板 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}){: new_window}，以确保服务由 {{site.data.keyword.iamshort}} (IAM) 而不是 Cloud Foundry 管理。

  **要点**：该模块会检查 {{site.data.keyword.pm_short}} 的实例。如果您具有实例，那么该模块会使用此实例。但是，如果实例由 Cloud Foundry 管理，那么必须首先[将其迁移到 IAM 资源组，然后再运行模块](/docs/resources?topic=resources-migrate#migrate)。

## 运行模块
{: #as-run}

运行以下命令：

```
ibm-ai-openscale-cli --apikey <Your API key>
```
{: codeblock}

## 在 {{site.data.keyword.aios_short}} 中查看结果
{: #as-open}

要查看对模型的公平性和准确性的洞察、受监视数据的详细信息以及个别事务的可解释性，请打开 [{{site.data.keyword.aios_short}} 仪表板![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window}。

- 要了解样本数据的方案，请阅读 [{{site.data.keyword.aios_short}} 的用例和值](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted#gs-use)。

### 查看洞察
{: #as-insights}

从 [{{site.data.keyword.aios_short}} 仪表板 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window} 中，单击**洞察**选项卡，其中显示已部署的模型的度量概述：![洞察](images/insight-dash-tab.png)

- “洞察”页面概括显示根据所配置的阈值确定的任何公平性和准确性问题。

- 每个部署显示为磁贴。模块配置了一个名为 `GermanCreditRiskModel` 的部署，如以下截屏中所示：

  ![洞察概述](images/setup01-0206.png)

### 查看监视数据
{: #as-monitoring}

1. 从“洞察”页面中，单击 `GermanCreditRiskModel` 磁贴以查看有关受监视数据的详细信息。
2. 在图表中滑动标记以查看显示数据的日期和时间段，然后单击**查看详细信息**链接。

   - 例如，以下屏幕显示特定日期和时间的数据。日期和时间根据您运行模块的时间而异。

   - 有关解释时间序列图表的信息，请参阅[监视公平性、每分钟的平均请求数以及准确性](/docs/services/ai-openscale?topic=ai-openscale-it-ov)。

    ![监视数据](images/setup02-0206.png)

3. 要查看有关 `AGE` 数据监视的详细信息，请确保从下拉菜单中选择 `AGE`。

  - 请注意，在以下截屏中，不存在任何偏差。

  - 有关解释特定小时所对应数据点的图表的信息，请参阅[监视公平性、每分钟的平均请求数以及准确性](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-intp)。

    ![查看详细信息](images/setup03-0206.png)

### 查看可解释性
{: #as-explain}

要了解造成在给定时间段存在偏差的因素，请从先前部分中显示的可视化屏幕中选择**查看事务**按钮。

对于具有偏差的事务，将会列出过去一小时的事务标识。对于此模块中使用的模型，可用的请求不存在任何偏差。因此，以下截屏中的时间段不会显示任何事务。

  ![不含任何事务的事务列表](images/setup06-0206.png)

有关查找和解释事务的信息，请参阅[解释事务](/docs/services/ai-openscale?topic=ai-openscale-ie-ov#ie-view)。

## 相关信息
{: #as-info}

- 要了解偏差，请参阅[公平性](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)。
- 要了解模型预测结果的良好程度，请参阅[准确性](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor)。
- 要了解如何解释图表和数据，请参阅[监视公平性、每分钟的平均请求数以及准确性](/docs/services/ai-openscale?topic=ai-openscale-it-ov)。
- 要了解基础因素如何影响结果，请参阅[监视可解释性](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)。
