---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds

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

# 创建定制监视器和度量 ![beta 标签](images/beta.png)
{: #cst_mtrcs}

定制监视器会合并一组定制度量，使您能够以定量方式跟踪模型部署和业务应用程序的任何方面。 您可以定义定制度量值，并将它们与标准度量（例如，{{site.data.keyword.aios_full}} 中所监视的模型质量、性能或公平性度量）一起使用。
{: shortdesc}

要管理定制监视器和度量，必须使用 Python SDK 中包含的程序化接口。通过类似方式，您可以在 {{site.data.keyword.aios_short}} 数据集市中存储定制度量以在需要时访问这些度量。定制度量还会显示在 {{site.data.keyword.aios_short}} 仪表板中。

## 管理定制度量
{: #cst_mtrc_mgmt}

要使用定制度量，必须执行以下任务：

1. 向度量定义注册定制监视器。
2. 启用定制监视器。
3. 存储度量值。

以下高级教程说明如何执行此操作：

- [使用 Watson Machine Learning](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb)
- [使用定制 Machine Learning 引擎](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb)

您可以随时禁用和启用定制监视。如果不再需要定制监视器，那么可以将其移除。

有关更多信息，请参阅 [Python SDK 文档](http://ai-openscale-python-client.mybluemix.net/)。

## 访问和可视化定制度量
{: #cst_mtrcs_viz}

要访问和可视化定制度量，您可以使用程序化接口。 以下高级教程说明如何执行此操作：

- [使用 Watson Machine Learning](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb)
- [使用定制 Machine Learning 引擎](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb)

   有关更多信息，请参阅 [Python SDK 文档](http://ai-openscale-python-client.mybluemix.net/)。

定制度量的可视化显示在 {{site.data.keyword.aios_short}} 仪表板上。

<!---
![screen shot with metrics from Advanced Tutorial](images/adv_tutorial_metrics.png)
--->
