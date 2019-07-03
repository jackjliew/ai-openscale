---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, Area under PR

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

# PR 曲線下面積 ![ベータ・タグ](images/beta.png)
{: #quality-area-pr}

適合率再現率 (PR) 曲線下面積とは、適合率と再現率の曲線の下の面積で、クラスが非常に偏っている場合に役立つことがあります。
{: shortdesc}

## 一目でわかる PR 曲線下面積
{: #quality-area-pr-glance}

- **説明**: 適合率と再現率を示す曲線の下の領域です
- **デフォルトのしきい値**: 下限 = 80%
- **デフォルトの推奨**:
   - **上昇傾向**: 上昇傾向は、指標が向上していることを示します。 これは、モデルの再訓練の効果が出ていることを意味します。
   - **下降傾向**: 下降傾向は、指標が悪化していることを示します。 フィードバック・データと訓練データの差異が明らかに広がっています。
   - **不規則または不定期変化**: 不規則変化または不定期変化は、フィードバック・データが各評価で一貫性がないことを示します。 モデル性能モニタリングの最小サンプル・サイズを増やしてください。
- **問題タイプ**: 二項分類
- **グラフ値**: 時間フレーム内の最後の値
- **使用可能な指標の詳細**: 混同行列

## 表示内容についての解釈
{: #quality-area-pr-display}

![下降傾向の指標が示されている PR 曲線下面積が表示されています](images/quality-area-under-pr.png)


## 計算
{: #quality-area-pr-math}

適合率再現率曲線下面積は、`適合率 + 再現率` の合計です。

適合率 (P) は、真陽性 (Tp) と偽陽性 (Fp) の合計数に対する真陽性の数と定義されます。

```
               真陽性の数
適合率 =   ______________________________________________________

              (真陽性の数 + 偽陽性の数)
```

再現率 (R) は、真陽性 (Tp) と偽陰性 (Fn) の合計数に対する真陽性の数と定義されます。

```
            真陽性の数
再現率 =   ______________________________________________________

           (真陽性の数 + 偽陰性の数)
```
