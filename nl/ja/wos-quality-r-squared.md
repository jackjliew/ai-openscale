---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, R squared

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

# R2 (決定係数) ![ベータ・タグ](images/beta.png)
{: #quality_r_squared}

R2 (決定係数) は、ターゲット分散と、ターゲット分散に対する予測誤差の分散の差異の比率です。 モデルの作成に使用したデータが、どれほど回帰に適合しているデータかがわかります。
{: shortdesc}

## 一目でわかる R2 (決定係数)
{: #quality_r_squared-glance}

- **説明**: ターゲット分散と、ターゲット分散に対する予測誤差の間の差異の比率です
- **デフォルトのしきい値**: 下限 = 80%
- **デフォルトの推奨**:
   - **上昇傾向**: 上昇傾向は、指標が向上していることを示します。 これは、モデルの再訓練の効果が出ていることを意味します。
   - **下降傾向**: 下降傾向は、指標が悪化していることを示します。 フィードバック・データと訓練データの差異が明らかに広がっています。
   - **不規則または不定期変化**: 不規則変化または不定期変化は、フィードバック・データが各評価で一貫性がないことを示します。 モデル性能モニタリングの最小サンプル・サイズを増やしてください。
- **問題タイプ**: 回帰
- **グラフ値**: 時間フレーム内の最後の値
- **使用可能な指標の詳細**: なし

## 表示内容についての解釈
{: #quality_r_squared-display}

![R2 (決定係数) グラフが表示されています。](images/xxxx.png)

## 計算
{: #quality_r_squared-math}

R2 (決定係数) 指標は、次の数式で定義されます。

```
                  説明された分散
R2 (決定係数) = 1 -  _____________________

                    全体の分散
```
