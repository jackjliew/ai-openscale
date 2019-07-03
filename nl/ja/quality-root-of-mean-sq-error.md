---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

# 平均二乗誤差平方根 ![ベータ・タグ](images/beta.png)
{: #supqualdets_squ_errors_mean}

平均二乗誤差平方根 (RMSE) ビューは、モデルの予測値と観測値の差を示します。
{: shortdesc}

## 一目でわかる平均二乗誤差平方根
{: #anlz_metrics_supqualdets_squ_errors_mean}

- **説明**: モデル予測とターゲット値の差を二乗した平均の平方根
- **デフォルトのしきい値**: 上限 = 80%
- **デフォルトの推奨**:
   - **上昇傾向**: 上昇傾向は、指標が悪化していることを示します。 フィードバック・データと訓練データの差異が明らかに広がっています。
   - **下降傾向**: 下降傾向は、指標が向上していることを示します。 これは、モデルの再訓練の効果が出ていることを意味します。
   - **不規則または不定期変化**: 不規則変化または不定期変化は、フィードバック・データが各評価で一貫性がないことを示します。 モデル性能モニタリングの最小サンプル・サイズを増やしてください。
- **問題タイプ**: 回帰
- **グラフ値**: 時間フレーム内の最後の値
- **使用可能な指標の詳細**: なし

## 表示内容についての解釈
{: #supqualdets_squ_errors_mean-display}

![平均二乗誤差平方根グラフが表示されています。](images/xxxx.png)

## 計算
{: #supqualdets_squ_errors_mean-math}

平均二乗誤差平方根は、(予測値から観測値を減算した値) の平方の平均の平方根です。

```
          ___________________________________________________________
RMSE  =  √(予測値 - 観測値)*(予測値 - 観測値)
```
