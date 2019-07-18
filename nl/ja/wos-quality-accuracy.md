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

# 正解率
{: #accuracy-opener}

正解率は、モデルの予測の正解の割合を表す指標です。
{: shortdesc}

## 一目でわかる正解率
{: #anlz_metrics_supqualdets_acc}

- **説明**: 正確な予測の比率
- **デフォルトのしきい値**: 下限 = 80%
- **デフォルトの推奨**:
   - **上昇傾向**: 上昇傾向は、指標が向上していることを示します。 これは、モデルの再訓練の効果が出ていることを意味します。
   - **下降傾向**: 下降傾向は、指標が悪化していることを示します。 フィードバック・データと訓練データの差異が明らかに広がっています。
   - **不規則または不定期変化**: 不規則変化または不定期変化は、フィードバック・データが各評価で一貫性がないことを示します。 モデル性能モニタリングの最小サンプル・サイズを増やしてください。
- **問題タイプ**: 二項分類と多項分類
- **グラフ値**: 時間フレーム内の最後の値
- **使用可能な指標の詳細**: 混同行列


## 正解率について
{: #acc-understand}

正解率は、アルゴリズムのタイプに応じてその意味が異なります。

- *多項分類*: 正解率は、クラスが全体として正確に予測された回数を測定してから、その値をデータ・ポイント数で正規化することによって求められます。 詳しくは、Apache Spark 資料の [Multi-class classification](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#multiclass-classification){: external} を参照してください。

- *二項分類*: 二項分類アルゴリズムでは、正解率は ROC 曲線の下側の面積として測定されます。 詳しくは、Apache Spark 資料の [Binary classification](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#binary-classification){: external} を参照してください。

- *回帰*: 回帰アルゴリズムは、決定係数 (R2) を使用して測定されます。 詳しくは、Apache Spark 資料の [Regression model evaluation](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#regression-model-evaluation){: external} を参照してください。

### 処理の流れ
{: #acc-works}

以下の例に示すように {{site.data.keyword.aios_short}} UI により、または [Python クライアント](http://ai-openscale-python-client.mybluemix.net/#feedbacklogging){: external}を使用して、あるいは [Rest API](https://cloud.ibm.com/apidocs/ai-openscale#post-feedback-payload){: external} により、手動でラベル付けされたフィードバック・データを追加する必要があります。

正解率モニタリングの制約事項については、[サポートされるフレームワーク](/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-fram)を参照してください。

### バイアス緩和済みの正解率
{: #acc-debias-view}

サポートするデータがある場合は、元のモデルとバイアス緩和済みのモデルの両方に基づいて正解率が計算されます。 {{site.data.keyword.aios_full_notm}} はバイアス緩和済みの出力に関する正解率を計算し、ペイロード・ロギング・テーブル内に追加列として保管します。

![モデルの視覚化、オリジナルのモデルとバイアス緩和済みのモデルの両方に関する正解率が計算されて表示される](images/debiased-accuracy.png)
