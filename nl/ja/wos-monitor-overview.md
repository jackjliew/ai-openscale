---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: deployment, monitors, data

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

# デプロイメントでのモニタリングのための準備
{: #mo-config}

{{site.data.keyword.aios_short}} で追跡するデプロイメントごとにモニターをセットアップして有効にします。
{: shortdesc}

## デプロイメントの選択
{: #mo-select-deploy}

1. **「インサイト」**タブで、**「デプロイメントの追加 (Add deployments)」**ボタンをクリックします。 

   ![デプロイメントの選択ページ](images/config-select-deploy.png)

   使用可能なモデル・デプロイメントのリストが表示されます。

   ![モニタリングのための準備](images/wos-select-model-deployment.png)

2. モデル・デプロイメントをクリックしてから、**「構成」**をクリックします。

   特定の 1 つのモデルに複数のデプロイメントがある場合、1 つのデプロイメントを構成すると、同じモデルに属する他のすべてのデプロイメントも構成されます。

   選択内容を保存したら、ペイロード・ロギング、正解率、公平性などのモニターを構成する準備は完了です。 

2. 開始するには、**「モニタリングの構成」**をクリックします。

## ペイロード・ロギングの詳細の入力
{: #mo-work-data}

モデルと訓練データに関する情報を入力する必要があります。 訓練データの詳細については、[{{site.data.keyword.aios_short}} が訓練データにアクセスする必要があるのはなぜですか?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata) を参照してください。

![説明の準備](images/config-what-monitor.png)

- {{site.data.keyword.aios_short}} インスタンスと同じ地域の {{site.data.keyword.pm_full}} インスタンスを使用する場合は、データ・タイプとアルゴリズム・タイプを選択する必要がありますが、一部のペイロード・ロギング情報は自動的に構成されます。
- そうでない場合は、**「ペイロード・ロギング (Payload logging)」**タブおよびウィンドウで、データ、アルゴリズム・タイプ、およびペイロード・ロギングに関する情報を入力する必要があります。 

   選択内容に応じて固有の要件があります。 詳しくは、[数値/カテゴリカル・データ](https://test.cloud.ibm.com/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mo-config#mo-datan)を参照してください。

   モニターを構成するには、実行するコード・スニペットの 1 つをコピーしておく必要があります。 クライアント・アプリケーションで cURL コマンドを実行するか、データ・サイエンス・ノートブックで Python コマンドを実行します。 これにより、モデル・デプロイメントの要求をログに記録し、応答データをペイロード・データベースに書き込むことができます。
   
ローカル {{site.data.keyword.pm_full}} メソッドを使用するか API を使用してペイロード・ロギングの詳細を送信した後に、**「ペイロード・ロギング (Payload logging)」**画面に戻り、**「完了 (I'm finished)」**をクリックする必要があります。

![ペイロード・ロギング画面が表示されています](images/payload-logging-gosales001.png)

評価が正しく {{site.data.keyword.aios_short}} に送信されていた場合は、**「完了 (I'm finished)」**ボタンをクリックすると次の画面が表示されます。ボタンが非表示になり、**「ロギングは正常にアクティブになりました (Logging activated successfully)」**というメッセージが表示されます。

![データが正常にアップロードされた後のペイロード・ロギング画面が表示されています](images/payload-logging-gosales002.png)


### モデル詳細の入力
{: #mo-work-model-dets}

{{site.data.keyword.aios_short}} がデータベースにアクセスしてモデルのセットアップ方法を理解できるように、モデルに関する情報を入力します。

具体的には、モニターを構成するために以下のタスクを実行する必要があります。

1. 訓練データの場所を指定します。 これを行うには、場所、ホスト名または IP アドレス、データベース名、および認証情報を入力します。
2. データベース内で、スキーマとテーブルを選択して訓練テーブルを選択する必要があります。
3. 訓練テーブルからラベル列を選択します。
4. AI デプロイメントの訓練に使用された特徴量を選択します。
5. テキストの特徴量とカテゴリカルの特徴量を選択します。
6. デプロイメント予測列を選択します。
7. 最後に、モデルの詳細を確認してから、そのモデルを保存できます。

以下のセクションでは、モデルのタイプ ([数値/カテゴリカル・データ](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mo-config#mo-datan)または[画像と非構造化テキスト](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mo-config#mo-datai)) に応じて必要になる具体的な情報について説明します。


### 数値/カテゴリカル・データ
{: #mo-nuca}

数値データまたはカテゴリカル・データの場合、モニターを構成するためにはモデルの訓練データに関する情報を入力する必要があります。

- **モニターの手動構成** - 訓練データの接続情報を入力する必要があります。

    - [アルゴリズムのタイプ](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-understand)を選択して、**「次へ」**をクリックします。

      訓練データのフォーマットはモデルと一致する必要があります。 例えば、モデルで特徴量 `Gender` の値に `M` と `F` を使用する必要がある場合は、訓練データに `Male` と `Female` ではなく、`M` と `F` が入っていなければなりません。  現行リリースの {{site.data.keyword.aios_short}} では、Db2 データベースまたは Cloud Object Storage のロケーションのみサポートされています。
        {: important}

    - 「場所」(`Db2` または `Cloud Object Storage`) を指定し、以下のいずれかの操作を行います。

        - Db2 データベースの場合は、以下の情報を入力します。

            - ホスト名または IP アドレス
            - ポート
            - データベース (名前)
            - ユーザー名
            - パスワード

        - Cloud Object Storage の場合は、以下の情報を入力します。

            - ログイン URL: ログイン URL は、訓練データが配置されているバケットの地域設定と一致している必要があります。 訓練データのバケットは次のステップで指定します。
            - リソース・インスタンス (ID)
            - API キー

    - 有効な接続であることを確認するには、**「テスト」**ボタンをクリックして訓練データに接続します。
    - 訓練データが配置されている Db2 データベースまたは Cloud Object Storage の正確な場所を指定します。

        - Db2 データベースの場合は、モデルに必要な列が含まれている訓練テーブルとスキーマの両方を選択します。
        - Cloud Object Storage の場合は、バケットとデータ・セットを選択します。

- **構成ファイルのアップロード** - 訓練データを秘密にしておく場合はこのオプションを選択します。 カスタム Python ノートブックを使用して、訓練データ自体にはアクセスできないように訓練データを分析するための情報を {{site.data.keyword.aios_short}} に提供できます。

  Python ノートブックを実行すると、スキーマ列の個別の値と列名をキャプチャーできます。 また、ノートブックを使用して公平性モニターを事前構成することもできます。

   - [カスタム・ノートブック](https://github.com/IBM-Watson/aios-data-distribution/blob/master/training_statistics_notebook.ipynb){: external}をダウンロードし、資格情報をすべて独自の資格情報に置き換えます。
   - ノートブックの内容を慎重に確認し、モデルのデータを適宜指定します。 ノートブックを保存します。
   - ノートブックを実行して JSON 形式の構成ファイルを生成します。
   - JSON 構成ファイルをアップロードします。

     ![JSON 構成のアップロード](images/config-json-monitor.png)

- {{site.data.keyword.aios_short}} は、{{site.data.keyword.pm_full}} にモデルと一緒に保管されているメタデータから訓練データを見つけます。 予測値が入っている訓練データのラベル列を選択します。
- モデルの訓練に使用する列を選択します。これらの列は、モデルのデプロイメントでリクエストに含まれている必要がある特徴量です。
- 最後に、テキストから整数に変換された値が入っている列を選択します。 例えば、元の訓練データでは `Gender` として `Male` または `Female` が設定されていて、これらの値がそれぞれ `0` と `1` にマップされている場合、訓練データの `Gender` 列の値として `0` と `1` が設定されるようになります。 最初はテキスト値が入っていたけれども今は整数が入るようになった列を確認します。

### イメージと非構造化テキスト
{: #mo-imun}

- **イメージ**

  イメージを入力として受け入れるモデルでは、イメージは (高さ) x (幅) x (チャネル数) という形式で表記する必要があります。各ポイントは各ピクセルの単色値または RGB 値のいずれかを表します。

- **非構造化テキスト**

   テキストを入力として受け入れるモデルでは、モデルがテキストのベクトル化表記ではなくテキスト全体を受け入れる必要があります。

## 構成の確認と保存
{: #mo-save}

選択内容の要約を確認し、**「保存」**をクリックして先に進みます。

  ![データ・テーブルの選択](images/config-summary-monitor.png)

### 次のステップ
{: #mo-next}

モニターの構成を続けるには、**「正解率」**タブをクリックし、**「開始」**をクリックします。詳しくは、[正解率モニターまたはモデル性能モニターの構成](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor)を参照してください。
