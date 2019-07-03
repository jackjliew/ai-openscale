---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, weighted recal

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

# 加重再現率 ![ベータ・タグ](images/beta.png)
{: #quality_weighted_recall}

加重再現率は、クラス確率に相当する値で重みづけした再現率の平均です。
{: shortdesc}

## 一目でわかる加重再現率
{: #quality_weighted_recall-glance}

- **説明**: 加重再現率の加重平均は、クラス確率と同等です
- **デフォルトのしきい値**: 下限 = 80%
- **デフォルトの推奨**:
   - **上昇傾向**: 上昇傾向は、指標が向上していることを示します。 これは、モデルの再訓練の効果が出ていることを意味します。
   - **下降傾向**: 下降傾向は、指標が悪化していることを示します。 フィードバック・データと訓練データの差異が明らかに広がっています。
   - **不規則または不定期変化**: 不規則変化または不定期変化は、フィードバック・データが各評価で一貫性がないことを示します。 モデル性能モニタリングの最小サンプル・サイズを増やしてください。
- **問題タイプ**: 多項分類
- **グラフ値**: 時間フレーム内の最後の値
- **使用可能な指標の詳細**: 混同行列

## 表示内容についての解釈
{: #quality_weighted_recall-display}

![加重再現率グラフが表示されています。](images/quality-recall.png)

## 計算
{: #quality_weighted_recall-math}

加重再現率 (wR) は、重みづけデータで使用する真陽性 (Tp) と偽陰性 (Fn) の合計数に対する真陽性の数と定義されます。 

```
            真陽性の数
再現率 =   ______________________________________________________

           (真陽性の数 + 偽陰性の数)
```
