---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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

このチュートリアルでは、必要な {{site.data.keyword.Bluemix_notm}} サービスのプロビジョン方法、Watson Studio でのプロジェクトのセットアップとサンプル・モデルのデプロイ方法、および {{site.data.keyword.aios_short}} でのモニタリングの構成方法を説明します。
{: shortdesc}

1. [{{site.data.keyword.Bluemix_notm}} 機械学習およびストレージ・サービスをプロビジョンします](/docs/services/ai-openscale?topic=ai-openscale-gs-obj#gs-prps)。
2. [Watson Studio プロジェクトをセットアップして、機械学習モデルを作成、トレーニング、およびデプロイします](/docs/services/ai-openscale?topic=ai-openscale-gs-obj#gs-setup)。
3. [モデルの信頼性、透明性、および説明性を構成して検討します](/docs/services/ai-openscale?topic=ai-openscale-gs-obj#gs-confaios)。

## 前提条件の {{site.data.keyword.Bluemix_notm}} サービスのプロビジョン
{: #gs-prps}

このチュートリアルを完了するには、{{site.data.keyword.aios_short}} に加えて、以下のアカウントとサービスが必要です。

**重要**: 最高のパフォーマンスを得るために、前提条件のサービスを {{site.data.keyword.aios_short}} と同じ地域に作成することをお勧めします。 {{site.data.keyword.aios_short}} の使用可能なロケーションを表示するには、[サービス可用性](/docs/resources?topic=resources-services_region){: external}を参照してください。

1.  {{site.data.keyword.ibmid}} を使用して、[{{site.data.keyword.Bluemix_notm}} アカウント](https://{DomainName}){: external} にログインします。
1.  以下のサービスのうち、アカウントにまだ関連付けられていないサービスについては、それぞれリンクをクリックし、サービスに名前を付け、**ライト** (無料) プランを選択し、**「作成」**ボタンをクリックして、インスタンスを作成します。

    - [{{site.data.keyword.DSX}}](https://{DomainName}/catalog/services/watson-studio){: external}

      ![Watson Studio](images/wos-watson_studio.png)

    - [{{site.data.keyword.pm_full}}](https://{DomainName}/catalog/services/machine-learning){: external}

      ![Machine Learning](images/machine_learning.png)

    - [Object Storage](https://{DomainName}/catalog/services/cloud-object-storage){: external}

      ![Object Storage](images/object_storage.png)


## Watson Studio プロジェクトのセットアップ
{: #gs-setup}

1.  [Watson Studio アカウント](https://dataplatform.ibm.com/){: external}にログインし、最初に新規プロジェクトを作成します。 **「プロジェクトの作成 (Create a project)」**をクリックします。

    ![Watson Studio のプロジェクトの作成](images/studio_create_proj.png)

1.  **「空のプロジェクトの作成 (Create an empty project)」**タイルをクリックします。
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

    ![credit risk タイルが示されています](images/credit-sample-model.png)

### `Credit Risk` モデルのデプロイ
{: #gs-depmod}

1.  `Credit Risk` モデルのページで、**「Deployments」**タブをクリックして、**「Add Deployment」**をクリックします。
1.  デプロイメントの名前として `credit-risk-deploy` を入力し、**「Web service」**デプロイメント・タイプを選択します。
1.  **「保存」**をクリックします。

## {{site.data.keyword.aios_short}} の構成
{: #gs-confaios}

機械学習モデルがデプロイされたので、次に、モデルの信頼性と透明性を確保するために {{site.data.keyword.aios_short}} を構成します。

### {{site.data.keyword.aios_short}} のプロビジョン
{: #gs-provaios}

1.  [新規 {{site.data.keyword.aios_short}} サービス・インスタンスをプロビジョンします](https://{DomainName}/catalog/services/watson-openscale){: external}

    ![{{site.data.keyword.aios_short}}](images/wos-cloud-tile.png)

2.  サービスに名前を付け、**ライト・プラン**を選択して、**「作成」**をクリックします。

1.  {{site.data.keyword.aios_short}} インスタンスの**「管理」**タブを選択し、**「アプリケーションの起動 (Launch application)」**ボタンをクリックします。 **「{{site.data.keyword.aios_short}} へようこそ」**デモ・ページが開きます。
2. このチュートリアルでは、**「実行しない」**をクリックします。

### データベースの選択
{: #gs-db-choice}

次に、データベースを選択する必要があります。 無料のデータベースと、既存または新規のデータベースという 2 つのオプションがあります。

2. このチュートリアルでは、**「無料のライト・プラン・データベースを使用する」**タイルを選択します。

   無料のデータベースには、いくつかの重要な制限事項があります。 これはホストされたデータベースであり、ユーザーにこのデータベースへ別途直接アクセスする権限は与えられていません。 データベースとデータへのアクセス権は、{{site.data.keyword.aios_short}} に対して付与されます。 このデータベースは GDPR に準拠していません。 これらの各オプションについて詳しくは、[データベースの指定](/docs/services/ai-openscale?topic=ai-openscale-connect-db)のトピックを参照してください。 既存のデータベースとしては、PostgreSQL データベースまたは Db2 データベースを選択できます。
    {: tip}

   ![データベースの選択](images/gs-set-lite-db2.png)

1.  要約データを確認し、**「保存」**をクリックします。 それを確定し、プロンプトが表示されたら**「構成を続行する (Continue with Configuration)」**ボタンをクリックします。

    データマート ID もリストされていますが、これは {{site.data.keyword.aios_short}} インスタンス ID と同じです。
    {: tip}

    ![要約の確認](images/gs-setup-summary4.png)

1.  以下の画面キャプチャーに類似した画面が表示されます。 データの評価に GUI 方式を使用するため、**「モニターの構成」**ボタンを選択するだけでこのセットアップは完了します。

    ![評価要求コード](images/gs-config-send-scoring.png)

### {{site.data.keyword.aios_short}} の機械学習モデルへの接続
{: #gs-ctmod}


1.  **「Watson Machine Learning」**タイルをクリックしてから、**「保存」**をクリックします。

1.  このチュートリアルでは、メニューから {{site.data.keyword.pm_full}} インスタンスを選択し、**「次へ」**をクリックします。

    別の {{site.data.keyword.pm_short}} の場所を選択することもできます。 詳しくは、[{{site.data.keyword.pm_full}} サービス・インスタンスの指定](/docs/services/ai-openscale?topic=ai-openscale-wml-connect)を参照してください。
    {: note}

    ![{{site.data.keyword.pm_short}} インスタンスの設定](images/gs-set-wml.png)

これで、{{site.data.keyword.aios_short}} によってモニターされるデプロイ済みモデルを選択できます。 


### モデルに一連のサンプル・データを入力する
{: #gs-samp}

モニターを構成するには、その前にモデルに対する評価要求を少なくとも 1 つ生成して、モニターで取り込むことができるペイロード・ロギングを生成する必要があります。 このセクションでは、JSON ファイル形式でサンプル・データを Watson Studio に提供し、スコアリング要求を生成します。

1.  [credit_payload_data.json](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/credit_payload_data.json) ファイルをダウンロードします。

1.  Watson Studio プロジェクトの**「デプロイメント」**タブから **credit-risk-deploy** リンクをクリックし、**「テスト」**タブをクリックしてから JSON 入力アイコンを選択します。

    ![JSON テスト](images/json_test02.png)

1.  今度は、ダウンロードした `credit_payload_data.json` ファイルを開き、その内容を**「Test」**タブの JSON フィールドにコピーします。 **「Predict」**ボタンをクリックして、訓練ペイロードをモデルに送信し、評価を実行します。

    ![JSON 予測](images/json_test03.png)

## 次のステップ
{: #gs-next-steps-config}

このチュートリアルを続行するため、以下のステップを実行します。

1. [デプロイメントのモニタリングを準備します](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-select-deploy)。

   モニタリングを準備するには、デプロイ済みモデルの 1 つを選択してダッシュボードに追加する必要があります。**「インサイト」**タブでデプロイメント・タイルをクリックするか、または**「ダッシュボードに追加」**ボタンをクリックしてデプロイメント・モデルを選択し、**「構成」**をクリックします。

2. [ペイロードのロギングをセットアップします](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-work-data)。

   **「ペイロードのロギング」**セクションで入力タイプを指定する必要があります。

3. [モデルの詳細を設定します](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-work-model-dets)。

   **「モデルの詳細」**セクションで、モデルの詳細を記録する必要があります。このチュートリアルでは、**「モニタリングの手動構成」**を選択します。

4. [品質モニタリングを構成します](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor)。

   **「品質」**セクションで、品質警告しきい値とサンプル・サイズを設定します。

5. [公平性モニタリングを構成します](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)。

   **「公平性」**セクションで、公平性をモニタリングする特徴量を選択します。選択した特徴量ごとに、{{site.data.keyword.aios_short}} は、デプロイ済みモデルが一方のグループに対して他方のグループより好ましい結果を出す傾向をモニターします。 特徴量は個々にモニタリングされますが、バイアス緩和ではすべての特徴量の問題がまとめて訂正されます。

6. [ドリフト検出モニタリングを構成します](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-config)。

   **「ドリフト (Drift)」**セクションで、ドリフト検出モデルをセットアップします。
   
5. [モデルに一連のサンプル・フィードバック・データを入力します](/docs/services/ai-openscale?topic=ai-openscale-fmt-upld-fdbk-data#fmt-upld-fdbk-data-upld-csv)。

   品質のモニタリングを有効にするには、モデルにフィードバック・データを入力する必要があります。それを行わないと、ダッシュボードに品質データが表示されません。予測用にモデルにサンプル・フィードバック・データを追加すると、すぐにすべてのリクエストを生成できます。 このタスクのために、サンプル・フィードバック・データが含まれる CSV ファイルをダウンロードします。

6. [インサイトを取得します](/docs/services/ai-openscale?topic=ai-openscale-io-ov)。

   正解率モニタリングを構成すると、1 時間後に正解率検査が実行されます。 実動システムでは、その期間にダッシュボードでフィードバック・データを累積できるので、この設定は理にかなっています。 このチュートリアルの場合、フィードバック・データの追加後に手動で正解率検査をトリガーして、**「インサイト」**ダッシュボードで結果を確認することもできます。

   結果をすぐに確認するには、**「インサイト」**ページからデプロイメントを選択してから、**「品質」**指標のいずれかを選択し、**「今すぐ品質を評価」**をクリックします。
