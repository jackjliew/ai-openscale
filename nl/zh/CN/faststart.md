---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: ai, getting started, tutorial, understanding, fast start

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:hide-dashboard: .hide-dashboard}
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

# 自动化设置
{: #wos-fast-start}

要快速了解 {{site.data.keyword.aios_short}} 如何监视模型，请运行首次登录到 {{site.data.keyword.aios_short}} UI 时提供的演示方案选项。请参阅[使用 UI 演示](#wos-work-demo)。
{: shortdesc}

## 开始之前
{: #wos-prereqs}

在开始教程之前，必须已设置以下资源：

- {{site.data.keyword.ibmid}}
- {{site.data.keyword.aios_full}}

## 使用 UI 演示
{: #wos-work-demo}

1.  在 {{site.data.keyword.bluemix_full}} 上登录到 {{site.data.keyword.aios_short}} 实例。
1.  要使用演示方案，请单击**运行演示**。

   ![演示欢迎](images/fastpath_demo_11.31.04.png)

   在供应 {{site.data.keyword.aios_short}} 服务时，您可以查看演示方案：

   ![演示预览](images/fastpath_demo_11.31.58.png)

供应完成后，单击**执行**按钮以浏览 {{site.data.keyword.aios_short}} 仪表板，然后继续[在 {{site.data.keyword.aios_short}} 中查看结果](#wos-open)。

   ![演示执行](images/fastpath_demo_11.33.45.png)


## 在 {{site.data.keyword.aios_short}} 中查看结果
{: #wos-open}

要查看对模型的公平性和准确性的洞察、受监视数据的详细信息以及个别事务的可解释性，请打开 {{site.data.keyword.aios_short}} 仪表板。每个部署显示为磁贴。教程配置了一个名为 `GermanCreditRiskModel` 的部署，如以下截屏中所示：


   ![演示执行](images/fastpath_demo_11.33.54.png)


### 查看洞察
{: #wos-insights}

“洞察”页面概括显示根据所配置的阈值确定的任何公平性和准确性问题。

   ![演示执行](images/fastpath_demo_11.34.00.png)

### 查看监视数据
{: #wos-monitoring}

1.  从“洞察”页面中，单击 `GermanCreditRiskModelICP` 磁贴以查看有关受监视数据的详细信息。
1.  单击标记并在图表中将其拖动，以查看显示数据的日期和时间段，然后单击**查看详细信息**链接。或者，可以单击图表中的不同时间段，以更改查看的数据。

     - 例如，以下屏幕显示特定日期和时间的数据。日期和时间根据您运行模块的时间而异。

     - 有关解释时间序列图表的信息，请参阅[监视公平性、每分钟的平均请求数以及准确性](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart)。

   ![演示执行](images/fastpath_demo_11.34.17.png)

1.  要查看有关 `SEX` 数据监视的详细信息，请确保从下拉菜单中选择 `SEX`。

    - 请注意，在以下截屏中，存在偏差。
    
   ![演示执行](images/fastpath_demo_11.34.27.png)

    - 有关解释特定小时所对应数据点的图表的信息，请参阅[数据可视化](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart#itc-data-visual)。


### 查看可解释性
{: #wos-explain}

要了解造成在给定时间段存在偏差的因素，请从先前部分中显示的可视化屏幕中单击**有偏差事务**按钮。

   ![演示执行](images/fastpath_demo_11.35.06.png)

对于具有偏差的事务，将会列出过去一小时的事务标识。对于此模块中使用的模型，可用的请求存在偏差。

   ![演示执行](images/fastpath_demo_11.35.12.png)

有关查找和解释事务的信息，请参阅[监视可解释性](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-ie-ov)。

   ![演示执行](images/fastpath_demo_11.35.50.png)

## 完成教程
{: #wos-done-demo}

1. 单击**完成**按钮。

   ![演示执行](images/fastpath_demo_11.37.22.png)

2. 单击**执行**按钮以开始使用 {{site.data.keyword.aios_short}}。

   ![演示执行](images/fastpath_demo_11.33.45.png)


## 相关信息
{: #wos-info}

- 要了解偏差，请参阅[公平性](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mf-monitor)。
- 要了解模型预测结果的良好程度，请参阅[准确性](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-acc-monitor)。
- 要了解有关解释图表、数据和事务的信息，请参阅[监视公平性、每分钟的平均请求数以及准确性](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart)。
