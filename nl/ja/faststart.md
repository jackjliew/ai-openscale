---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: ai, getting started, tutorial, understanding, fast start

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

# 対話式セットアップのチュートリアル
{: #gs-obj}

このチュートリアルでは、以下のステップを実行します。

- [{{site.data.keyword.Bluemix_notm}} の機械学習サービスとストレージ・サービスをプロビジョンします](/docs/services/ai-openscale?topic=ai-openscale-gs-obj&locale=en-US#gs-prps)。
- [Watson Studio プロジェクトをセットアップして、機械学習モデルを作成、トレーニング、およびデプロイします](/docs/services/ai-openscale?topic=ai-openscale-gs-obj&locale=en-US#gs-setup)。
- [モデルの信頼性、透明性、および説明性を構成して検討します](/docs/services/ai-openscale?topic=ai-openscale-gs-obj&locale=en-US#gs-confaios)。

## 前提条件の {{site.data.keyword.Bluemix_notm}} サービスのプロビジョン
{: #gs-prps}

このチュートリアルを完了するには、{{site.data.keyword.aios_short}} に加えて、以下のアカウントとサービスが必要です。

**重要**: 最高のパフォーマンスを得るために、前提条件のサービスを {{site.data.keyword.aios_short}} と同じ地域に作成することをお勧めします。 {{site.data.keyword.aios_short}} の使用可能なロケーションを表示するには、[サービス可用性](/docs/resources?topic=resources-services_region)を参照してください。

1.  {{site.data.keyword.ibmid}} を使用して、[{{site.data.keyword.Bluemix_notm}} アカウント](https://{DomainName}){: external} にログインします。
1.  以下のサービスのうち、アカウントにまだ関連付けられていないサービスについては、それぞれリンクをクリックし、サービスに名前を付け、**ライト** (無料) プランを選択し、**「作成」**ボタンをクリックして、インスタンスを作成します。

    - [{{site.data.keyword.DSX}}](https://{DomainName}/catalog/services/watson-studio){: external}

      ![Watson Studio](images/watson_studio.png)

    - [{{site.data.keyword.pm_full}}](https://{DomainName}/catalog/services/machine-learning){: external}

      ![Machine Learning](images/machine_learning.png)

    - [Object Storage](https://{DomainName}/catalog/services/cloud-object-storage){: external}

      ![Object Storage](images/object_storage.png)


## Watson Studio プロジェクトのセットアップ
{: #gs-setup}

1.  [Watson Studio アカウント](https://dataplatform.ibm.com/){: external}にログインし、最初に新規プロジェクトを作成します。 **「New project」**を選択します。

    ![Watson Studio のプロジェクトの作成](images/studio_create_proj.png)

1.  **「Standard」**タイルを選択します。

    ![Watson Studio の「Standard」プロジェクトの選択](images/studio_create_standard.png)

1.  プロジェクトに名前と説明を入力し、**「Storage」**メニューで、前のステップで作成した Object Storage サービスが選択されていることを確認し、**「Create」**をクリックします。

### {{site.data.keyword.Bluemix_notm}} サービスと Watson プロジェクトの関連付け
{: #gs-assoc}

1.  Watson Studio プロジェクトを開き、**「Settings」**タブを選択します。 **「Associated Services」**セクションで、**「Add service」**をクリックして**「Watson」**をクリックします。

    ![Watson サービスの追加](images/add_watson_service.png)

1.  **「Machine Learning」**タイルの**「Add」**リンクをクリックします。
2.  **「Existing」**タブの**「Existing Service Instance」**ドロップダウンで、前に作成したサービスをクリックします。
3. **「Select」**をクリックします。

### `Credit Risk` モデルの追加
{: #gs-addmod}

1.  {{site.data.keyword.DSX}} で、プロジェクトの**「Assets」**タブを選択して、**「Watson Machine Learning Models」**セクションまでスクロールし、**「New Watson Machine Learning model」**ボタンをクリックします。

1.  **「Select model type」**セクションで、**「From sample」**と `Credit Risk` モデルを選択して、**「Create」**をクリックします。

    ![新規ノートブック・フォーム](images/credit-sample-model.png)

### `Credit Risk` モデルのデプロイ
{: #gs-depmod}

1.  `Credit Risk` モデルのページで、**「Deployments」**タブをクリックして、**「Add Deployment」**をクリックします。
1.  デプロイメントの名前として `credit-risk-deploy` を入力し、**「Web service」**デプロイメント・タイプを選択します。
1.  **「保存」**をクリックします。

## {{site.data.keyword.aios_short}} の構成
{: #gs-confaios}

### {{site.data.keyword.aios_short}} のプロビジョン
{: hide-dashboard}
{: #gs-provaios}

1.  [新規 {{site.data.keyword.aios_short}} サービス・インスタンスをプロビジョンします](https://{DomainName}/catalog/services/watson-openscale){: external}

    ![{{site.data.keyword.aios_short}}](images/openscale.png)

2.  サービスに名前を付け、**ライト・プラン**を選択して、**「作成」**をクリックします。

### {{site.data.keyword.aios_short}} の機械学習モデルへの接続
{: #gs-ctmod}

機械学習モデルがデプロイされているので、モデルの信頼性と透明性を確保するために {{site.data.keyword.aios_short}} を構成できます。

1.  {{site.data.keyword.aios_short}} インスタンスの**「管理」**タブを選択し、**「アプリケーションの起動 (Launch application)」**ボタンをクリックします。 **「{{site.data.keyword.aios_short}} へようこそ」**デモ・ページが開きます。
2. このチュートリアルでは、**「実行しない」**をクリックし、**「開始」**をクリックします。

1.  **「Watson Machine Learning」**タイルをクリックします。

1.  このチュートリアルでは、メニューから {{site.data.keyword.pm_full}} インスタンスを選択し、**「次へ」**をクリックします。

    別の {{site.data.keyword.pm_short}} の場所を選択することもできます。 詳しくは、[{{site.data.keyword.pm_full}} サービス・インスタンスの指定](/docs/services/ai-openscale?topic=ai-openscale-wml-connect)を参照してください。
    {: note}

    ![{{site.data.keyword.pm_short}} インスタンスの設定](images/gs-set-wml.png)

1.  これで、{{site.data.keyword.aios_short}} によってモニターされるデプロイ済みモデルを選択できます。 作成したデプロイ済みモデルを選択し、**「次へ」**をクリックします。

    ![デプロイ済みモデルの選択](images/gs-set-deploy0.png)

1.  次に、データベースを選択する必要があります。 無料のデータベースと、既存または新規のデータベースという 2 つのオプションがあります。 このチュートリアルでは、**「{{site.data.keyword.aios_short}} によってホストされている無料のデータベースを使用する (Use the free database hosted by Watson OpenScale)」**タイルを選択します。

    無料のデータベースには、いくつかの重要な制限事項があります。 これはホストされたデータベースであり、ユーザーにこのデータベースへ別途直接アクセスする権限は与えられていません。 データベースとデータへのアクセス権は、{{site.data.keyword.aios_short}} に対して付与されます。 このデータベースは GDPR に準拠していません。 これらの各オプションについて詳しくは、[データベースの指定](/docs/services/ai-openscale?topic=ai-openscale-connect-db)のトピックを参照してください。 既存のデータベースとしては、PostgreSQL データベースや Db2 データベースを選択できます。
    {: tip}

    ![データベースの選択](images/gs-set-lite-db2.png)

1.  要約データを確認し、**「保存」**をクリックします。 それを確定し、プロンプトが表示されたら**「構成を続行する (Continue with Configuration)」**ボタンをクリックします。

    データマート ID もリストされていますが、これは {{site.data.keyword.aios_short}} インスタンス ID と同じです。
    {: tip}

    ![要約の確認](images/gs-setup-summary4.png)

1.  以下の画面キャプチャーに類似した画面が表示されます。 データの評価に GUI 方式を使用するため、**「モニターの構成」**ボタンを選択するだけでこのセットアップは完了します。

    ![評価要求コード](images/gs-config-send-scoring.png)

### モデルに一連のサンプル・データを入力する
{: #gs-samp}

モニターを構成するには、その前にモデルに対する評価要求を少なくとも 1 つ生成して、モニターで取り込むことができるペイロード・ロギングを生成する必要があります。 このセクションでは、JSON ファイル形式でサンプル・データを提供し、評価要求を生成します。

1.  [credit_payload_data.json](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/credit_payload_data.json) ファイルをダウンロードします。

1.  Watson Studio プロジェクトの**「デプロイメント」**タブから **credit-risk-deploy** リンクをクリックし、**「テスト」**タブをクリックしてから JSON 入力アイコンを選択します。

    ![JSON テスト](images/json_test02.png)

1.  今度は、ダウンロードした `credit_payload_data.json` ファイルを開き、その内容を**「Test」**タブの JSON フィールドにコピーします。 **「Predict」**ボタンをクリックして、訓練ペイロードをモデルに送信し、評価を実行します。

    ![JSON 予測](images/json_test03.png)

### モニタリングのための準備
{: #gs-prepmon}

1.  ここで、{{site.data.keyword.aios_short}} インスタンスでデプロイメントを選択し、**「開始」**をクリックします。

    ![デプロイメントの選択](images/config-select-deploy2.png)

1.  モデルが予測する答えが含まれる特徴量を指定します (データベースで表のどの列に予測値またはラベルが含まれるか)。 この場合、モデルは信用リスクを予測するので、**「Risk」**列を選択し、**「次へ」**をクリックします。

    ![モニタリングのための準備](images/config-prep-monitor.png)

1.  次に、モデルと訓練データに関する情報を入力します。 **「次へ」**をクリックします。

    ![説明の準備](images/config-what-monitor.png)

1.  **「データ・タイプ」**メニューでデプロイメントで分析するデータのタイプとして**「数値/カテゴリカル」**を選択し、**「次へ」**をクリックします。

    ![入力タイプの選択](images/config-input-monitor.png)

1.  数値データまたはカテゴリカル・データの場合、モニターを構成するためにはモデルの訓練データに関する情報を入力する必要があります。 **「モニターの手動構成」**を選択して、訓練データの接続情報を入力します。

    ![構成タイプの選択](images/config-manual-monitor.png)

1.  「正解率」など、モデルの指標をモニターするアルゴリズム・タイプは重要です。 このモデルで行える予測は「Risk」または「No Risk」なので、[「アルゴリズムのタイプ」](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-understand)には**「二項分類」**を選択し、**「次へ」**をクリックします。

    ![2 項](images/binary.png)

1.  サンプル・データのロケーション情報は、以下の画面で事前に入力されています。 **「次へ」**を選択して先に進みます。

    ![訓練データの Db2 ロケーションを指定するページ](images/gs-config-train-db2-monitor.png)

1.  スキーマと表も事前に入力されています。 **「次へ」**をクリックして先に進みます。

    ![スキーマと訓練テーブルが配置されている Db2 の場所の指定](images/gs-fair-config-table-db2.png)

1.  今度は、モデルが予測する答えが含まれる特徴量 (つまり、データベースで表のどの列に予測値 (ラベル) が含まれるか) を指定する必要があります。 この場合、モデルは信用リスクを予測するので、**「Risk」**列を選択し、**「次へ」**をクリックします。

    訓練データベースには、モデルを訓練するためにユーザーが入力した値があります。
    {: note}

    ![予測ラベルの入力](images/gs-config-label.png)

1.  モデルのトレーニングに使用する列を選択します。 これは、リクエストでモデル・デプロイメントが予期するデータです。 `_training` を除くすべてのデータ列は、モデルに対する入力データです。 他のすべての入力を選択し、**「次へ」**をクリックします。

    ![説明性の入力](images/explain_inputs1.png)

1.  カテゴリカル・データでは、元の値はテキスト値で今は整数になっている列を指定する必要があります。 以下に示すように、値を選択します。

    ![説明性の入力](images/config_categories.png)

1.  選択内容の要約を確認し、**「保存」**をクリックしてから**「OK」**をクリックします。

### 公平性モニタリングの構成
{: #gs-cfgfair}

1.  **「公平性」**をクリックします。

1.  公平性についての説明を読み、**「次へ」**をクリックします。 詳しくは、[公平性](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)を参照してください。

1.  どの特徴量で公平性をモニターするかを選択できるようになりました。 選択した特徴量ごとに、{{site.data.keyword.aios_short}} は、デプロイ済みモデルが一方のグループに対して他方のグループより好ましい結果を出す傾向をモニターします。 この例では**「Sex」**特徴量と**「Age」**特徴量をモニターします。

    特徴量は個々にモニターされますが、バイアス緩和では、すべての特徴量の問題が一緒に訂正されます。 **「Sex」**と**「Age」**タイルをクリックし、**「次へ」**をクリックします。

1.  {{site.data.keyword.aios_short}} は、参照グループと比較したモニター対象グループのバイアスを検出します。 **「Sex」**特徴量については、**「参照グループ」**に値 `male` を追加し、**「モニター対象グループ」**に値 `female` を追加してから、**「次へ」**をクリックします。

    モニター対象グループに対する「Risk」予測値比率が参照グループの比率と異なっている場合、モデルには、**「Sex」**に関してバイアスがあることを示すフラグが立てられます。 つまり、リスクありと予測する確率が男性顧客では 60% 、女性顧客では 20% であるモデルには、バイアスがあります。

    ![性別グループ](images/gender_groups1.png)

1.  **「Sex」**に対する公平性しきい値を割り当てます。 公平性の評価が、設定したしきい値を超えると、運用ダッシュボードに警告が表示されます。 しきい値を 90% に設定し、**「次へ」**をクリックします。

1.  **「Age」**特徴量については、**「参照グループ」**に値 `26-74` を追加し、**「モニター対象グループ」**に値 `19-25` を追加してから、**「次へ」**をクリックします。

    **「Sex」**同様、モニター対象グループに対する「Risk」予測値比率が参照グループの比率と異なっている場合、モデルには、**「Age」**に関してバイアスがあることを示すフラグが立てられます。 つまり、26 歳から 74 歳の顧客に対する「Risk」予測値比率が、19 歳から 25 歳の顧客の比率と異なっている場合、そのモデルにはバイアスがあります。

    ![BP グループ](images/age_groups.png)

1.  **「Age」**のしきい値を 90% に設定し、**「次へ」**をクリックします。

1.  **「訓練データの値」**フィールドから**「好ましい値」**フィールドと**「好ましくない値」**フィールドに、値をドラッグ・アンド・ドロップします。 このチュートリアルでは、好ましい値は**「No Risk」**で、好ましくない値は**「Risk」**です。 **「次へ」**をクリックします。

    {{site.data.keyword.aios_short}} は、ペイロード・ロギング・データベースのどの列に予測値が入っているかを自動的に検出し、それを**「訓練データの値」**フィールドに表示します。 モデルの訓練用に提供した値は訓練データベースに入りますが、モデルの実行時に収集されたフィードバック・データはペイロード・ロギング・データベースに入るので、そのデータをオプションで使用してモデルを再度訓練し、再デプロイすることもできます。
    {: note}

    ![肯定の値と否定の値](images/pos_and_neg2.png)

1.  スライダーを使用して最小サンプル・サイズを 100 に調整し、**「次へ」**をクリックします。

    ![最小サイズ](images/gs-fair-config-sample.png)

    このチュートリアルでは、最小サンプル・サイズは 100 に設定されます。 通常、これより大きなサンプル・サイズを設定してサンプル・サイズが小さくなりすぎないようにすることが推奨されます。サイズが小さいと、結果にゆがみが出やすくなります。
    {: note}

1.  選択を確認し、**「保存」**をクリックしてから**「OK」**をクリックします。

    ![構成の要約](images/fair-summary.png)

    バイアスが排除された予測エンドポイントを示す以下のウィンドウが表示されます。 このチュートリアルではデータの評価に GUI 方式を使用し、CLI は使用しないので、先に進むには**「OK」**をクリックします。

    ![バイアス緩和 API](images/gs-insight-debias-api.png)

### 正解率モニタリングの構成
{: #gs-cfgac}

1.  **「正解率」**をクリックします。

1.  正解率についての説明を読み、**「次へ」**をクリックします。 詳しくは、[正解率](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor)を参照してください。

1.  正解率の警告しきい値を 90% に設定し、**「次へ」**をクリックします。

1.  次の画面で、スライダーを使用して最小サンプル・サイズを 10 に調整し、**「次へ」**をクリックします。

    このチュートリアルでは、最小サンプル・サイズは 10 に設定されています。 通常、これより大きなサンプル・サイズを設定してサンプル・サイズが小さくなりすぎないようにすることが推奨されます。サイズが小さいと、結果にゆがみが出やすくなります。
    {: note}

1.  最大サンプル・サイズには 10000 を使用します。 **「次へ」**をクリックします。

1.  選択を確認し、**「保存」**をクリックしてから**「OK」**をクリックします。

1.  最後に、フィードバック・データを追加するかどうかのオプションが表示されます。フィードバック・データについては次のセクションで取り上げます。 今回は**「フィードバック・データの追加」**ボタンをクリックしないで**「OK」**をクリックし、ウィンドウを閉じます。

    詳しくは、[正解率モニターの構成](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-config)を参照してください。

## モデルに一連のサンプル・フィードバック・データを入力する
{: #gs-smpfeed}

正解率のモニタリングを有効にするには、モデルにフィードバック・データを入力する必要があります。 それを行わないと、ダッシュボードに正解率データが表示されません。 予測用にモデルにサンプル・フィードバック・データを追加すると、すぐにすべてのリクエストを生成できます。 このタスクのために、サンプル・フィードバック・データが含まれる CSV ファイルをダウンロードします。

1.  [credit_feedback_data.csv](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/credit_feedback_data.csv) ファイルをダウンロードします。

1.  {{site.data.keyword.aios_short}} で、**「インサイト」**タブをクリックします。

    ![インサイト](images/insight-dash-tab.png)

1.  デプロイ済みモデルのタイルをクリックします。

    ![「インサイト」タブ - データなし](images/gs-insight-overview.png)

1.  次に、「編集」アイコンをクリックしてデプロイメント構成を編集します。

    ![編集アイコンの表示](images/gs-insight-edit-icon.png)

1.  「要約」サイド・パネルで、** 「フィードバック・データの追加」 **  ボタンをクリックし、ダウンロードした  `credit_feedback_data.csv`  ファイルを選択します。 **「コンマ (,)」**区切り文字を選択し、**「OK」**をクリックします。

    現在、ファイルのサイズは 8 MB に制限されています。
    {: note}

    ![正解率の区切り文字](images/accuracy-delimit.png)

    CSV ファイルを追加することで、モデルにフィードバック・データが追加されます。

    ![「要約」パネル](images/gs-insight-summary-panel-2.png)

## 結果の表示
{: #gs-viewres}

正解率モニタリングを構成すると、1 時間後に正解率検査が実行されます。 実動システムでは、その期間にダッシュボードでフィードバック・データを累積できるので、この設定は理にかなっています。 このチュートリアルの場合、フィードバック・データの追加後に手動で正解率検査をトリガーして、**「インサイト」**ダッシュボードで結果を確認することもできます。

結果をすぐに確認するには、**「インサイト」**ページからデプロイメントを選択してから、**「今すぐ公平性を評価」**ボタンまたは**「今すぐ品質を評価」**ボタンをクリックします。

### デプロイメントに関するインサイトの表示
{: #gs-viewin}

1. [{{site.data.keyword.aios_short}} ダッシュボード](https://aiopenscale.cloud.ibm.com/aiopenscale/){: external} で、**「インサイト」**タブをクリックします。

  ![インサイト](images/insight-dash-tab.png)

1. 「インサイト」ページを表示して、デプロイ済みモデルの指標の概要を確認します。 90% のしきい値を超える公平性または正解率の指標の警告を表示できます。

  公平性と正解率の指標は、表示されるまで最大 1 時間かかることがあります。
  {: tip}

  ![「インサイト」の概要](images/insight-overview.png)

### デプロイメントのモニタリング・データの表示
{: #gs-viewmon}

1.  「インサイト」ページのタイルをクリックして、デプロイメントを選択します。 そのデプロイメントのモニタリング・データが表示されます。 注記: フィードバックの .csv ファイルをアップロードした後に、公平性や正解率のデータが更新されていないことに気付くことがあります。 結果をすぐに確認するには、**「今すぐ公平性を評価」**ボタンまたは**「今すぐ品質を評価」**ボタンをクリックします。
1.  グラフの上でマーカーをスライドさせ、サンプル・データとサンプル・フィードバック・データを実行した時間フレームのデータを選択します。 その後、**「詳細を表示します」**をクリックします。

    ![モニター・データ](images/insight-monitor-data.png)

1.  次に、モニターしたデータのグラフを確認します。 この例では、モニターしたデータに関する詳細を表示するために、**「特徴量」**メニューを使用して `Age` または `Sex` のいずれかを選択します。

    これらのグラフの読み方について詳しくは、[特定の時間のデータの視覚化](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet)を参照してください。
    {: tip}

    ![「洞察」の概要](images/insight-review-charts.png)

### モデル・トランザクションの説明性の表示
{: #gs-viewextx}

1.  モニターしたデータのグラフにある**「トランザクションの表示」**ボタンをクリックします。

    ![トランザクションの表示](images/view_transactions.png)

1.  過去 1 時間にバイアスの原因となったトランザクションのリストが表示されます。 特定のトランザクションの詳細な説明を表示するには、**「アクション」**列で**「説明」**をクリックします。

    ![トランザクション・リスト](images/transaction_list_cr.png)
    
1.  モデルがこの結論に達した理由を示す説明が表示されます。 この説明には、モデルの確信度、確信度レベルに貢献した要因、モデルに取り込まれた列などが含まれます。

    ![トランザクションの表示](images/view_transaction1.png)

## 関連情報
{: #wos-info}

- バイアスについては、[公平性](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mf-monitor)を参照してください。
- モデルの予測結果の精度については、[正解率](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-acc-monitor)を参照してください。
- グラフ、データ、およびトランザクションの解釈については、[公平性、分当たりの平均リクエスト数、および正解率のモニター](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart)を参照してください。
