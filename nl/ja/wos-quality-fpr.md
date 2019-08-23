---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, False positive rate, fpr

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

# 偽陽性率 (FPR)
{: #quality_fpr_false}

偽陽性率は、肯定クラスの予測の不正解率です。
{: shortdesc}

## 偽陽性率 (FPR)
{: #quality_fpr_false-glance}

- **説明**: 肯定クラスでの正しくない予測の比率です
- **デフォルトのしきい値**: 下限 = 80%
- **デフォルトの推奨**:
   - **上昇傾向**: 上昇傾向は、指標が悪化していることを示します。 フィードバック・データと訓練データの差異が明らかに広がっています。
   - **下降傾向**: 下降傾向は、指標が向上していることを示します。 これは、モデルの再訓練の効果が出ていることを意味します。
   - **不規則または不定期変化**: 不規則変化または不定期変化は、フィードバック・データが各評価で一貫性がないことを示します。 モデル性能モニタリングの最小サンプル・サイズを増やしてください。
- **問題タイプ**: 二項分類
- **グラフ値**: 時間フレーム内の最後の値
- **使用可能な指標の詳細**: 混同行列

## 表示内容についての解釈
{: #quality_fpr_false-display}

![偽陽性率グラフが表示されています。](images/quality-fpr.png)

## 計算
{: #quality_fpr_false-math}

偽陽性率は、偽陽性の合計数を、偽陽性と真陰性の合計数で除算して算出します。

```
                        偽陽性の数
偽陽性率 =  ______________________________________________________

                       (偽陽性の数 + 真陰性の数)
```
