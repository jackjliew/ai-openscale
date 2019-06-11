---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: feedback data, data, feedback, models

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

# {{site.data.keyword.aios_short}} でのフィードバック・データのフォーマット設定とアップロード
{: #fmt-upld-fdbk-data}

フィードバック・データは、バイアスのないモデルを維持するには不可欠です。定期的にフィードバック・データを {{site.data.keyword.aios_full}} サービスにアップロードすることにより、モデルで最新のデータ (予測アプリケーションのコンテキストの変更を示している場合がある) が考慮されるようにする必要があります。フィードバック・ループを通して、システムは、予測の有効性をモニタリングして必要に応じてリトレーニングすることにより、継続的に学習していきます。モニタリングしてその結果のフィードバックを利用するということは、機械学習の中核を成す部分です。フィードバック・データのフォーマット設定とアップロードに際しては、以下の情報を参考にしてください。
(: shortdesc)

## フィードバック・データのフォーマット設定
{: #fmt-upld-fdbk-data-fmt}

フィードバック・データを正しく読み取るには、フォーマット設定が適切に行われている必要があります。{{site.data.keyword.aios_short}} サービスは、以下の形式を受け入れます。

- CSV ファイル形式。この形式は UI または REST API を使用してアップロードできます。
- JSON ファイル形式。この形式は REST API によってのみアップロードできます。

これらのファイル形式は、スキーマ `training_data_schema` で定義されています。これは、サブスクリプションの詳細の中に含まれています。`training_data_schema` を表示するには、Python API を使用して以下のコマンドを実行します。

```
subscription.get_details()['entity']['asset_properties']['training_data_schema']
```

訓練データ・スキーマをフィードバック・スキーマと比較するためにフィードバック・スキーマを表示したいという場合もあります。フィードバック・スキーマを表示するには、Python API を使用して以下のコマンドを実行します。

```
subscription.feedback_logging.print_table_schema()
```


### CSV 形式
{: #fmt-upld-fdbk-data-fmt-csv}

CSV ファイルの場合は通常、複数の列名に 1 行で対応する行を入力して、列と行のデータを提供します。

通常、列名がすべて大文字の場合は、Db2 では大/小文字を区別しなくなるので、引用符で囲む必要はありません。その他のデータベースの場合や、大文字と小文字が混在している場合は、大文字と小文字が完全に一致する必要があります。
ファイルに列名が含まれている場合、列がテーブルの順序と一致している必要はありませんが、ファイルに列名が含まれていない場合、列はテーブルの順序と一致している必要があります。元の訓練データにはない列が含まれることがあります。処理中、これらの列は無視されます。


### JSON 形式
{: #fmt-upld-fdbk-data-fmt-json}

JSON 形式は、列名に対応するフィールドが含まれるオブジェクトの集合で構成されています。

