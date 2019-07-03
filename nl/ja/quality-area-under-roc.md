---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, Area under ROC

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

# ROC 曲線下面積 ![ベータ・タグ](images/beta.png)
{: #quality_roc}

受信者操作特性曲線下面積は、再現率と偽陽性率を示す曲線の下の領域です。フォールアウト率に対する感度を計算します。
{: shortdesc}

## 一目でわかる ROC 曲線下面積
{: #quality_roc-glance}

- **説明**: 再現率と偽陽性の比率を示す曲線の下の面積です
- **デフォルトのしきい値**: 下限 = 80%
- **デフォルトの推奨**:
   - **上昇傾向**: 上昇傾向は、指標が向上していることを示します。 これは、モデルの再訓練の効果が出ていることを意味します。
   - **下降傾向**: 下降傾向は、指標が悪化していることを示します。 フィードバック・データと訓練データの差異が明らかに広がっています。
   - **不規則または不定期変化**: 不規則変化または不定期変化は、フィードバック・データが各評価で一貫性がないことを示します。 モデル性能モニタリングの最小サンプル・サイズを増やしてください。
- **問題タイプ**: 二項分類
- **グラフ値**: 時間フレーム内の最後の値
- **使用可能な指標の詳細**: 混同行列

## 表示内容についての解釈
{: #quality_roc-display}

![ROC 曲線下面積グラフが表示されています。](images/quality-area-under-roc.png)

## 計算
{: #quality_roc-math}

ROC 曲線下面積は、しきい値 `T` に関して、`真陽性率`と`偽陽性率`を対比してパラメーター的にプロットします。

