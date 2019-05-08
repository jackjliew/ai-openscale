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
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Watson Machine Learning 以外のサービス・インスタンスに関するペイロード・ロギング
{: #cml-ml}

Watson Machine Learning (WML) 以外の機械学習エンジン内で AI モデルがデプロイされている場合は、Python クライアントで外部機械学習エンジンに関するペイロード・ロギングを有効にしなければなりません。
{: shortdesc}

完全な情報については、[{{site.data.keyword.aios_short}} Python クライアントの資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://ai-openscale-python-client.mybluemix.net/){: new_window} を参照してください。また、[{{site.data.keyword.aios_short}} チュートリアル ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/README.md){: new_window} の一部であるサンプルの {{site.data.keyword.aios_short}} Python クライアント・ノートブックも参照してください。

## 始める前に
{: #cml-prereq}

ご使用のモデルを対象にバイアスをモニターするには、Db2 または Cloud Object Storage でそのモデルのトレーニング・データを使用できるようにする必要があります。Python 関数に関する説明可能性と正確度はサポートされていません。

- {{site.data.keyword.aios_short}} をインポートして開始します

    ```python
    from ibm_ai_openscale import APIClient

    aios_credentials = {
      "instance_guid": "***",
      "url": "https://api.aiopenscale.cloud.ibm.com",
      "apikey": "***"
    }

    client = APIClient(service_credentials)
    ```
  「[資格情報の作成](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-cred-creds)」のトピックで示されている手順に従うと、資格情報を見つけることができます。

- PostgreSQL データベース内でスキーマ名を作成します

- データマートをセットアップします

    ```python
    client.data_mart.setup(db_credentials=postgres_credentials, schema=schemaName)

    client.data_mart.get_details()
    ```

## カスタムの機械学習エンジンの処理
{: #cml-custom}

### カスタムの機械学習エンジンのバインド
{: #cml-cusbind}

- WML 以外のエンジンをカスタムとしてバインドします。この場合、単なるメタデータということになり、WML 以外のサービスとの直接の統合はありません。

    ```python
    custom_engine_credentials = {
    "url": "***",
    "username": "***",
    "password": "***"
    }

    binding_uid = client.data_mart.bindings.add('My custom engine', CustomMachineLearningInstance(custom_engine_credentials))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  以下のコマンドを使用すると、サービス・バインディングを参照できます。

    ```python
    client.data_mart.bindings.list()
    ```

    ![汎用 ML のバインディング](images/ml-generic-bind.png)

### カスタム・サブスクリプションの追加
{: #cml-cussub}

- サブスクライブを追加します

    ```python
    client.data_mart.subscriptions.add(CustomMachineLearningAsset(source_uid='action', binding_uid=binding_uid, prediction_column='predictedActionLabel'))
    ```

- サブスクリプション・リストを取得します

    ```python
    subscriptions = client.data_mart.subscriptions.get_details()

    subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```

### ペイロード・ロギングの有効化
{: #cml-cusenlog}

- サブスクリプション内でペイロード・ロギングを有効にします

    ```python
    subscription.payload_logging.enable()
    ```

- ロギングの詳細を取得します

    ```python
    subscription.payload_logging.get_details()
    ```

### スコアリングとペイロード・ロギング
{: #cml-cusscore}

- モデルをスコアリングします。完全な例については、[IBM {{site.data.keyword.aios_short}} とカスタム ML エンジンのノートブック ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: new_window} を参照してください。

- ペイロード・ロギング・テーブルに要求と応答を保管します

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time), PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    subscription.payload_logging.store(records=records_list)
    ```
    **注**: Python 以外の言語の場合、REST API を使用して、直接ペイロード・ロギングを実行することもできます。

    ```json
    token_endpoint = "https://iam.bluemix.net/identity/token"
    headers = {
            "Content-Type": "application/x-www-form-urlencoded",
            "Accept": "application/json"
    }

    data = {
            "grant_type":"urn:ibm:params:oauth:grant-type:apikey",
            "apikey":aios_credentials["apikey"]
    }

    req = requests.post(token_endpoint, data=data, headers=headers)
    token = req.json()['access_token']
    ```

    ```json
    import requests, uuid

    PAYLOAD_STORING_HREF_PATTERN = '{}/v1/data_marts/{}/scoring_payloads'
    endpoint = PAYLOAD_STORING_HREF_PATTERN.format(aios_credentials['url'], aios_credentials['data_mart_id'])

    payload = [{
      'binding_id': binding_uid,
      'deployment_id': subscription.get_details()['entity']['deployments'][0]['deployment_id'],
      'subscription_id': subscription.uid,
      'scoring_id': str(uuid.uuid4()),
      'response': response_data,
      'request': request_data
    }]

    headers = {"Authorization": "Bearer " + token}
    req_response = requests.post(endpoint, json=payload, headers = headers)
    print("Request OK: " + str(req_response.ok))
    ```

## IBM SPSS Collaboration & Deployment Services 機械学習エンジンの処理
{: #cml-spss}

### IBM SPSS C&DS 機械学習エンジンのバインド
{: #cml-spbind}

- IBM SPSS C&DS エンジンをカスタムとしてバインドします。この場合、単なるメタデータということになり、WML 以外のサービスとの直接の統合はありません。

    ```python
    SPSS_CDS_ENGINE_CREDENTIALS = {
    "username": "***",
    "password": "***",
    "url": "***"
    }

    binding_uid = client.data_mart.bindings.add('My SPSS C&DS engine', SPSSMachineLearningInstance(SPSS_CDS_ENGINE_CREDENTIALS))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  以下のコマンドを使用すると、サービス・バインディングを参照できます。

    ```python
    client.data_mart.bindings.list()
    ```

    ![SPSS ML のバインディング](images/ml-spss-bind.png)

### IBM SPSS C&DS サブスクリプションの追加
{: #cml-spsub}

- サブスクライブを追加します

    ```python
    client.data_mart.subscriptions.add(SPSSMachineLearningAsset(source_uid='source_uid', binding_uid=binding_uid, prediction_column='predictedActionLabel'))
    ```

- サブスクリプション・リストを取得します

    ```python
    subscriptions = client.data_mart.subscriptions.get_details()

    subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```

### スコアリングとペイロード・ロギング
{: #cml-spenlog}

- モデルをスコアリングします。完全な例については、[{{site.data.keyword.aios_short}} & SPSS C&DS エンジンのノートブック ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SPSS%20C%26DS%20Engine.ipynb){: new_window} を参照してください。

- ペイロード・ロギング・テーブルに要求と応答を保管します

    ```python
    records_list = [PayloadRecord(request=scoring_payload, response=result, response_time=response_time), PayloadRecord(request=scoring_payload, response=result, response_time=response_time)]

    subscription.payload_logging.store(records=records_list)
    ```

<!---
    **Note**: For languages other than Python, you can also perform payload logging directly, using a REST API.

    ```bash
    token_endpoint = "https://iam.bluemix.net/identity/token"
    headers = {
            "Content-Type": "application/x-www-form-urlencoded",
            "Accept": "application/json"
    }

    data = {
            "grant_type":"urn:ibm:params:oauth:grant-type:apikey",
            "apikey":aios_credentials["apikey"]
    }

    req = requests.post(token_endpoint, data=data, headers=headers)
    token = req.json()['access_token']
    ```

    ```json
    import requests, uuid

    PAYLOAD_STORING_HREF_PATTERN = '{}/v1/data_marts/{}/scoring_payloads'
    endpoint = PAYLOAD_STORING_HREF_PATTERN.format(aios_credentials['url'], aios_credentials['data_mart_id'])

    payload = [{
      'binding_id': binding_uid,
      'deployment_id': subscription.get_details()['entity']['deployments'][0]['deployment_id'],
      'subscription_id': subscription.uid,
      'scoring_id': str(uuid.uuid4()),
      'response': response_data,
      'request': request_data
    }]

    headers = {"Authorization": "Bearer " + token}
    req_response = requests.post(endpoint, json=payload, headers = headers)
    print("Request OK: " + str(req_response.ok))
    ```
--->

## Microsoft Azure 機械学習エンジンの処理
{: #cml-azure}

### MS Azure ML エンジンのバインド
{: #cml-azbind}

- WML 以外のエンジンをカスタムとしてバインドします。この場合、単なるメタデータということになり、WML 以外のサービスとの直接の統合はありません。

    ```python
    AZURE_ENGINE_CREDENTIALS = {
    "client_id": "***",
    "client_secret": "***",
    "subscription_id": "***",
    "tenant": "***"
    }

    binding_uid = client.data_mart.bindings.add('My Azure ML Studio engine', AzureMachineLearningInstance(AZURE_ENGINE_CREDENTIALS))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  以下のコマンドを使用すると、サービス・バインディングを参照できます。

    ```python
    client.data_mart.bindings.list()
    ```

    ![Azure ML のバインディング](images/ml-azure-bind.png)

### MS Azure ML サブスクリプションの追加
{: #cml-azsub}

- サブスクライブを追加します

    ```python
    client.data_mart.subscriptions.add(
        AzureMachineLearningAsset(source_uid=source_uid,
                                  binding_uid=binding_uid,
                                  input_data_type=InputDataType.STRUCTURED,
                                  problem_type=ProblemType.MULTICLASS_CLASSIFICATION,
                                  label_column='<my_label_column_name>',
                                  prediction_column='Scored Labels'))
    ```

- サブスクリプション・リストを取得します

    ```python
    subscriptions = client.data_mart.subscriptions.get_details()

    subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```

### ペイロード・ロギングの有効化
{: #cml-azenlog}

- サブスクリプション内でペイロード・ロギングを有効にします

    ```python
    subscription.payload_logging.enable()
    ```

- ロギングの詳細を取得します

    ```python
    subscription.payload_logging.get_details()
    ```

### スコアリングとペイロード・ロギング
{: #cml-azscore}

- モデルをスコアリングします。完全な例については、[Working with Azure Machine Learning Studio Engine ノートブック ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: new_window} を参照してください。

- 以下のようにして、ペイロード・ロギング・テーブルに要求と応答を保管します。

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time),
                    PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    for i in range(1, 10):
    records_list.append(PayloadRecord(request=request_data, response=response_data, response_time=response_time))

    subscription.payload_logging.store(records=records_list)
    ```
    **注**: Python 以外の言語の場合、REST API を使用して、直接ペイロード・ロギングを実行することもできます。

    ```json
    token_endpoint = "https://iam.bluemix.net/identity/token"
    headers = {
            "Content-Type": "application/x-www-form-urlencoded",
            "Accept": "application/json"
    }

    data = {
            "grant_type":"urn:ibm:params:oauth:grant-type:apikey",
            "apikey":aios_credentials["apikey"]
    }

    req = requests.post(token_endpoint, data=data, headers=headers)
    token = req.json()['access_token']
    ```

    ```json
    import requests, uuid

    PAYLOAD_STORING_HREF_PATTERN = '{}/v1/data_marts/{}/scoring_payloads'
    endpoint = PAYLOAD_STORING_HREF_PATTERN.format(aios_credentials['url'], aios_credentials['data_mart_id'])

    payload = [{
      'binding_id': binding_uid,
      'deployment_id': subscription.get_details()['entity']['deployments'][0]['deployment_id'],
      'subscription_id': subscription.uid,
      'scoring_id': str(uuid.uuid4()),
      'response': response_data,
      'request': request_data
    }]

    headers = {"Authorization": "Bearer " + token}
    req_response = requests.post(endpoint, json=payload, headers = headers)
    print("Request OK: " + str(req_response.ok))
    ```

## Amazon SageMaker 機械学習エンジンの処理
{: #cml-sage}

### AWS SageMaker ML エンジンのバインド
{: #cml-smbind}

- WML 以外のエンジンをカスタムとしてバインドします。この場合、単なるメタデータということになり、WML 以外のサービスとの直接の統合はありません。

    ```python
    SAGEMAKER_ENGINE_CREDENTIALS = {
    "access_key_id": "***",
    "secret_access_key": "***",
    "region": "***"
    }

    binding_uid = client.data_mart.bindings.add('My SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  以下のコマンドを使用すると、サービス・バインディングを参照できます。

    ```python
    client.data_mart.bindings.list()
    ```

    ![SageMaker ML のバインディング](images/ml-sagemaker-bind.png)

### Amazon SageMaker ML サブスクリプションの追加
{: #cml-smsub}

- サブスクライブを追加します

    ```python
    client.data_mart.subscriptions.add(
        SageMakerMachineLearningAsset(source_uid=source_uid,
                                  binding_uid=binding_uid,
                                  input_data_type=InputDataType.STRUCTURED,
                                  problem_type=ProblemType.MULTICLASS_CLASSIFICATION,
                                  label_column='<my_label_column_name>',
                                  prediction_column='Scored Labels'))
    ```

- サブスクリプション・リストを取得します

    ```python
    subscriptions = client.data_mart.subscriptions.get_details()

    subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```

### ペイロード・ロギングの有効化
{: #cml-smenlog}

- サブスクリプション内でペイロード・ロギングを有効にします

    ```python
    subscription.payload_logging.enable()
    ```

- ロギングの詳細を取得します

    ```python
    subscription.payload_logging.get_details()
    ```

### スコアリングとペイロード・ロギング
{: #cml-smscore}

- モデルをスコアリングします。完全な例については、[Working with SageMaker Machine Learning Engine ノートブック ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: new_window} を参照してください。

- ペイロード・ロギング・テーブルに要求と応答を保管します

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time),
                    PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    for i in range(1, 10):
    records_list.append(PayloadRecord(request=request_data, response=response_data, response_time=response_time))

    subscription.payload_logging.store(records=records_list)
    ```
    **注**: Python 以外の言語の場合、REST API を使用して、直接ペイロード・ロギングを実行することもできます。

    ```json
    token_endpoint = "https://iam.bluemix.net/identity/token"
    headers = {
            "Content-Type": "application/x-www-form-urlencoded",
            "Accept": "application/json"
    }

    data = {
            "grant_type":"urn:ibm:params:oauth:grant-type:apikey",
            "apikey":aios_credentials["apikey"]
    }

    req = requests.post(token_endpoint, data=data, headers=headers)
    token = req.json()['access_token']
    ```

    ```json
    import requests, uuid

    PAYLOAD_STORING_HREF_PATTERN = '{}/v1/data_marts/{}/scoring_payloads'
    endpoint = PAYLOAD_STORING_HREF_PATTERN.format(aios_credentials['url'], aios_credentials['data_mart_id'])

    payload = [{
      'binding_id': binding_uid,
      'deployment_id': subscription.get_details()['entity']['deployments'][0]['deployment_id'],
      'subscription_id': subscription.uid,
      'scoring_id': str(uuid.uuid4()),
      'response': response_data,
      'request': request_data
    }]

    headers = {"Authorization": "Bearer " + token}
    req_response = requests.post(endpoint, json=payload, headers = headers)
    print("Request OK: " + str(req_response.ok))
    ```

## 次のステップ
{: #cml-next}

- {{site.data.keyword.aios_short}} クライアントで続行するには、「[データベースの指定](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-cdb-connect)」のトピックを参照してください。

- Python コマンド・ライブラリーで続行するには、[Python クライアントの資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://ai-openscale-python-client.mybluemix.net/){: new_window} を参照してください。
