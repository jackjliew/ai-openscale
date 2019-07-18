---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: Watson Studio, Watson Machine Learning, wml, machine learning, services

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

# 指定 {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}} 服务实例
{: #wml-connect}

您在 {{site.data.keyword.aios_short}} 工具中的第一步是指定 {{site.data.keyword.pm_full}} 实例。{{site.data.keyword.pm_short}} 实例是存储 AI 模型和部署的位置。
{: shortdesc}

## 先决条件
{: #wml-prereq}

您应该已在 {{site.data.keyword.aios_short}} 服务实例所在的 {{site.data.keyword.Bluemix_notm}} 帐户中供应 {{site.data.keyword.pm_full}} 实例。如果您已在其他某个帐户中供应 {{site.data.keyword.pm_full}} 实例，那么将无法使用 {{site.data.keyword.aios_short}} 通过自动有效内容日志记录来配置该实例。

## 连接 {{site.data.keyword.pm_short}} 服务实例
{: #wml-config}

{{site.data.keyword.aios_short}} 连接到 {{site.data.keyword.pm_full}} 实例中的 AI 模型和部署。

1.  从**配置**选项卡中，单击**机器学习提供程序**。

    ![显示“选择机器学习服务提供程序”屏幕，其中包含受支持的机器学习引擎的磁贴](images/wos-machine-learning-providers-selection.png)

2.  选择 {{site.data.keyword.pm_full}} 磁贴。{{site.data.keyword.aios_short}} 检查 {{site.data.keyword.Bluemix_notm}} 帐户以查找任何现有 {{site.data.keyword.pm_full}} 实例。 
3. 从 **Watson Machine Learning 服务**下拉菜单中选择实例。

    ![选择 {{site.data.keyword.pm_short}} 服务](images/gs-set-wml.png)

4.  （可选）您还可以**选择其他位置**，以在 {{site.data.keyword.Bluemix_notm}} 帐户外指定 Machine Learning 位置。以有效的 JSON 形式提供位置的凭证：

    ![设置 {{site.data.keyword.pm_short}} 实例](images/gs-get-wml.png)

    单击**保存**。

1.  {{site.data.keyword.aios_short}} 列出已部署模型；选择要监视的模型，然后单击**配置**。

### 后续步骤
{: #wml-next}

{{site.data.keyword.aios_short}} 现在可供您用于[配置监视器](/docs/services/ai-openscale?topic=ai-openscale-mo-config)。
