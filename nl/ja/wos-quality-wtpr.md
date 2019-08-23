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

# 加重真陽性率 (wTPR)
{: #quality-wtpr}

加重真陽性率は、クラス確率に相当する値で重みづけしたクラス TPR の平均です。
{: shortdesc)

## 一目でわかる加重真陽性率 (wTPR)
{: #quality-wtpr-glance}

- **説明**: 加重クラス TPR の加重平均は、クラス確率と同等です
- **デフォルトのしきい値**: 下限 = 80%
- **デフォルトの推奨**:
   - **上昇傾向**: 上昇傾向は、指標が向上していることを示します。 これは、モデルの再訓練の効果が出ていることを意味します。
   - **下降傾向**: 下降傾向は、指標が悪化していることを示します。 フィードバック・データと訓練データの差異が明らかに広がっています。
   - **不規則または不定期変化**: 不規則変化または不定期変化は、フィードバック・データが各評価で一貫性がないことを示します。 モデル性能モニタリングの最小サンプル・サイズを増やしてください。
- **問題タイプ**: 多項分類
- **グラフ値**: 時間フレーム内の最後の値
- **使用可能な指標の詳細**: 混同行列

## 表示内容についての解釈
{: #quality-wtpr-display}

![加重真陽性率が表示されています](images/quality-tpr.png)

## 計算
{: #quality-wtpr-math}

真陽性率は、以下の数式で計算されます。

```
                  真陽性の数
TPR =  _________________________________________________________

        (真陽性の数 + 偽陰性の数)
```
