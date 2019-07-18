---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds

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

# モデル性能の指標の概要 ![ベータ・タグ](images/beta.png)
{: #anlz_metrics}

モデル性能モニタリングを使用して、モデルがどの程度正確な結果を予測するかを判別します。 モデル性能モニタリングを有効にすると、デフォルトでは 1 時間ごとに指標のセットが生成されます。 これらの指標は、**「今すぐ品質を評価」**ボタンをクリックするか、Python クライアントを使用して、オンデマンドで生成できます。

品質指標は、以下の情報に基づいて計算されます。

- 手動でラベル付けするフィードバック・データ
- これらのデータに関するモニター対象デプロイメントの応答

適切なモニタリングのために、フィードバック・データを {{site.data.keyword.aios_short}} に定期的にログ記録する必要があります。 フィードバック・データを提供するには、「フィードバック・データの追加」オプションを使用するか、Python クライアントまたは REST API を使用します。

Microsoft Azure ML Studio、Microsoft Azure ML Service、Amazon Sagemaker ML などの {{site.data.keyword.aios_short}} 以外の機械学習エンジンでは、モデル性能モニタリングにより、モニター対象のデプロイメントに関する追加の評価要求が作成されます。
{: note}

{{site.data.keyword.aios_short}} ダッシュボードで、すべての指標値を経時的に確認できます。

![ROC 曲線下面積のドリフトが表示された品質指標グラフ](images/quality_metrics_001.png)


一部の指標について使用できる、関連する詳細 (二項分類と多項分類の混同行列など) を確認するには、グラフをクリックします。

![品質指標の詳細テーブル](images/quality_metrics_002.png)

## サポートされている品質指標
{: #anlz_metrics_supqualdets}

以下の品質指標が {{site.data.keyword.aios_short}} によってサポートされています。

- [ROC 曲線下面積](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_roc)
- [PR 曲線下面積](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality-area-pr)
- [正解率](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-accuracy-opener)
- [真陽性率 (TPR)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_tpr)
- [偽陽性率 (FPR)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_fpr_false)
- [再現率](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_recall)
- [適合率](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_precision)
- [F1 値](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_f1-measr)
- [対数損失](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_log_loss)

## サポートされている品質の詳細
{: #anlz_metrics_supqualdets_suppr_dets}

以下の品質指標に関する詳細が {{site.data.keyword.aios_short}} によってサポートされています。

### 混同行列
{: #anlz_metrics_supqualdets_confusion-quickovr}

混同行列は、モニター対象デプロイメントの応答が、どのフィードバック・データに関して正しく、どのフィードバック・データに関しては正しくないかを理解するのに役立ちます。

詳しくは、[混同行列](/docs/services/ai-openscale?topic=ai-openscale-it-conf-mtx)を参照してください。
