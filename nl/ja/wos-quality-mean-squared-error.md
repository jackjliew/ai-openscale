---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Mean squared error

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

# 平均二乗誤差 (MSE) ![ベータ・タグ](images/beta.png)
{: #quality_squerror}

平均二乗誤差 (MSE) は、モデル予測とターゲット値の差の二乗の平均です。 推定量の質を表す指標として使用できます。
{: shortdesc}

## 一目でわかる平均二乗誤差 (MSE)
{: #quality_squerror-glance}

- **説明**: モデル予測とターゲット値の差を二乗した平均
- **デフォルトのしきい値**: 上限 = 80%
- **デフォルトの推奨**:
   - **上昇傾向**: 上昇傾向は、指標が悪化していることを示します。 フィードバック・データと訓練データの差異が明らかに広がっています。
   - **下降傾向**: 下降傾向は、指標が向上していることを示します。 これは、モデルの再訓練の効果が出ていることを意味します。
   - **不規則または不定期変化**: 不規則変化または不定期変化は、フィードバック・データが各評価で一貫性がないことを示します。 モデル性能モニタリングの最小サンプル・サイズを増やしてください。
- **問題タイプ**: 回帰
- **グラフ値**: 時間フレーム内の最後の値
- **使用可能な指標の詳細**: なし

## 表示内容についての解釈
{: #quality_squerror-display}

![平均二乗誤差 (MSE) グラフが表示されています。](images/xxxx.png)

## 計算
{: #quality_squerror-math}

最も簡単な形式の平均二乗誤差 (MSE) は次の数式で表されます。

```
                         SUM  (Yi - ^Yi) * (Yi - ^Yi)
平均二乗誤差  =  ____________________________

                             誤差数
```
