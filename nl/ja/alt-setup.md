---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: Python, install, python module, setup, set up, insights, explainability

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# {{site.data.keyword.aios_short}} をセットアップするための Python モジュールのインストール
{: #as-module}

必要な {{site.data.keyword.cloud_notm}} サービスのプロビジョニングと構成を自動化し、{{site.data.keyword.aios_full}} アプリケーション (サンプル・データを含む) を表示するために、Python モジュールをインストールできます。
{: shortdesc}

## このモジュールについて
{: #as-about}

- このモジュールを使用すると、テクニカル・ユーザーは[入門](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted)チュートリアルで説明されている方法で自分でサービスのプロビジョンと構成を行わなくても、{{site.data.keyword.aios_short}} インスタンスが稼働していることを確認できます。
- Python モジュールは、自分が所有するサービスの確認と、{{site.data.keyword.aios_short}} など必要なサービスの作成を行うプロセスを支援します。 モジュールが正常に実行されると、{{site.data.keyword.cloud_notm}} ダッシュボードから {{site.data.keyword.aios_short}} を起動してモデルのモニター方法を確認できます。

## 始めに
{: #as-prereqs}

1. [{{site.data.keyword.cloud_notm}} API キーを作成して、ダウンロードします](/docs/iam?topic=iam-userapikey#create_user_key)。 後ほどのステップでこの API キーを入力する必要があります。

2. [Python 3 の任意のリリース ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.python.org/downloads/){: new_window} をインストールします。

  Python 3 には、必要な pip パッケージ管理システムが含まれています。
  {: note}

3. 次のコマンドを実行して `ibm-ai-openscale-cli` パッケージをインストールします。

    ```
    pip install -U ibm-ai-openscale-cli
    ```
    {: codeblock}

    システムに複数のバージョンの pip がインストールされている場合、`pip` ではなく `pip3` を `pip3 install -U ibm-ai-openscale-cli` と実行する必要があります。
    {: tip}

4. 既存の {{site.data.keyword.pm_short}} サービス・インスタンスがある場合、[{{site.data.keyword.cloud_notm}} ダッシュボード ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}){: new_window} を確認して、サービスが Cloud Foundry ではなく {{site.data.keyword.iamshort}} (IAM) によって管理されていることを確かめます。

  **重要**: このモジュールは、{{site.data.keyword.pm_short}} のインスタンスの有無を検査します。 インスタンスがある場合、モジュールはそのインスタンスを使用します。 ただし、インスタンスが Cloud Foundry によって管理されている場合、最初に[ IAM リソース・グループにマイグレーションしてからモジュールを実行する必要があります](/docs/resources?topic=resources-migrate#migrate)。

## モジュールの実行
{: #as-run}

以下のコマンドを実行します。

```
ibm-ai-openscale-cli --apikey <Your API key>
```
{: codeblock}

## {{site.data.keyword.aios_short}} における結果の表示
{: #as-open}

モデルの公平性と正解率に関するインサイト、モニター対象データの詳細、および個々のトランザクションの説明性を表示するには、[{{site.data.keyword.aios_short}} ダッシュボード ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window} を開きます。

- サンプル・データのシナリオを把握するには、[{{site.data.keyword.aios_short}} のユースケースと利用価値に関する説明](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted#gs-use)を参照してください。

### インサイトの表示
{: #as-insights}

[{{site.data.keyword.aios_short}} ダッシュボード ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window} で**「インサイト」**タブをクリックします。このタブには、デプロイ済みモデルの指標の概要が示されます。![インサイト](images/insight-dash-tab.png)

- 「インサイト」ページには、公平性と正解率に関する問題が一目で分かるように表示されます。問題の判定には、構成されたしきい値が使用されます。

- 各デプロイメントはタイルとして表示されます。 以下の画面キャプチャーに示すように、このモジュールでは `GermanCreditRiskModel` というデプロイメントが構成されています。

  ![「洞察」の概要](images/setup01-0206.png)

### モニタリング・データの表示
{: #as-monitoring}

1. 「インサイト」ページで `GermanCreditRiskModel` タイルをクリックして、モニター対象データに関する詳細を表示します。
2. グラフの上でマーカーをスライドさせ、データを表示する日時期間を表示して**「詳細を表示します」**リンクをクリックします。

   - 例えば、以下の画面には、特定の日時のデータが表示されています。 モジュールの実行タイミングによって日時は異なります。

   - 時系列グラフの解釈について詳しくは、[公平性、毎分平均リクエスト数、正解率のモニター](/docs/services/ai-openscale?topic=ai-openscale-it-ov)を参照してください。

    ![モニター・データ](images/setup02-0206.png)

3. `AGE` データのモニタリングに関する詳細を確認するには、ドロップダウン・メニューで `AGE` が選択されていることを確認します。

  - 以下の画面キャプチャーでは、バイアスが存在しないことに注目してください。

  - 特定時刻におけるデータ・ポイントのグラフの解釈について詳しくは、[公平性、毎分平均リクエスト数、正解率のモニター](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-intp)を参照してください。

    ![詳細を表示します](images/setup03-0206.png)

### 説明性の表示
{: #as-explain}

特定の期間にバイアスが存在する要因について理解するには、前のセクションの可視化画面に示されているように、**「トランザクションの表示」**ボタンを選択します。

過去の時刻においてバイアスが存在するトランザクションのトランザクション ID がリストされます。 このモジュールで使用されるモデルの場合、選択可能なリクエストにおいてはバイアスが存在しません。 そのため、以下の画面キャプチャーでは、対象期間において表示されているトランザクションはありません。

  ![トランザクションのないトランザクション・リスト](images/setup06-0206.png)

トランザクションの検出と説明について詳しくは、[トランザクションの説明](/docs/services/ai-openscale?topic=ai-openscale-ie-ov#ie-view)を参照してください。

## 関連情報
{: #as-info}

- バイアスについては、[公平性](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)を参照してください。
- モデルの予測結果の精度については、[正解率](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor)を参照してください。
- グラフとデータの解釈方法については、[公平性、毎分平均リクエスト数、正解率のモニター](/docs/services/ai-openscale?topic=ai-openscale-it-ov)を参照してください。
- 背後にある要因が結果に及ぼす影響については、[説明性のモニター](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)を参照してください。
