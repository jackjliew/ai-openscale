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

# 分類モデルの説明
{: #ie-class}

この説明性の例は、保険金請求を承認または拒否する二項分類モデルを示すものです。 この事例の最終結果が `DENIED` (拒否) になった原因となるプラス要因とマイナス要因を読み取ることができます。
{: shortdesc}

特徴量 *POLICY AGE* の値が `<ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling serviceyear` であることが、モデルで DENIED の結果を決定する上で最大の影響がありました。 この結果の原因となった他の特徴量には、*CLAIM FREQUENCY* (`High`) および *AGE* (`18`) があり、また、ほんのわずかな影響ですが *CAR VALUE* (`$50,000`) がありました。

![拒否された保険金請求と承認された保険金請求の詳細が表示されている説明性二項分類](images/insight-explain-binary.png)

グラフは、トランザクションの結果を決定する最も有意な要因を示す上で役立ちますが、分類モデルには詳細説明も含まれる場合があります。これについては、`承認結果を導く最小の変更 (Minimum changes for Approved outcome)` および`この結果を導く最小の変更 (Minimum changes for this outcome)` のセクションで詳しく説明されています。

回帰、イメージ、および非構造化テキストのモデルでは、詳細説明は提供されません。
{: note}

`承認結果を導く最小の変更 (Minimum changes for Approved outcome)` は、特徴量の値がこのセクションにリストされている値に変更された場合に、モデルの予測が変わることを示します。

同様に、`この結果を導く最小の変更 (Minimum changes for this outcome)` は、特徴量の値がこのセクションにリストされた値に変更されても、モデルの予測は変わらないことを示します。

このため、これらの 2 つの値は、説明が生成されたデータ・ポイントの近辺でのモデルの振る舞いを示します。

![結果の変更に必要な最小の変更に関する詳細が表示されている説明性二項分類](images/insight-explain-binary2.png)
