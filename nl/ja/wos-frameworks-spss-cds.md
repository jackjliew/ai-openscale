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

# IBM SPSS C&DS フレームワーク
{: #frmwrks-spss}

{{site.data.keyword.aios_full}} は、以下の IBM SPSS Collaboration and Deployment Services (C&DS) フレームワークをすべてサポートする予定です。
{: shortdesc}

現在のサポートは {{site.data.keyword.wos4d_full}} に制限されています。
{: note}

表 1. フレームワークのサポート詳細

| フレームワーク | 問題のタイプ | データ・タイプ |
|:---|:---:|:---:|
| SPSS | 分類 | 構造 |
{: caption="フレームワークのサポート詳細" caption-side="top"}

通常、公平性指標の「バイアス緩和済み」タブにバイアス緩和済みの正解率が表示されますが、サブスクリプションの `deployment id` に下線が含まれている場合にはこれが表示されません。
{: note}


## IBM SPSS Collaboration and Deployment Services (C&DS) フレームワークの説明性サポート
{: #frmwrks-spss-exp-supp}

- バイナリー・モデル、およびすべてのクラスの確率を返す SPSS マルチクラス・モデルでは、説明性がサポートされます。 
- 最高のクラス確率のみを返す SPSS マルチクラス・モデルでは、説明性はサポートされません。



