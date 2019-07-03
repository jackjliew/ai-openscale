---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: drift, behavior, metrics

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

# ドリフトの検出 ![ベータ・タグ](images/beta.png)
{: #behavior-drift-ovr}

モデルの特徴量の中には、時間とともにその重要性や影響が変化するものがあります。その結果、関連するアプリケーションが影響を受け、ビジネスの結果にも影響が及びます。ドリフト検出により、{{site.data.keyword.aios_short}} は、モデル指標、モデル・パフォーマンス、時間の経過に伴う特徴量の加重の変化を追跡できます。ドリフトとは、隠れたコンテキストのために、予測パフォーマンスが時間とともに低下することです。時間とともにデータが変化すると、正確な予測を行うモデルの能力が低下する可能性があります。{{site.data.keyword.aios_short}} は、ユーザーが対処できるように、ドリフトを検出して強調表示します。
{: shortdesc}

{{site.data.keyword.aios_short}} は、すべてのトランザクションを分析して、ドリフトの原因になっているものを見つけます。その後、ドリフトの大きな原因になっていた属性値に基づいてレコードをグループ化します。

## ドリフトの概要
{: #behavior-drift-glance}




## 表示内容についての解釈
{: #behavior-drift-display}

![設定したしきい値を下回るドリフトが表示された公平性指標グラフ](images/fairness_metrics_001.png)


## 計算
{: #behavior-drift-math}

{{site.data.keyword.aios_short}} はドリフトを計算します 
