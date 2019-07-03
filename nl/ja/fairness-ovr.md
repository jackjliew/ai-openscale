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

# 公平性指標の概要
{: #anlz_metrics_fairness}

{{site.data.keyword.aios_full}} の公平性モニタリングを使用して、モデルによって生成された結果が、モニター対象グループにとって公平な結果かどうかを判別できます。公平性モニタリングを有効にすると、デフォルトでは 1 時間ごとに指標のセットが生成されます。 これらの指標は、**「今すぐ品質を評価」**ボタンをクリックするか、Python クライアントを使用して、オンデマンドで生成できます。{: shortdesc}

{{site.data.keyword.aios_short}} は、モデル内に既知の保護属性が存在するかどうかを自動的に検知します。保護属性を検知すると、{{site.data.keyword.aios_short}} は、潜在的にセンシティブな属性についてのバイアスを稼働環境で確実に追跡するために、存在している各属性についてバイアス・モニターを構成するように自動的に推奨します。 

現在、{{site.data.keyword.aios_short}} が検出してモニターを推奨するのは、以下の保護属性です。 

- 性別
- 人種
- 婚姻状態
- 年齢
- 郵便番号

{{site.data.keyword.aios_short}} は、保護属性を検出するだけでなく、各属性のどの値をモニター対象値および参照値に設定すべきかについての推奨情報を生成します。例えば、{{site.data.keyword.aios_short}} は、「性別」属性の「女性」と「ノンバイナリー」をモニター対象値に、「男性」を参照値にしてバイアス・モニターを構成することを推奨します。推奨された項目を変更したい場合は、バイアス構成パネルで編集できます。 

推奨されたバイアス・モニターを利用すれば、構成を素早く完了して、センシティブな属性に対する AI モデルの公平性を確実に検査することができます。規制当局がアルゴリズムのバイアスに目を光らせるようになった今、組織のモデルがどのように機能しているのか、また、特定のグループにとって不公平な結果を生成していないかについて、組織が明確に把握することがますます重要になっています。 

公平性指標は、以下の情報に基づいて計算されます。

- ペイロード・データの評価

適切なモニタリングのために、すべての評価要求は {{site.data.keyword.aios_short}} でログ記録する必要もあります。 {{site.data.keyword.pm_full}} エンジンの場合、ペイロード・データのロギングは自動化されています。

その他の機械学習エンジンの場合、Python クライアントか REST API を使用してペイロード・データを提供できます。

{{site.data.keyword.pm_full}} 以外の機械学習エンジンの場合、公平性モニタリングにより、モニター対象のデプロイメントに関する追加の評価要求が作成されます。
{: note}

{{site.data.keyword.aios_short}} ダッシュボードで、すべての指標値を経時的に確認できます。

![設定したしきい値を下回るドリフトが表示された公平性指標グラフ](images/fairness_metrics_001.png)

以下のように、好ましい結果と好ましくない結果などの、関連した詳細情報を検討できます。

![公平性の詳細](images/fairness_metrics_002.png)

以下のように、詳細トランザクションを表示できます。

![トランザクションのリストが表示された、公平性に関するグラフ](images/fairness_metrics_003.png)

推奨されるバイアス緩和済みの評価エンドポイントを表示できます。

![バイアス緩和済みの評価エンドポイントの詳細](images/fairness_metrics_004.png)

### サポートされている公平性指標
{: #anlz_metrics_supfairmets}

以下の公平性指標が {{site.data.keyword.aios_short}} によってサポートされています。

- [グループに関する公平性](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_group)

以下の保護属性が {{site.data.keyword.aios_short}} によってサポートされています。 

- [性別](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-sex)
- [人種](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-ethnicity)
- [婚姻状態](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-marital)
- [年齢](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-age)
- [郵便番号](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-zip)


### サポートされている公平性の詳細
{: #anlz_metrics_supfairdets}

以下の公平性指標に関する詳細が {{site.data.keyword.aios_short}} によってサポートされています。

- グループごとの好ましい割合
- すべての公平性グループに関する公平性の平均

```
                          (モニター対象グループにおける好ましい結果の割合
差別的効果率 =  ____________________________________________
                          (参照グループにおける好ましい結果の割合)
```

- モニター対象グループごとのデータの分布
- ペイロード・データの分布
