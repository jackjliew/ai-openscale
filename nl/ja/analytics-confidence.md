---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: fairness, fairness monitor, payload, perturbation, training data, debiased

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


# 確信度別予測結果 ![ベータ・タグ](images/beta.png)
{: #anlz_metrics_payload-confidence}

デプロイメントに送信された評価ペイロードを、予測クラスおよび各クラス内の確信度の分布を参照して、選択したデータ範囲で分析できます。
{: shortdesc}

   ![確信度の分布別に予測をマップするグラフ](images/by_confidence.png)
