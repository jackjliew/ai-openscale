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

# 自訂機器學習引擎範例
{: #fmrk-workaround-cstmmlsengex}

使用下列範例，來設置您自己的自訂機器學習引擎。
{: shortdesc}

## Python 和 Flask
{: #fmrk-workaround-pandflask}

[發佈到 Git 上的自訂 ML 引擎範例](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix)使用 Python 和 Flask 來處理 scikit-learn 模型。

[README 檔](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix)說明基於測試用途，如何將應用程式部署在本端，以及如何將 cf 應用程式部署在 IBM Cloud 上。REST API 端點的實作可以在 [app.py 檔](https://github.com/pmservice/ai-openscale-tutorials/blob/master/applications/custom-ml-engine-bluemix/app.py)中找到。

## Node.js
{: #fmrk-workaround-nodejs}

您也可以找到自訂機器學習引擎範例，它撰寫在[這裡的 Node.js](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-nodejs) 中。

## 端對端程式碼型樣
{: #fmrk-workaround-e2ecode}

[程式碼型樣](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale)顯示自訂引擎部署以及與 {{site.data.keyword.aios_short}} 整合的端對端範例。

