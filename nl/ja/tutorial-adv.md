---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: tutorial, Jupyter notebooks, Watson Studio projects, projects, models, deploy, 

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

# Python SDK チュートリアル (上級)
{: #crt-ov}

## シナリオ
{: #crt-scenario}

従来型の融資機関は、さらに多くの多様な顧客に金融サービスのデジタル・ポートフォリオを展開する必要に迫られています。これには、信用リスク・モデリングに対する新たな取り組みが必要です。 そうした企業のデータ・サイエンス・チームが現在利用している標準的なモデリング手法 (決定木やロジスティック回帰など) は、標準的なデータ・セットでは適切に機能し、容易に説明可能な推奨事項を提案します。 これは、信用融資に関する決定は透明かつ説明可能でなければならないという規制要件を満たしています。

対象範囲を広げてリスクの高い申請者が貸付を利用できるようにするため、申請者の信用履歴の確認範囲を、従来の貸付で利用していた情報 (住宅ローンや自動車ローンなど) から広げて、光熱費や携帯電話料金プランの支払い履歴、さらには学歴や職責などの代替信用情報も確認する必要があります。 このような新しいデータ・ソースは融資の裏付けとして役立ちますが、申請者の年齢、性別、その他の個人の特徴に基づく予期しない相関関係が設定されてバイアスが発生する可能性が高くなる、というリスクも生まれます。

このような多様なデータ・セットに最も適したデータ・サイエンス手法 (こう配ブースティング木、ニューラル・ネットワークなど) では、精度の高いリスク・モデルを生成できますが、コストがかかります。 このような「ブラック・ボックス」モデルで生成される予測は決定過程が不透明であるため、一般データ保護規則 (GDPR) の第 22 項や、アメリカ合衆国消費者金融保護局が管理する連邦公正信用報告法 (FCRA) などの規制に基づく承認を受けるためには、なんらかの方法で透明性を確保する必要があります。

このチュートリアルで使用する信用リスク・モデルでは、それぞれの融資申請者に関する 20 個の属性を設定した訓練データ・セットが使用されます。 これらの属性のうち、年齢と性別という 2 つの属性がバイアス検証に使用されます。 このチュートリアルでは、性別と年齢に対するバイアスに重点を置いています。 訓練データの詳細については、[{{site.data.keyword.aios_short}} が訓練データにアクセスする必要があるのはなぜですか?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata) を参照してください。

{{site.data.keyword.aios_short}} は、デプロイ済みモデルが一方のグループ (参照グループ) に対して他方のグループ (モニター対象グループ) より好ましい結果 (「No Risk」) を出す傾向をモニターします。 このチュートリアルでは、性別のモニター対象グループは `female` であり、年齢のモニター対象グループは `18 to 25` です。

## 前提条件
{: #crt-prereqs}

このチュートリアルで使用する Jupyter ノートブックは、Watson Studio プロジェクトで「Python 3.5 with Spark」ランタイム環境を使用して実行する必要があります。 以下の {{site.data.keyword.cloud_notm}} サービスのサービス資格情報が必要です。

- Cloud Object Storage ({{site.data.keyword.DSX}} プロジェクト保管のため)
- {{site.data.keyword.aios_short}}
- {{site.data.keyword.pm_full}}
- (オプション) Databases for PostgreSQL または Db2 Warehouse

Jupyter ノートブックは、German Credit Risk モデルをトレーニング、作成、デプロイし、デプロイメントをモニターするように {{site.data.keyword.aios_short}} を構成し、{{site.data.keyword.aios_short}} の「インサイト」ダッシュボードに表示する 7 日分の履歴レコードと指標値を提供します。 また、Watson Studio と Spark を使用した継続的な学習のためにモデルを構成することもできます。

## 概要
{: #crt-intro}

このチュートリアルでは、以下のタスクを実行します。

- [{{site.data.keyword.cloud_notm}} の機械学習サービスとストレージ・サービスをプロビジョンします](/docs/services/ai-openscale?topic=ai-openscale-crt-ov#crt-services)。
- [機械学習モデルを作成、トレーニング、およびデプロイするために、Watson Studio プロジェクトをセットアップして Python ノートブックを実行します](/docs/services/ai-openscale?topic=ai-openscale-crt-ov#crt-set-wstudio)。
- [{{site.data.keyword.aios_short}} をプロビジョンします](/docs/services/ai-openscale?topic=ai-openscale-crt-ov#crt-wos-adv)。
- [Python ノートブックを実行することによって、データマートを作成し、パフォーマンス・モニター、正解率モニター、および公平性モニターを構成し、モニター対象データを作成します](/docs/services/ai-openscale?topic=ai-openscale-crt-ov#crt-edit-notebook)。
- [{{site.data.keyword.aios_short}} の「インサイト」タブで結果を表示します](/docs/services/ai-openscale?topic=ai-openscale-crt-ov#crt-view-results)。

## {{site.data.keyword.cloud_notm}} サービスのプロビジョン
{: #crt-services}

{{site.data.keyword.ibmid}} を使用して、[{{site.data.keyword.cloud_notm}} アカウント ](https://{DomainName}){: external} にログインします。 サービスをプロビジョンする際、特に Db2 Warehouse を使用する場合は、選択した組織とスペースがすべてのサービスで同じであることを確認してください。

### {{site.data.keyword.DSX}} アカウントの作成
{: #crt-wstudio}

- [{{site.data.keyword.DSX}} インスタンス](https://{DomainName}/catalog/services/watson-studio){: external}を作成します (アカウントに関連付けられているものがまだない場合)。

  ![Watson Studio](images/watson_studio.png)

- サービスに名前を付け、「Lite」(無料) プランを選択し、**「作成」**ボタンをクリックします。

### {{site.data.keyword.cos_full_notm}} サービスのプロビジョン
{: #crt-cos}

- [{{site.data.keyword.cos_short}} サービスをプロビジョンします](https://{DomainName}/catalog/services/cloud-object-storage){: external} (アカウントに関連付けられているものがまだない場合)。

  ![Object Storage](images/object_storage.png)

- サービスに名前を付け、「Lite」(無料) プランを選択し、**「作成」**ボタンをクリックします。

### {{site.data.keyword.pm_full}} サービスのプロビジョン
{: #crt-wml}

- [{{site.data.keyword.pm_short}} インスタンスをプロビジョンします](https://{DomainName}/catalog/services/machine-learning){: external} (アカウントに関連付けられているものがまだない場合)。

  ![Machine Learning](images/machine_learning.png)

- サービスに名前を付け、「Lite」(無料) プランを選択し、**「作成」**ボタンをクリックします。

### {{site.data.keyword.aios_full}} サービスのプロビジョン
{: #crt-wos-adv}

まだ {{site.data.keyword.aios_full}} をプロビジョンしていない場合は、確実にプロビジョンしてください。 

- [{{site.data.keyword.aios_short}} インスタンスをプロビジョンします](https://{DomainName}/catalog/services/watson-openscale){: external} (アカウントに関連付けられているものがまだない場合)。

  ![{{site.data.keyword.aios_short}} タイル](images/wos-cloud-tile.png)

1. **「カタログ」**>**「AI」**>**「{{site.data.keyword.aios_short}}」**をクリックします。
2. サービスに名前を付け、プランを選択し、**「作成」**ボタンをクリックします。
3. {{site.data.keyword.aios_short}} を開始するには、**「開始」**ボタンをクリックします。

### (オプション) Databases for PostgreSQL サービスまたは DB2 Warehouse サービスのプロビジョン
{: #crt-db2}

有料の {{site.data.keyword.cloud_notm}} アカウントを持っている場合、`Databases for PostgreSQL` サービスまたは `Db2 Warehouse` サービスをプロビジョンし、{{site.data.keyword.DSX}} サービスと統合して継続的な学習サービスを十分に活用できます。 有料サービスをプロビジョンしない場合、無料の内部 PostgreSQL ストレージを {{site.data.keyword.aios_short}} で使用できますが、ご使用のモデル向けに継続的な学習を構成することはできません。

- [Databases for PostgreSQL サービス](https://{DomainName}/catalog/services/databases-for-postgresql)または [Db2 Warehouse サービス](https://{DomainName}/catalog/services/db2-warehouse)をプロビジョンします (アカウントに関連付けられているものがまだない場合)。

  ![DB for Postgres](images/dbpostgres.png)

  ![Db2 Warehouse](images/db2_warehouse.png)

- サービスに名前を付け、Standard プラン (Databases for PostgreSQL) または Entry プラン (Db2 Warehouse) を選択し、**「作成」**ボタンをクリックします。

## {{site.data.keyword.DSX}} プロジェクトのセットアップ
{: #crt-set-wstudio}

- [{{site.data.keyword.DSX}} アカウント](https://dataplatform.ibm.com/){: external}にログインします。 {{site.data.keyword.avatar}} をクリックし、使用しているアカウントが {{site.data.keyword.cloud_notm}} サービスの作成に使用したアカウントと同じであることを確認します。

  ![同じアカウント](images/same_account.png)

- {{site.data.keyword.DSX}} で最初に新規プロジェクトを作成します。 「Create a project」を選択します。

  ![Watson Studio のプロジェクトの作成](images/studio_create_proj.png)

- プロジェクトを作成するため、**「Standard」**タイルを選択します。

  ![Watson Studio の「Standard」プロジェクトの選択](images/studio_create_standard.png)

- プロジェクトに名前と説明を入力します。**「Storage」**ドロップダウンで、作成した Cloud Object Storage サービスが選択されていることを確認し、**「Create」**をクリックします。

## {{site.data.keyword.pm_short}}モデルの作成とデプロイ
{: #crt-make-model}

### `Working with Watson Machine Learning` ノートブックを {{site.data.keyword.DSX}} プロジェクトに追加する
{: #crt-add-notebook}

- 以下のファイルをダウンロードします。

    - [Working with Watson Machine Learning](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb){: external}

- {{site.data.keyword.DSX}} プロジェクトの**「Assets」**タブで**「Add to project」**ボタンをクリックし、ドロップダウンから**「Notebook」**を選択します。

  ![接続の追加](images/add_notebook.png)

- **「From file」**を選択します。

  ![新規ノートブック・フォーム](images/new_notebook_name.png)

- 次に**「Choose file」**ボタンをクリックし、ダウンロードした「german_credit_lab.ipynb」ノートブック・ファイルを選択します。

  ![新規ノートブック・フォーム](images/new_notebook_name2a.png)

- **「Select runtime」**セクションで、「Python 3.5 with Spark」オプションを選択します。

- **「Create Notebook」**をクリックします。

### `Working with Watson Machine Learning` ノートブックの編集と実行
{: #crt-edit-notebook}

`Working with Watson Machine Learning` ノートブックには、実行する Python コードの各ステップの詳細な説明が記載されています。 ノートブックを進めるにあたり、時間をとって各コマンドの実行内容を理解してください。
{: tip}

- Watson Studio プロジェクトの**「Assets」**タブで `Working with Watson Machine Learning` ノートブックの横にある**「Edit」**アイコンをクリックし、このノートブックを編集します。

- 「Provision services and configure credentials」セクションで以下のように変更します。

    - 説明に従い、{{site.data.keyword.cloud_notm}} API キーを作成、コピー、および貼り付けします。

    - {{site.data.keyword.pm_full}} サービス資格情報を、以前に作成した資格情報に置き換えます。

    - DB 資格情報を、Databases for PostgreSQL のために作成した資格情報に置き換えます。

    - データマートとして無料の内部 PostgreSQL データベースを使用するように既に {{site.data.keyword.aios_short}} を構成している場合は、Databases for PostgreSQL サービスを使用する新しいデータマートに切り替えることができます。 古い PostgreSQL 構成を削除して新しい構成を作成するには、KEEP_MY_INTERNAL_POSTGRES 変数に `False` を設定します。

        ノートブックにより既存の内部 PostgreSQL データマートが削除され、提供された DB 資格情報を使用して新しいデータマートが作成されます。 **データ・マイグレーションは行われません**。
        {: important}

- サービスをプロビジョンし、資格情報を入力したら、ノートブックを実行できる状態になります。 **「Kernel」**メニュー項目をクリックし、メニューから**「Restart & Clear Output」**を選択します。

  ![再始動してクリア](images/restart_and_clear.png)

- 次に、ノートブックの各ステップを順に実行します。 各ステップの処理内容が説明されているとおりであることを確認します。 「Additional data to help debugging」セクションのステップまでのすべてのステップを実行します。

最終的には、**Spark German Risk Deployment** モデルが作成およびトレーニングされ、{{site.data.keyword.aios_short}} サービス・インスタンスにデプロイされます。 {{site.data.keyword.aios_short}} は、このモデルで性別 (この例では Female) または年齢 (この例では 18 から 25 歳) に対するバイアスがあるかを調べるように構成されます。

## 結果の表示
{: #crt-view-results}

### デプロイメントに関するインサイトの表示
{: #crt-view-insights}

[{{site.data.keyword.aios_short}} ダッシュボード](https://aiopenscale.cloud.ibm.com/aiopenscale/){: external}を使用して**「インサイト」**タブをクリックします。

  ![インサイト](images/insight-dash-tab.png)

「インサイト」ページには、デプロイ済みモデルの指標の概要が表示されます。 ノートブックの実行時に設定したしきい値を超えている公平性または正解率の指標の警告を簡単に確認できます。 このチュートリアルで使用するデータと設定により、以下のような正解率と公平性の指標が作成されます。

  ![「インサイト」の概要](images/insight-overview-adv-tutorial-2.png)

### デプロイメントのモニタリング・データの表示
{: #crt-view-mon-data}

1. モニタリングの詳細を表示するには、**「インサイト」**ページでデプロイメントに対応するタイルをクリックします。 そのデプロイメントのモニタリング・データが表示されます。 
2. グラフの上でマーカーをスライドさせ、特定の 1 時間枠のデータを選択します。 
3. **「詳細を表示します」**リンクをクリックします。

  ![モニター・データ](images/insight-monitor-data2.png)

これで、モニターしたデータのグラフを確認できます。 この例では、「Sex」特徴量において、`female` グループが好ましい結果 (「No Risk」) になる確率 (68%) は `male` グループ (78%) より低いことがわかります。

  ![「インサイト」の概要](images/insight-review-charts2.png)

### モデル・トランザクションの説明性の表示
{: #crt-view-explain}

デプロイメントごとに、特定のトランザクションについての説明性データを表示することができます。

確認するトランザクションが既に分かっている場合、トランザクション ID を使用して簡単に確認できます。 デプロイメント・タイルをクリックした後で、ナビゲーターで**「トランザクションの説明」**![「トランザクションの説明」タブ](images/insight-transact-tab.png) アイコンをクリックし、トランザクション ID を入力して、**Enter** キーを押します。
{: tip}

PostgreSQL の内部ライト・バージョンを使用している場合は、データベース資格情報を取得できない可能性があります。 これが原因で、トランザクションを表示できないことがあります。
{: note}

1. バイアスがある最新データのグラフで**「トランザクションの表示」**ボタンをクリックします。

  ![トランザクションの表示](images/view_transactions.png)

  デプロイメントがバイアス挙動を示すトランザクションが表示されます。 
  
2. いずれかのトランザクションを選択し、**「アクション」**列で**「説明」**リンクをクリックします。

  ![トランザクション・リスト](images/transaction_list_cr.png)

モデルがこの結論に達した理由の説明 (モデルの確信度、確信度レベルに貢献した要因、モデルに取り込まれた属性など) が表示されます。

  ![トランザクションの表示](images/view_transaction_cr.png)
  
## 次のステップ
{: #crt-next-steps}

- 詳しくは、[データの表示と解釈](/docs/services/ai-openscale?topic=ai-openscale-it-ov)および[説明性のモニター](/docs/services/ai-openscale?topic=ai-openscale-ie-ov)を参照してください。
