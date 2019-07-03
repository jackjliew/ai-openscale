---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, precision

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

# 適合率 ![ベータ・タグ](images/beta.png)
{: #quality_precision}

適合率は、肯定クラスの予測の正解率です。
{: shortdesc}

## 一目でわかる適合率
{: #quality_precision-glance}

- **説明**: 肯定クラスの予測での正しい予測の比率です
- **デフォルトのしきい値**: 下限 = 80%
- **デフォルトの推奨**:
   - **上昇傾向**: 上昇傾向は、指標が向上していることを示します。 これは、モデルの再訓練の効果が出ていることを意味します。
   - **下降傾向**: 下降傾向は、指標が悪化していることを示します。 フィードバック・データと訓練データの差異が明らかに広がっています。
   - **不規則または不定期変化**: 不規則変化または不定期変化は、フィードバック・データが各評価で一貫性がないことを示します。 モデル性能モニタリングの最小サンプル・サイズを増やしてください。
- **問題タイプ**: 二項分類
- **グラフ値**: 時間フレーム内の最後の値
- **使用可能な指標の詳細**: 混同行列

## 表示内容についての解釈
{: #quality_precision-display}

![適合率グラフが表示されています。](images/quality-precision.png)

## 計算
{: #quality_precision-math}

適合率 (P) は、真陽性 (Tp) と偽陽性 (Fp) の合計数に対する真陽性の数と定義されます。


```
             真陽性の数
適合率 =  __________________________________________________________

             (真陽性の数 + 偽陽性の数)
```
