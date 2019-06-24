---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: deployment, monitors, data

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

# デプロイメントでのモニタリングのための準備
{: #mo-config}

{{site.data.keyword.aios_short}} で追跡するデプロイメントごとにモニターをセットアップして有効にします。
{: shortdesc}

## デプロイメントの選択
{: #mo-select-deploy}

1.  最初にデプロイメントを選択する必要があります。

    特定の 1 つのモデルに複数のデプロイメントがある場合、1 つのデプロイメントを構成すると、同じモデルに属する他のすべてのデプロイメントも構成されます。
    {: note}

    ![デプロイメントの選択ページ](images/config-select-deploy.png)

1.  *「モニタリングのための準備」*タイルを選択します。

    ![モニタリングのための準備](images/config-prep-monitor.png)

## データの操作
{: #mo-work-data}

1.  次に、モデルと訓練データに関する情報を入力します。**「次へ」**をクリックします。 訓練データの詳細については、[{{site.data.keyword.aios_short}} が訓練データにアクセスする必要があるのはなぜですか?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata) を参照してください。

    ![説明の準備](images/config-what-monitor.png)

1.  ドロップダウン・メニューからデプロイメントで分析するデータのタイプを選択し、**「次へ」**をクリックします。

    ![入力タイプの選択](images/config-input-monitor.png)

### 数値/カテゴリカル・データ
{: #mo-nuca}

数値データまたはカテゴリカル・データの場合、モニターを構成するためにはモデルの訓練データに関する情報を入力する必要があります。

  ![構成タイプの選択](images/config-manual-monitor.png)

- **モニターの手動構成** - 訓練データの接続情報を入力する必要があります。

    - [アルゴリズムのタイプ](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-understand)を選択して、**「次へ」**をクリックします。

      ![マルチクラス](images/multiclass.png)

      訓練データのフォーマットが、ご使用のモデルで必要なフォーマットと厳密に同一であることを確認してください。 例えば、モデルで特徴量 *Gender* の値が `M` と `F` である必要がある場合、訓練データには `Male` と `Female` ではなく、`M` と `F` を入れておく必要があります。 現在 {{site.data.keyword.aios_short}} では、Db2 データベースまたは Cloud Object Storage のロケーションだけがサポートされています。
        {: important}

    - 「場所」(`Db2` または `Cloud Object Storage`) を指定し、以下のいずれかの操作を行います。

        - Db2 データベースの場合、以下の情報を指定します。

            - ホスト名または IP アドレス
            - ポート
            - データベース (名前)
            - ユーザー名
            - パスワード

            ![訓練データが配置されている Db2 の場所を指定するページ](images/config-train-db2-monitor.png)

        - Cloud Object Storage の場合、以下の情報を指定します。

            - ログイン URL

              ログイン URL は、訓練データが配置されているバケットのリージョン設定に一致している必要があります。 訓練データのバケットは次のステップで指定します。
              {: important}

            - リソース・インスタンス (ID)
            - API キー

            ![訓練データが配置されている Cloud Object Storage の場所を指定するページ](images/config-train-cos-monitor.png)

    - 有効な接続であることを確認するため、**「テスト」**ボタンをクリックして訓練データに接続します。 **「次へ」**をクリックします。

    - 訓練データが配置されている Db2 データベースまたは Cloud Object Storage の正確な場所を指定します。

        - Db2 データベースの場合、モデルに必要な列が格納されている訓練テーブルとスキーマの両方を選択します。

          ![スキーマとト訓練テーブルが配置されている Db2 の場所の指定](images/fair-config-table-db2.png)

        - Cloud Object Storage の場合、バケットとデータ・セットを選択します。

          ![データ・セットが配置されている Cloud Object Storage の場所の指定](images/fair-config-dset-cos.png)

          **「次へ」**をクリックして以下のステップ 5 に進みます。

- **構成ファイルのアップロード** - 訓練データを秘密にしておく場合はこのオプションを選択します。 カスタム Python ノートブックを使用して、訓練データ自体にはアクセスできないように訓練データを分析するための情報を {{site.data.keyword.aios_short}} に提供できます。

  Python ノートブックを実行すると、スキーマ列の個別の値と列名をキャプチャーできます。 また、ノートブックを使用して公平性モニターを事前構成することもできます。

    - [カスタム・ノートブック ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/IBM-Watson/aios-data-distribution/blob/master/training_statistics_notebook.ipynb){: new_window} をダウンロードし、資格情報をすべて独自の資格情報に置き換えます。

    - ノートブックの内容を慎重に確認し、モデルのデータを適宜指定します。 ノートブックを保存します。

    - ノートブックを実行して JSON 形式の構成ファイルを生成します。

    - JSON 構成ファイルをアップロードします。

        ![JSON 構成のアップロード](images/config-json-monitor.png)

    - **「次へ」**をクリックします。

- {{site.data.keyword.aios_short}} により、WML でモデルと共に保管されているメタデータから訓練データが検出されます。 予測値を入れた訓練データのラベル列を選択し、**「次へ」**をクリックします。

  ![列ラベルの選択](images/fair-config-column.png)

- モデルのトレーニングに使用する列を選択します。これらの列は、モデルのデプロイメントでリクエストに含まれている必要がある特徴量です。 **「次へ」**をクリックします。

    ![列ラベルの選択](images/explain-select-column.png)

- 最後に、テキストから整数に変換された値が入っている列を選択します。 例えば、元の訓練データでは *Gender* として `Male` または `Female` が設定されていて、これらの値がそれぞれ `0` と `1` にマップされている場合、訓練データの *Gender* 列の値として `0` と `1` が設定されるようになります。 元の値はテキスト値で今は整数になっている列を指定します。 **「次へ」**をクリックします。

    ![データ・テーブルの選択](images/explain-text-column.png)

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

モニターの構成を開始するため、カテゴリーを選択して**「開始」**をクリックします。
