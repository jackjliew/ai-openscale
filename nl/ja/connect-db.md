---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# データベースの指定
{: #cdb-connect}

{{site.data.keyword.aios_short}} インスタンスで使用されるデータベースを指定します。
{: shortdesc}

## データベースへの接続
{: #cdb-config}

{{site.data.keyword.aios_short}} では、データベースを使用してペイロード、フィードバック、測定データを保管します。データベースを選択するだけでなく、データベースのスキーマを選択することもできます。スキーマとは、データベース内のテーブルの名前指定されている集合のことです。

1.  データベースを選択します。無料のライト・プラン・データベースと、既存または新規のデータベースの 2 つのオプションがあります。

    ![データベースの選択](images/gs-config-database.png)

### 無料のライト・プラン・データベース
{: #cdb-lite}

無料のライト・プラン・データベースには以下のような重要な制限事項があります。

- 無料のライト・プラン・データベースはホストされるので、直接アクセスできません。
- {{site.data.keyword.aios_full}} にはご使用のデータベースに対する全アクセス権限があるので、ご使用のデータに対する全アクセス権限があることになります。
- 無料のライト・プラン・データベースは GDPR に準拠していません。ご使用のモデルで個人情報 (PII) が処理される場合は、無料のライト・プラン・データベースを使用することはできません。新しいデータベースを購入するか、GDPR 規則に準拠している既存のデータベースを使用しなければなりません。詳細については、[機密保護](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-is-infosec)を参照してください。

無料のライト・プラン・データベースを使用して続行するには、単にそのオプションを選択してから、要約データを検討し、**「保存」**をクリックするだけです。

  ![データベースの選択](images/gs-config-database2.png)

### 既存または新規のデータベース
{: #cdb-exn}

1.  「既存のデータベースの使用または新規データベースの購入 (Use existing or purchase new database)」オプションを選択すると、{{site.data.keyword.aios_short}} で {{site.data.keyword.cloud_notm}} アカウントが検査されて既存のデータベースが探索されます。

1.  以下のように、既存のデータベース・タイプ (Compose for Postgres、Database for Postgres、または Db2) を選択し、続いて**「データベース」**ドロップダウン・メニューからデータベースを選択し、続いて**「スキーマ」**からスキーマを選択します。

    {{site.data.keyword.aios_short}} では、PostgreSQL または Db2 データベースを使用して、モデル・デプロイメントの出力とリトレーニング・データを保管します。Db2 のライト・プランは現在サポートされていません。
    {: note}

    ![データベースの選択](images/gs-config-database3.png)

1.  **「別の場所の選択 (Select a different location)」**をクリックして、{{site.data.keyword.cloud_notm}} アカウント外のデータベースの場所を指定することもできます。

    - **「データベース・タイプ」** (`Compose for PostgreSQL`、`Database for PostgreSQL`、または `Db2`) を選択してから、接続情報を入力します。

        - `Compose for PostgreSQL` データベースの場合、以下の情報を入力します。

            - ホスト名または IP アドレス
            - ポート
            - データベース (名前)
            - ユーザー名
            - パスワード

            ![Compose for Postgres データベースの場所の指定](images/db-config-cpostgres.png)

        - `Database for PostgreSQL` データベースの場合、以下の情報を入力します。

            - ホスト名または IP アドレス
            - SSL ポート
            - Base 64 エンコードされた証明書
            - データベース (名前)
            - ユーザー名
            - パスワード

            ![Database for Postgres データベースの場所の指定](images/db-config-dpostgres.png)

        - `Db2` データベースの場合、以下の情報を入力します。

            - ホスト名または IP アドレス
            - SSL ポート
            - データベース (名前)
            - ユーザー名
            - パスワード

            ![Db2 の場所の指定](images/db-config-db2.png)

    - 正常に接続し終えたら、スキーマを選択できます。

      アクセスに制限のある Db2 インスタンスの指定時には、スキーマ名を自動生成できないので、スキーマ名を明示的に指定する必要があります。これは Db2 Warehouse エントリー・プランに適用されます。
      {: important}

      ![スキーマの選択](images/gs-config-database5.png)

**「次へ」**をクリックし、要約データを検討してから、**「保存」**をクリックします。

## スコアリング要求の送信
{: #cdb-scoring}

{{site.data.keyword.aios_short}} では、モニターの構成時に、モニターされるデータの記録を開始するために、スコアリング要求を送信する必要があります。

Watson Machine Learning 内でデプロイされるモデルは、{{site.data.keyword.aios_short}} により自動的にスコアリングされます。Watson Machine Learning 内でデプロイされているモデルのみ使用する場合は、この画面は表示されません。
{: note:}

デプロイメント (この場合は「不正検出 (Fraud Detector)」) を選択してから、提供されている `cURL` または `Python` コード・スニペットを使用して、モデル・デプロイメントの要求と応答のデータを記録します。詳細については、[Watson Machine Learning 以外のサービス・インスタンスに関するペイロード・ロギング](/docs/services/ai-openscale?topic=ai-openscale-cml-connect)を参照してください。

コード・スニペット内のフィールドと値を、実際の値に置換する必要があります。提供されている値は例にすぎないからです。
{: important}

![スコアリング要求の送信](images/config-send-scoring.png)

ペイロード・ロギングを実行すると、選択したデプロイメントに関する「モニターの準備ができました (Ready to Monitor)」列にチェック・マークが表示されます。**「モニターの構成」**をクリックして先に進みます。

## 次のステップ
{: #cdb-next}

{{site.data.keyword.aios_short}} で[ご使用のデプロイメント用にモニターを構成](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mo-config)する準備ができました。
