---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits

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

# WML フレームワーク
{: #frmwrks-wml}

{{site.data.keyword.aios_full}} では以下の {{site.data.keyword.pm_full}} フレームワークが完全にサポートされています。 
{: shortdesc}

表 1. フレームワークのサポート詳細

| フレームワーク | 問題のタイプ | データ・タイプ |
|:---|:---:|:---:|
| Apache Spark MLlib | 分類 | 構造化 |
| Python 関数 | 分類 | 構造化 |
| Python 関数 | 回帰 | 構造化 |
| XGBoost | 分類 | 構造化 |
| XGBoost | 回帰 | 構造化 |
| scikit-learn | 分類 | 構造化 |
| scikit-learn | 回帰 | 構造化 |
| Keras と TensorFlow<sup>1</sup> | 分類 | 非構造化 (イメージ、テキスト) |
| Keras と TensorFlow<sup>1</sup> | 回帰 | 非構造化 (イメージ、テキスト) |
{: caption="フレームワークのサポート詳細" caption-side="top"}

<sup>1</sup>Keras のサポートには、公平性のサポートは含まれていません。
{: note}



