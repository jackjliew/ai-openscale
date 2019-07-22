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

# データベースの指定
{: #connect-db}

{{site.data.keyword.aios_short}} インスタンスで使用するデータベースを指定します。
{: shortdesc}

## データベースへの接続
{: #cdb-connect}

{{site.data.keyword.aios_short}} はデータベースを使用して、ペイロード、フィードバック、指標のデータを格納します。 データベースの選択以外に、データベースのスキーマを選択することもできます。スキーマとは、データベース内のテーブルのコレクションに名前を付けたものです。

1.  データベースを選択します。 無料のデータベースと、既存または新規のデータベースという 2 つのオプションがあります。

    ![データベースの選択](images/gs-config-database.png)

    有料の {{site.data.keyword.cloud_notm}} アカウントを持っている場合、`Databases for PostgreSQL` サービスまたは `Db2 Warehouse` サービスをプロビジョンし、Watson Studio サービスと統合して継続的な学習サービスを十分に活用できます。 有料サービスをプロビジョンしない場合、無料の内部 PostgreSQL ストレージを {{site.data.keyword.aios_short}} で使用できますが、ご使用のモデル向けに継続的な学習を構成することはできません。
    {: note}

### 無料の Lite プラン・データベース
{: #cdb-lite}

**注**: 無料のデータベースには、次のようないくつかの重要な制限事項があります。

- 無料のデータベースはホストされており、これに直接アクセスすることはできません。
- {{site.data.keyword.aios_full}} にはデータベースに対する全アクセス権限があります。つまり、自分のデータに対する全アクセス権限があります。
- 無料のデータベースは GDPR に準拠していません。 ご使用のモデルで PII (個人の特定が可能な情報) を処理する場合は、無料のデータベースを使用することはできません。 GDPR 規則に準拠している新しいデータベースを購入するか、そうした既存のデータベースを使用する必要があります。 詳しくは、[機密保護](/docs/services/ai-openscale?topic=ai-openscale-is-ov)を参照してください。

無料のデータベースを使用して作業を進めるには、**「無料のライト・プラン・データベースを使用する」**タイルをクリックしてから、**「保存」**をクリックします。

  ![データベースの選択](images/gs-config-database2.png)
  
無料のデータベースから別のデータベースにアップグレードすることはできますが、Compose for Postgres、Database for Postgres、または Db2 のインスタンスを再構成することによって無料のデータベースに切り替えることはできません。 アップグレード後は、無料のデータベースの使用に戻ることはできません。 構成、評価結果、説明などの現行データはすべて再利用できません。 別のスキーマやデータベースを選択すると、{{site.data.keyword.aios_short}} 環境は完全にリセットされます。



### 既存のデータベースまたは新しいデータベース
{: #cdb-exn}

1.  **「既存のデータベースを使用するか新しいデータベースを購入する」**オプションを選択すると、{{site.data.keyword.aios_short}} によって {{site.data.keyword.Bluemix_notm}} アカウントが調べられ、既存のデータベースが検出されます。

1.  既存のデータベース・タイプ (Compose for Postgres、Database for Postgres、または Db2) を選択し、**「データベース」**ドロップダウン・メニューからデータベースを選択し、**「スキーマ」**を選択します。

    {{site.data.keyword.aios_short}} は PostgreSQL データベースまたは Db2 データベースを使用して、モデル関連データ (フィードバック・データ、評価ペイロード) や計算された指標を保管します。 Db2 の Lite プランは現在サポートされていません。 訓練データの詳細については、[{{site.data.keyword.aios_short}} が訓練データにアクセスする必要があるのはなぜですか?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata) を参照してください。
    {: note}

    ![データベースの選択](images/gs-config-database3.png)

1.  **「別の場所を選択」**をクリックして、{{site.data.keyword.Bluemix_notm}} アカウントに含まれないデータベースの場所を指定することもできます。

    {{site.data.keyword.aios_short}} は PostgreSQL データベースまたは Db2 データベースを使用して、モデル関連データ (フィードバック・データ、評価ペイロード) や計算された指標を保管します。 Db2 の Lite プランは現在サポートされていません。
    {: note}

    - **「データベース・タイプ」**(`Compose for PostgreSQL`、`Database for PostgreSQL`、または `Db2`) を選択し、接続情報を指定します。

        - `Compose for PostgreSQL` データベースの場合、以下の情報を指定します。

            - ホスト名または IP アドレス
            - ポート
            - データベース (名前)
            - ユーザー名
            - パスワード

        - `Database for PostgreSQL` データベースの場合、以下の情報を指定します。

            - ホスト名または IP アドレス
            - SSL ポート
            - Base 64 エンコード証明書
            - データベース (名前)
            - ユーザー名
            - パスワード

        - `Db2` データベースの場合、以下の情報を指定します。

            - ホスト名または IP アドレス
            - SSL ポート
            - データベース (名前)
            - ユーザー名
            - パスワード

    - 正常に接続すると、スキーマを選択して作業を保存できます。

      アクセスを限定して Db2 インスタンスを提供する場合、スキーマ名を明示的に指定する必要があります。この場合、スキーマ名が自動生成されることはありません。 これは、Db2 Warehouse のエントリー・プランに当てはまります。
      {: important}

## 次のステップ
{: #cdb-next}

{{site.data.keyword.aios_short}} で[評価ペイロードを送信し](/docs/services/ai-openscale?topic=ai-openscale-connect-db#cdb-score)、[デプロイメント用のモニターを構成](/docs/services/ai-openscale?topic=ai-openscale-mo-config)する準備が整いました。