---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, confusion matrix

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

# 混同行列 ![ベータ・タグ](images/beta.png)
{: #it-conf-mtx}

品質指標の詳細情報として、モデルが誤って分析したレコードを表示することができます。 このような異常は、二項分類モデルの場合は誤検出か検出漏れである可能性があり、多項モデルの場合はクラスの割り当ての誤りの可能性があります。 モデルが正しく分析しなかったフィードバック・レコードのリストを表示することもできます。
{: shortdesc}

一部の指標について使用できる、関連する詳細 (二項分類と多項分類の混同行列など) を確認するには、グラフをクリックします。

![品質指標の詳細テーブル](images/quality_metrics_002.png)

二項の問題が検出された場合、{{site.data.keyword.aios_full}} はターゲット・カテゴリーを `positive` または `negative` のいずれかのレベルに割り当てます。この場合、混同行列出力は、positive カテゴリーのラベルを 2 番目の行または列に置くという規則に従います。


## 手順
{: #it-conf-mtx-steps}

1. **「モデル性能 (Quality)」**のグラフ (**「正解率」**グラフなど) から、グラフ内の時間/日をクリックします。
    
    ![バイアスのあるトランザクションのリスト](images/Confusion_Matrix_040819.004.png)

1. 混同行列に、誤検出と検出漏れが表示されます。 セルをクリックして、フィードバック・レコードのサブセットを表示します。

    ![バイアスのあるトランザクションのリスト](images/Confusion_Matrix_040819.005.png)

1. フィードバック・レコードを検討し、フィードバック・レコードに対する分析の説明を要求します。

    ![バイアスのあるトランザクションのリスト](images/Confusion_Matrix_040819.006.png)

1. トランザクションがインラインで表示されます。

    ![バイアスのあるトランザクションのリスト](images/Confusion_Matrix_040819.007.png)

