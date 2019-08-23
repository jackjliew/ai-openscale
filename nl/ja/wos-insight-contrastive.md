---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, monitoring, charts, de-biasing, bias, accuracy

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

# 対比的説明では陽性所見と陰性所見が使用される
{: #ie-pp-pn}

対比的説明では、{{site.data.keyword.aios_short}} は陽性所見を表す値と陰性所見を表す値を表示します。
{: shortdesc}

- 関連する陽性とは、あるものの正体を決定するために重要な所見のことです。
- 関連する陰性とは、所見がないことであり、所見がないことが重要な意味を持つものです。

{{site.data.keyword.aios_short}} では、関連する陽性は常に表示されます。一方、関連する陰性は、表示するものがない場合があります。 その場合は、その特徴量の値が既に中央値にあるか、中央値から離れた値を移動しても予測が変わらなかったかのどちらかです。

これについての理解を深めるには、{{site.data.keyword.aios_short}} が、関連する陰性の値を計算するときに、すべての特徴量の中央値から離れた値を変更することを考慮してください。 関連する陰性の場合、これは、中央値から最も離れた特徴量の値を意味します。 データ・ポイントの値が既に中央値にある場合、または中央値から離れた値を変更しても予測が変わらなかった場合は、関連する陰性として表示するものがありません。 関連する陽性の場合は、{{site.data.keyword.aios_short}} は、予測が変わらないようにして中央値に対する特徴量値の最大の変化を検出します。 実際には、これは、トランザクションを説明するための関連する陽性がほぼ常に存在することを意味します。

