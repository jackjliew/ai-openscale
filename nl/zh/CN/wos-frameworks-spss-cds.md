---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"


keywords: supported frameworks, models, model types, limitations, limits, spss, c&ds

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

# IBM SPSS C&DS 框架
{: #frmwrks-spss}

您可以使用 IBM SPSS C&DS 在 {{site.data.keyword.aios_full}} 中执行有效内容日志记录、反馈日志记录以及度量性能准确性、运行时偏差检测、可解释性和自动除偏功能。

{{site.data.keyword.aios_full}} 计划完全支持以下 IBM SPSS Collaboration and Deployment Services (C&DS) 框架：
{: shortdesc}

目前，支持限于 {{site.data.keyword.wos4d_full}}。
{: note}

表 1. 框架支持详细信息

| 框架 | 问题类型 | 数据类型 |
|:---|:---:|:---:|
| SPSS |分类| 结构 |
{: caption="框架支持详细信息" caption-side="top"}

如果预订的 `deployment id` 包含下划线，那么将不会看到通常显示在公平性度量的已除偏选项卡上的已除偏准确性。
{: note}


## IBM SPSS Collaboration and Deployment Services (C&DS) 框架的可解释性支持
{: #frmwrks-spss-exp-supp}

- 二元模型和返回所有类的概率的 SPSS 多类模型支持可解释性。 
- 仅返回优胜类概率的 SPSS 多类模型不支持可解释性。



