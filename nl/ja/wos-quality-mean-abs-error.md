---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Mean absolute error

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

# 平均絶対誤差 (MAE) ![ベータ・タグ](images/beta.png)
{: #quality_abserror}

平均絶対誤差 (MAE) は、モデル予測とターゲット値の絶対差の平均です。
{: shortdesc}

## 一目でわかる平均絶対誤差 (MAE)
{: #quality_abserror-glance}

- **説明**: モデル予測とターゲット値の絶対差の平均
- **デフォルトのしきい値**: 上限 = 80%
- **デフォルトの推奨**:
   - **上昇傾向**: 上昇傾向は、指標が悪化していることを示します。 フィードバック・データと訓練データの差異が明らかに広がっています。
   - **下降傾向**: 下降傾向は、指標が向上していることを示します。 これは、モデルの再訓練の効果が出ていることを意味します。
   - **不規則または不定期変化**: 不規則変化または不定期変化は、フィードバック・データが各評価で一貫性がないことを示します。 モデル性能モニタリングの最小サンプル・サイズを増やしてください。
- **問題タイプ**: 回帰
- **グラフ値**: 時間フレーム内の最後の値
- **使用可能な指標の詳細**: なし

## 表示内容についての解釈
{: #quality_abserror-display}

![平均絶対誤差 (MAE) グラフが表示されています。](images/xxxx.png)

## 計算
{: #quality_abserror-math}

平均絶対誤差 (MAE) は、すべての絶対誤差を合計し、その合計を誤差数で除算して算出されます。

```
                         SUM  | Yi - Xi |
平均絶対誤差 (MAE) =  ____________________

                          誤差数
```
