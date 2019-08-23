---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, fairness monitor, payload, perturbation, training data, debiased, Logarithmic loss

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

# 対数損失
{: #quality_log_loss}

対数損失は、ターゲット・クラスの確率 (確信度) の対数の平均です。 これは、予想対数尤度とも呼ばれ、モデルのパフォーマンスを表す有効な指標です。
{: shortdesc}

## 一目でわかる対数損失
{: #quality_log_loss-glance}

- **説明**: ターゲット・クラス確率の対数の平均 (確信度)。 これは、予想対数尤度とも呼ばれます。
- **デフォルトのしきい値**: 下限 = 80%
- **デフォルトの推奨**:
   - **上昇傾向**: 上昇傾向は、指標が悪化していることを示します。 フィードバック・データと訓練データの差異が明らかに広がっています。
   - **下降傾向**: 下降傾向は、指標が向上していることを示します。 これは、モデルの再訓練の効果が出ていることを意味します。
   - **不規則または不定期変化**: 不規則変化または不定期変化は、フィードバック・データが各評価で一貫性がないことを示します。 モデル性能モニタリングの最小サンプル・サイズを増やしてください。
- **問題タイプ**: 二項分類と多項分類
- **グラフ値**: 時間フレーム内の最後の値
- **使用可能な指標の詳細**: なし

## 表示内容についての解釈
{: #quality_log_loss-display}

![対数損失が表示されています](images/quality-log-loss.png)

### 公平性スコア
{: #quality_log_loss-display-fairness-score}

「対数損失」指標の場合、次の公平性スコアが表示されます。 

![再現率スコアのパーセンテージが表示されています](images/wos-quality-logloss-score.png)

### スケジュール
{: #quality_log_loss-display-schedule}

**「スケジュール」**ペインには**「最新の評価」**と**「次の評価」**の時刻が表示されます。品質指標は毎時間評価されます。評価を強制的に実行するには、**「今すぐ品質を評価」**をクリックします。フィードバックを追加するには、**「フィードバック・データの追加」**をクリックします。

![スケジュール・ペインが表示されています。このペインには、最新の評価の時刻と次の評価の時刻が表示されています。](images/wos-quality-schedule.png)


### 推奨
{: #quality_log_loss-display-recommendations}

グラフを解釈できるように、**「推奨」**ペインには、モデルの有効性の向上を示す傾向や悪化を示す傾向が表示されます。

![推奨ペインが表示されています。](images/wos-quality-negative-recommendation.png)



## 計算
{: #quality_log_loss-math}

バイナリー・モデルの場合、対数は以下の数式で計算されます。

```
-(y log(p) + (1-y)log(1-p))
```

p は真ラベル、y は予測される確率です

多項モデルの場合、対数損失は以下の数式で計算されます。

```
  M
-SUM Yo,c log(Po,c)
 c=1 
```

M > 2、p は真ラベル、y は予測される確率です
