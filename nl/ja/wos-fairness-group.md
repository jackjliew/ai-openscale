---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Fairness for a group, sex, age, race

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

# グループに関する公平性
{: #quality_group}

グループに関する公平性という指標は、あるグループに対して別のグループよりも好ましい結果を出すモデルの傾向を表すことができます。 グループとしては、年齢、性別、人種などのグループがあります。
{: shortdesc}

## グループに関する公平性の概要
{: #quality_group-glance}

- **説明**: モデルがあるグループに対して別のグループよりも好ましい結果を出す傾向です。
- **デフォルトのしきい値**: 下限 = 80%
- **デフォルトの推奨**: デプロイ済みモデルからバイアス緩和済みの応答を受信するために、ビジネス・アプリケーションで使用できるバイアス緩和済みの評価エンドポイント。
- **問題タイプ**: すべて
- **データ・タイプ**: 構造化
- **グラフ値**: 時間フレーム内の最後の値
- **使用可能な指標の詳細**: あり

## 保護属性
{: #quality_group-atts}

{{site.data.keyword.aios_short}} は、モデル内に既知の保護属性が存在するかどうかを自動的に検知します。 保護属性を検知すると、{{site.data.keyword.aios_short}} は、この潜在的にセンシティブな属性についてのバイアスを稼働環境で確実に追跡するために、存在している各属性についてバイアス・モニターを構成するように自動的に推奨します。 

### 性別
{: #quality_group-sex}

{{site.data.keyword.aios_short}} は、**性別**属性について、`女性`と`ノンバイナリー`をモニター対象値に、`男性`を参照値にしてバイアス・モニターを構成することを推奨します。 

### 人種
{: #quality_group-ethnicity}

{{site.data.keyword.aios_short}} は、**人種**属性について、`白色人種`を参照値に、その他の人種をモニター対象値にしてバイアス・モニターを構成することを推奨します。

### 婚姻状態
{: #quality_group-marital}

{{site.data.keyword.aios_short}} は、**婚姻状態**の属性について、`既婚`を参照値に、`独身`をモニター対象値にしてバイアス・モニターを構成することを推奨します。

### 年齢
{: #quality_group-age}

{{site.data.keyword.aios_short}} は、**年齢**属性について、特定の範囲の年齢に対してバイアス緩和を適用するバイアス・モニターを構成することを推奨します。

### 郵便番号
{: #quality_group-zip}

{{site.data.keyword.aios_short}} は、**郵便番号**属性について、個々の郵便番号を評価するバイアス・モニターを構成することを推奨します。

## 表示内容についての解釈
{: #quality_group-display}

### グループの公平性スコア
{: #quality_group-display-fairnessscore}



### モニタリング対象グループ
{: #quality_group-display-monitoredgroups}



### スケジュール
{: #quality_group-display-schedule}

**「スケジュール」**ペインの表示内容: 



