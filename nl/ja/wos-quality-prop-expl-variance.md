---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Proportion explained variance

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

# 分散説明率
{: #quality_var}

分散説明率は、説明された分散とターゲット分散の比率です。 説明された分散とは、ターゲット分散と予測誤差の分散の間の差異です。
{: shortdesc}

## 一目でわかる分散説明率
{: #quality_var-glance}

- **説明**: 分散説明率とは、説明された差異とターゲット差異の比率を表します。 説明された差異とは、ターゲット差異と予測誤差の差異の間の差異です。
- **デフォルトのしきい値**: 下限 = 80%
- **デフォルトの推奨**:
   - **上昇傾向**: 上昇傾向は、指標が向上していることを示します。 これは、モデルの再訓練の効果が出ていることを意味します。
   - **下降傾向**: 下降傾向は、指標が悪化していることを示します。 フィードバック・データと訓練データの差異が明らかに広がっています。
   - **不規則または不定期変化**: 不規則変化または不定期変化は、フィードバック・データが各評価で一貫性がないことを示します。 モデル性能モニタリングの最小サンプル・サイズを増やしてください。
- **問題タイプ**: 回帰
- **グラフ値**: 時間フレーム内の最後の値
- **使用可能な指標の詳細**: なし

## 表示内容についての解釈
{: #quality_var-display}

![分散説明率グラフが表示されています。](images/xxxx.png)

## 計算
{: #quality_var-math}

分散説明率は、数値の平均を求め、各数値について、平均を減算した結果を二乗します。 その後、それらの平方を計算します。

```
                                  グループ間の平方和
分散説明率 =  ________________________________

                                      全体の平方和
```
