---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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

- {{site.data.keyword.pm_full}} でデプロイされたモデルの場合、モデルは自動的に {{site.data.keyword.aios_short}} に送信されます。自動的に送信される評価要求の場合、この作業を行う必要はなく、コード・スニペットは表示されません。
- その他の機械学習エンジン (Microsoft Azure、Amazon SageMaker、カスタムの機械学習エンジンなど) を使用している場合は、ペイロード・ロギング API を使用して評価ペイロードを送信する必要があります。 このため、cURL 形式または Python 形式のコード・スニペットを使用してください。このコード・スニペットは、「ペイロードのロギング」ページから取得できます。詳しくは、[{{site.data.keyword.pm_full}} サービス以外のインスタンスのペイロード・ロギング](/docs/services/ai-openscale?topic=ai-openscale-cml-connect)を参照してください。

## ペイロード・ロギングのための手順
{: #cdb-score-apisteps}

1. {{site.data.keyword.aios_short}} ダッシュボードでデプロイメント・タイルをクリックします。
2. **「モニタリングの構成」**をクリックします。 
3. ナビゲーション・ペインで**「ペイロードのロギング」**をクリックします。
2. `cURL` と `Python` のどちらのコードを使用するかを、`「cURL」`タブまたは`「Python」`タブをクリックして選択します。
3. **「クリップボードにコピー」**をクリックしてコピーしたものを貼り付け、モデル・デプロイメントの要求と応答のデータをログに記録します。 詳しくは、[{{site.data.keyword.pm_full}} サービス以外のインスタンスのペイロード・ロギング](/docs/services/ai-openscale?topic=ai-openscale-cml-connect)を参照してください。

提供されている値は単なる例であるため、コード・スニペット内のフィールドと値を、実際の値に置換する必要があります。
{: important}

![データベースの選択](images/config-send-scoring.png)

ペイロード・ロギングを実行すると、選択したデプロイメントの**「モニタリング準備完了」**列にチェック・マークが表示されます。 **「モニターの構成」**をクリックして先に進みます。

## 評価要求数について
{: #cdb-score-capacity}

評価要求は {{site.data.keyword.aios_short}} 処理の不可欠な部分です。 評価するトランザクション・レコードをモデルに送信するたびに、{{site.data.keyword.aios_short}} サービスで摂動を実行して説明を生成するための追加処理が発生します。

- 表形式、テキスト、画像のモデルでは、以下のベースライン要求によってデータ・ポイントが生成されます。

   (-ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service) 個の評価要求で 5000 個のデータ・ポイントが生成されます。

- 表形式の分類モデルの場合のみ、対比的説明のために追加で実行される評価要求があります。 上記のベースライン要求に次の要求が追加されます。

   - 100 個の評価要求で、要求 1 つにつき 51 個の追加のデータ・ポイントが生成されます。
   - 101 個の評価要求で、要求 1 つにつき (ai-open-scale-ibm-aios-scheduling | 1 | Scheduling service) 個の追加のデータ・ポイントが生成されます。


## 次のステップ
{: #cdb-score-next-steps-scoringreq}

[モニタリングの構成](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-mo-config)。
