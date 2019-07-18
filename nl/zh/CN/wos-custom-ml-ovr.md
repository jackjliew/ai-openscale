---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: machine learning engines, frameworks, Microsoft Azure, Amazone SageMaker, custom ML engine 

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

# 定制机器学习引擎
{: #fmrk-workaround-customengine}

定制机器学习引擎为机器学习模型和 Web 应用程序提供基础结构和托管功能。{{site.data.keyword.aios_short}} 支持的定制机器学习引擎必须符合以下需求：

- 公开两种类型的 REST API 端点：

   * 发现端点（执行 GET 操作以获取部署和详细信息的列表）
   * 评分端点（在线和实时评分）

- 所有端点需要兼容 Swagger 规范才能受支持。

- 以部署作为目标或来源的输入有效内容和输出必须符合规范中描述的 JSON 文件格式。

目前，仅支持 `BasicAuth` 或 `none` 格式。
{: Note}

以下示例显示 REST API 端点规范：

![从 Swagger 文档中显示 REST API 端点规范](images/wosdeployments.png)


以下示例显示输入有效内容的格式：

![显示输入有效内容示例](images/wosinputdata.png)


## 定制机器学习引擎何时是我的最佳选项？
{: #fmrk-workaround-enging-choice}

当以下情况成立时，定制机器学习引擎是最佳选项：

- 您不是使用任何可用的现成产品来为机器学习模型提供服务。您只是开发了自己的系统来执行此操作。{{site.data.keyword.aios_short}} 中没有且将来也不会有与此对应的直接支持。
- {{site.data.keyword.aios_short}} 尚不支持您使用的来自第三方供应商的服务引擎。在此情况下，请考虑开发定制机器学习引擎作为原始或本机部署的包装器。

## 后续步骤
{: #fmrk-workaround-nxt-steps-over}

通过使用其中一个[定制机器学习示例](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-cstmmlsengex)来实施您自己的解决方案。
