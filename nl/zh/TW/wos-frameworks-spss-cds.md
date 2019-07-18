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

# IBM SPSS C&DS 架構
{: #frmwrks-spss}

{{site.data.keyword.aios_full}} 打算完整支援下列的 IBM SPSS Collaboration and Deployment Services (C&DS) 架構：
{: shortdesc}

目前僅限於支援 {{site.data.keyword.wos4d_full}}。
{: note}

表 1. 架構支援明細

|架構|問題類型|資料類型|
|:---|:---:|:---:|
|SPSS|分類|結構|
{: caption="架構支援明細" caption-side="top"}

如果訂閱的 `deployment id` 含有底線，將看不見已除去偏誤的精確度；此精確度通常會出現在公平性度量的除去偏誤標籤上。
{: note}


## IBM SPSS Collaboration and Deployment Services (C&DS) 架構的可解釋性支援
{: #frmwrks-spss-exp-supp}

- 二進位模型以及會傳回所有類別之機率的 SPSS 多類別模型支援可解釋性。 
- 只會傳回勝出類別機率的 SPSS 多類別模型不支援可解釋性。



