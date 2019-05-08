---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-15"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:hide-dashboard: .hide-dashboard}
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

# 入門
{: #gs-get-started}

{{site.data.keyword.aios_full}} を使用すると、企業は、ビジネス・アプリケーションの AI ライフサイクルを自動化して運用可能にすることができます。これにより、AI モデルにバイアスがなくなるので、ビジネス・ユーザーによる説明や理解が容易になり、ビジネス・トランザクションでの監査が可能になります。{{site.data.keyword.aios_short}} は、ツールで作成されて実行される AI モデルをサポートしています。また、モデルは、選択したフレームワークを提供します。
{: shortdesc}

## 概説
{: #gs-demo}

このビデオを視聴して、{{site.data.keyword.aios_short}} の概要を把握してください。

<p>
  <div class="embed-responsive embed-responsive-16by9">
    <iframe class="embed-responsive-item" id="youtubeplayer" title="Trust and Transparency in AI" type="text/html" width="640" height="390" src="https://www.youtube.com/embed/6Ei8rPVtCf8" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>
  </div>
</p>

## 自動化されたセットアップ
{: #gs-module}

{{site.data.keyword.aios_short}} でモデルがどのようにモニターされるかを簡単に確認するには、最初に {{site.data.keyword.aios_short}} UI にログインした際に提供されたデモ・シナリオ・オプションを実行します。[UI デモの利用](#gs-work-demo)を参照してください。

テクニカル・ユーザーは、Python モジュールをインストールすることを選択できます。このモジュールは、{{site.data.keyword.aios_short}} やその他のサービスの構成を自動化して、サンプル・データを提供します。[Python モジュールの実行](#gs-run)を参照してください。

[追加リソース](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-arsc-ov)のトピックに、追加のチュートリアル・リンクがあります。

## UI デモの利用
{: #gs-work-demo}

1.  {{site.data.keyword.icpfull}} for Data 上の {{site.data.keyword.aios_short}} インスタンスにサインインします。

    ![OpenScale クラスターへのサインイン](images/icp4d_sign_in.png)

1.  デモ・シナリオを利用するには、**「次へ」**を選択します。

    ![デモ「ようこそ」](images/demo_welcome.png)

1.  次に、Db2 データベースのホスト名/IP アドレス、ポート、ユーザー名、およびパスワードを指定します。デモ用のデータベース名を作成してから、**「準備 (Prepare)」**をクリックします。

    ![デモ「データベースへの接続」](images/demo_connect_db2.png)

{{site.data.keyword.aios_short}} サービスがプロビジョンされる過程で、以下のように、デモ・シナリオを確認できます。

  ![デモ・シナリオ](images/demo_wait.png)

プロビジョニングが完了したら、**「始めましょう (Let's Go)」**を選択して、{{site.data.keyword.aios_short}} ダッシュボードを終了し、以下の [{{site.data.keyword.aios_short}} での結果の表示](#gs-open)に進みます。

  ![デモ「始めましょう」](images/demo_go.png)

## Python モジュールの実行
{: #gs-run}

### 始める前に
{: #gs-prereqs}

1.  [{{site.data.keyword.aios_short}} を {{site.data.keyword.icpfull}} for Data にインストールします](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-inst-install-icp)。
1.  [Python 3 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.python.org/downloads/){: new_window} の任意のリリースをインストールします。

    Python 3 には、必要な pip パッケージ管理システムが組み込まれています。
    {: note}

1.  次のコマンドを実行して、`ibm-ai-openscale-cli` パッケージをインストールします。

    ```bash
    pip install -U ibm-ai-openscale-cli
    ```
    {: codeblock}

### コマンドの実行
{: #gs-command}

この Python モジュールを以前に実行している場合、再度実行すると新規テーブルが作成され、`AIOSFASTPATHICP` スキーマ内の以前のデータがすべてオーバーライドされることに注意してください。スキーマを手動でクリアするには、以下の[サンプル・データベースとスキーマの削除](#gs-cleanup)を参照してください。
{: note}

コマンドに、以下の必要な情報に置き換わる必須の引数を指定して、実行します。

```bash
ibm-ai-openscale-cli --apikey None --db2 <path to IBM DB2 credentials file> --env icp --username <admin> --password <password> --url https://<IP address of host ICP for Data installation>:31843
```
{: codeblock}

オプションの `--datamart-name <datamart name>` 引数の場合、モジュールを実行すると、`aiosfastpath` という `datamart-name` 値が作成されます。これは、専ら {{site.data.keyword.aios_short}} で使用するために予約する必要があるスキーマです。モジュールは、再実行されると、`datamart-name` スキーマをプログラマチックに削除して再作成します。したがって、このスキーマを他の目的に使用することはできません。
{: note}

モジュールを正常に実行するには、いくつかの Db2 パラメーターの値を変更する必要があります。Db2 データベース環境のコマンド・ウィンドウから、**_行ごとに_** 編成された以下のコマンドを実行します。

```bash
db2 connect to [dbname] user [db username] using [db password]
```

```bash
db2 update db cfg for [dbname] using SELF_TUNING_MEM ON
```

```bash
db2 update db cfg for [dbname] using SORTHEAP 1024 AUTOMATIC
```

```bash
db2 update db cfg for [dbname] using SHEAPTHRES_SHR 5000 AUTOMATIC
```

```bash
db2 update db cfg for [dbname] using LOGFILSIZ 5000
```

Db2 データベース環境のコマンド・ウィンドウから、**_列ごとに_** 編成された以下のコマンドを実行します。

```bash
db2  AUTOCONFIGURE APPLY DB AND DBM
```
{: important}

### IBM DB2 資格情報ファイルの例

IBM DB2 資格情報ファイルは、以下の `db2-vcap.json` ファイルのようなものです。

```bash
{
  "hostname": "<DB2 IP address>",
  "password": "<your password>",
  "port": 50000,
  "db": "FASTPATH",
  "username": "<DB2 user name>"
}
```
{: codeblock}

## {{site.data.keyword.aios_short}} での結果の表示
{: #gs-open}

モデルの公平性と正確度、モニター対象データの詳細、および個々のトランザクションの説明可能性に対する洞察を表示するには、{{site.data.keyword.aios_short}} ダッシュボードを開きます。

### 洞察の表示
{: #gs-insights}

{{site.data.keyword.aios_short}} ダッシュボードで、**「洞察 (Insights)」**タブをクリックします。このタブには、デプロイしたモデルのメトリックの概要が表示されます。![洞察 (Insights)](images/insight-dash-tab.png)

- 「洞察 (Insights)」ページには、構成されたしきい値で判別されるとおりに、公平性と正確度に関するあらゆる問題が表示されているのが一目で分かります。

- 各デプロイメントは、タイルとして表示されます。次の画面キャプチャーに示すように、モジュールによって、`GermanCreditRiskModelICP` というデプロイメントが構成されています。

  ![洞察の概要](images/setup01-0206.png)

### モニター・データの表示
{: #gs-monitoring}

1.  「洞察 (Insights)」ページで、`GermanCreditRiskModelICP` タイルをクリックして、モニター対象データに関する詳細を表示します。
1.  グラフでマーカーをクリックしてドラッグし、データが表示される日時の期間を表示して、**「詳細の表示 (View details)」**リンクをクリックします。あるいは、グラフで別の期間をクリックして、表示するデータを変更することもできます。

     - 例えば、次の画面には、特定日時のデータが表示されます。日付と時刻は、モジュールをいつ実行するかによって異なります。

     - 時系列グラフの解釈については、[公平性、分当たりの平均要求数、および正確度のモニター](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart)を参照してください。

      ![モニター・データ](images/setup02-0206.png)

1.  `AGE` のデータのモニタリングに関する詳細を表示するには、ドロップダウン・メニューで `AGE` が選択されていることを確認してください。

    - 次の画面キャプチャーでは、バイアスが存在していないことに注意してください。

    - 特定時間のデータ・ポイントのグラフの解釈については、[データ可視化](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart#itc-data-visual)を参照してください。

      ![詳細の表示](images/setup03-0206.png)

### 説明可能性の表示
{: #gs-explain}

指定の期間にバイアスが存在する場合にその原因となる要素を理解するには、前のセクションで示した可視化画面から、**「バイアスしたトランザクションの表示 (View biased transactions)」**ボタンを選択します。

バイアスがあるトランザクションについて、過去 1 時間のトランザクション ID がリストされます。このモジュールで使用されるモデルの場合、使用可能な要求にバイアスは存在しません。したがって、次の画面キャプチャーには、その期間のトランザクションは表示されません。

  ![トランザクションが含まれないトランザクション・リスト](images/setup06-0206.png)

トランザクションの検索と説明については、[説明可能性のモニター](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-ie-ov)を参照してください。

## サンプル・データベースとスキーマの削除
{: #gs-cleanup}

サンプル・データベースとそのスキーマを削除するには、次のコマンドを実行します。

```bash
ibm-ai-openscale-cli -i <iam-token> --datamart-reset --datamart-name <datamart name>
```

## 関連情報
{: #gs-info}

- バイアスについては、[公平性](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mf-monitor)を参照してください。
- モデルでの結果の適切な予測方法については、[正確度](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-acc-monitor)を参照してください。
- グラフ、データ、およびトランザクションの解釈については、[公平性、分当たりの平均要求数、および正確度のモニター](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart)を参照してください。
