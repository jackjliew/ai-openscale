---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: databases, connections, scoring, requests

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

# 評価要求の送信
{: #cdb-score}

モニターを構成するには、{{site.data.keyword.aios_short}} でモニター対象となるデータのログ記録を開始するために、ユーザーから評価ペイロードを送信する必要があります。

- {{site.data.keyword.pm_full}} でデプロイされたモデルの場合、デプロイメントを評価するだけです。{{site.data.keyword.pm_short}} が、{{site.data.keyword.aios_short}} に自動的に評価ペイロードを送信します。 
- その他の機械学習エンジン (Microsoft Azure や Amazon SageMaker など) やカスタムの機械学習エンジンを使用している場合は、ペイロード・ロギング API を使用して評価ペイロードを送信する必要があります。詳しくは、[{{site.data.keyword.pm_full}} サービス以外のインスタンスのペイロード・ロギング](/docs/services/ai-openscale?topic=ai-openscale-cml-connect)を参照してください。

{{site.data.keyword.pm_full}} でデプロイしたモデルは自動的に {{site.data.keyword.aios_short}} で評価されるので、{{site.data.keyword.pm_short}} でデプロイしたモデルしかない場合は、この手順が完了したことを示すチェック・マークが**「モニタリング準備完了」**列に表示されます。
{: note}

## ペイロード・ロギングのための手順
{: #cdb-score-apisteps}

1. デプロイメントを選択します。以下の例では、**Fraud Detector** がデプロイメントです。
2. `cURL` と `Python` のどちらのコードを使用するかを、`「cURL」`タブまたは`「Python」`タブをクリックして選択します。
3. **「クリップボードにコピー」**をクリックしてコピーしたものを貼り付け、モデル・デプロイメントの要求と応答のデータをログに記録します。詳しくは、[{{site.data.keyword.pm_full}} サービス以外のインスタンスのペイロード・ロギング](/docs/services/ai-openscale?topic=ai-openscale-cml-connect)を参照してください。

提供されている値は単なる例であるため、コード・スニペット内のフィールドと値を、実際の値に置換する必要があります。
{: important}

![データベースの選択](images/config-send-scoring.png)

ペイロード・ロギングを実行すると、選択したデプロイメントの「モニタリング準備完了」列にチェック・マークが表示されます。**「モニターの構成」**をクリックして先に進みます。

## 評価要求数について
{: #cdb-score-capacity}

評価要求は {{site.data.keyword.aios_short}} 処理の不可欠な部分です。評価するトランザクション・レコードをモデルに送信するたびに、{{site.data.keyword.aios_short}} サービスで摂動を実行して説明を生成するための追加処理が発生します。

- 表形式、テキスト、画像のモデルでは、以下のベースライン要求によってデータ・ポイントが生成されます。

   - 1 個の評価要求で 5000 個のデータ・ポイントが生成されます。

- 表形式の分類モデルの場合のみ、対比的説明のために追加で実行される評価要求があります。上記のベースライン要求に次の要求が追加されます。

   - 100 個の評価要求で、要求 1 つにつき 51 個の追加のデータ・ポイントが生成されます。
   - 101 個の評価要求で、要求 1 つにつき 1 個の追加のデータ・ポイントが生成されます。


## 次のステップ
{: #cdb-score-next-steps-scoringreq}

[モニタリングの構成](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-mo-config)。
