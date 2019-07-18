---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: databases, connections, scoring, requests, schema, REST API, API

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

# 定制机器学习引擎示例
{: #fmrk-workaround-cstmmlsengex}

使用以下示例来设置您自己的定制机器学习引擎。
{: shortdesc}

## Python 和 Flask
{: #fmrk-workaround-pandflask}

[git 上发布的定制 ML 引擎示例](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix)使用 Python 和 Flask 来为 scikit-learn 模型提供服务。

[自述文件](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix)描述如何能够在本地部署该应用程序以进行测试，以及如何在 IBM Cloud 上部署 cf 应用程序。可以在 [app.py 文件](https://github.com/pmservice/ai-openscale-tutorials/blob/master/applications/custom-ml-engine-bluemix/app.py)中找到 REST API 端点的实施。

## Node.js
{: #fmrk-workaround-nodejs}

您还可以在[此处](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-nodejs)找到以 Node.js 编写的定制机器学习引擎的示例。

## End2end 代码模式
{: #fmrk-workaround-e2ecode}

显示定制引擎部署的 end2end 示例以及与 {{site.data.keyword.aios_short}} 的集成的[代码模式](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale)。

