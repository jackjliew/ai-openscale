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

# 再現率
{: #quality_recall}

再現率は、肯定クラスの予測の正解率です。
{: shortdesc}

## 一目でわかる再現率
{: #quality_recall-glance}

- **説明**: 肯定クラスでの正しい予測の比率です
- **デフォルトのしきい値**: 下限 = 80%
- **デフォルトの推奨**:
   - **上昇傾向**: 上昇傾向は、指標が向上していることを示します。 これは、モデルの再訓練の効果が出ていることを意味します。
   - **下降傾向**: 下降傾向は、指標が悪化していることを示します。 フィードバック・データと訓練データの差異が明らかに広がっています。
   - **不規則または不定期変化**: 不規則変化または不定期変化は、フィードバック・データが各評価で一貫性がないことを示します。 モデル性能モニタリングの最小サンプル・サイズを増やしてください。
- **問題タイプ**: 二項分類
- **グラフ値**: 時間フレーム内の最後の値
- **使用可能な指標の詳細**: 混同行列

## 「再現率」指標の表示の解釈
{: #quality_recall-display}

![再現率グラフが表示されています。](images/quality-recall.png)

### 公平性スコア
{: #quality_recall-display-fairness-score}

「再現率」指標の場合、次の公平性スコアが表示されます。 

![再現率スコアのパーセンテージが表示されています](images/wos-quality-recall-score.png)

### スケジュール
{: #quality_recall-display-schedule}

**「スケジュール」**ペインには**「最新の評価」**と**「次の評価」**の時刻が表示されます。品質指標は毎時間評価されます。評価を強制的に実行するには、**「今すぐ品質を評価」**をクリックします。フィードバックを追加するには、**「フィードバック・データの追加」**をクリックします。

![スケジュール・ペインが表示されています。このペインには、最新の評価の時刻と次の評価の時刻が表示されています。](images/wos-quality-schedule.png)


### 推奨
{: #quality_recall-display-recommendations}

グラフを解釈できるように、**「推奨」**ペインには、モデルの有効性の向上を示す傾向や悪化を示す傾向が表示されます。

![推奨ペインが表示されています。](images/wos-quality-positive-recommendation.png)




## 計算
{: #quality_recall-math}

再現率 (R) は、真陽性 (Tp) と偽陰性 (Fn) の合計数に対する真陽性の数と定義されます。

```
                       真陽性の数
再現率 =   ______________________________________________________

           (真陽性の数 + 偽陰性の数)
```
