---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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

# グラフ・ビルダー ![ベータ・タグ](images/beta.png)
{: #chart_builder}

{{site.data.keyword.aios_short}} グラフ・ビルダーでカスタム視覚化を作成すると、実行時のモデルの予測と入力を理解しやすくなります。 グラフ・ビルダーは、モデルの予測の出力を、ビジネスで重要と見なされている特徴量またはデータ範囲と比較して表示できます。 これにより、ビジネス・チームとデータ・サイエンス・チームが AI モデルの変更を検討する契機になるような新しい傾向をデータの中に見出すことができます。 
{: shortdesc}

例えば、チュートリアルの信用リスク・モデルをよく使用している場合は、Credit History 属性の範囲別に予測クラスの配分を表示できます。 

   ![特徴量「年齢」別に、性別に関する特徴量予測を表示するグラフ](images/by_custom_chart.png)
      
   これらの範囲の Credit History の予測についてのモデルの確信度もわかります。 カスタム・グラフを使用すると、デプロイメントに送信された評価ペイロードを、選択したデータ範囲で (特徴量、予測クラス、確信度の中から選択) 分析できます。

   ![特徴量「年齢」別に、性別に関する特徴量予測を表示するグラフ](images/by_custom_chart002.png)
   
