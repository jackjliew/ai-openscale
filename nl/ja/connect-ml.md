---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: payload, non-Watson, machine learning, services, subscription

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

# {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}} サービス以外のインスタンスのペイロード・ロギング
{: #cml-connect}

AI モデルを {{site.data.keyword.pm_full}} 以外の機械学習エンジンでデプロイしている場合、Python クライアントを使用して外部機械学習エンジンのペイロード・ロギングを有効にする必要があります。
{: shortdesc}

さらに詳しい情報については、[{{site.data.keyword.aios_short}} Python クライアント資料](http://ai-openscale-python-client.mybluemix.net/){: external}、および [{{site.data.keyword.aios_short}} チュートリアル](https://github.com/pmservice/ai-openscale-tutorials/blob/master/README.md){: external}に含まれているサンプル {{site.data.keyword.aios_short}} Python クライアント・ノートブックを参照してください。

## 始めに
{: #cml-prereq}

モデルのバイアスをモニターするためには、Db2 または {{site.data.keyword.cos_full}} でモデルの訓練データが利用できる状態になっている必要があります。 Python 関数では説明性と正解率はサポートされていません。 訓練データの詳細については、[{{site.data.keyword.aios_short}} が訓練データにアクセスする必要があるのはなぜですか?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata) を参照してください。

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
  資格情報は、「[資格情報の作成](/docs/services/ai-openscale?topic=ai-openscale-cred-create)」トピックに示されているステップに従って確認できます。

- PostgreSQL データベースでスキーマ名を作成します

- データマートをセットアップします

    ```python
    client.data_mart.setup(db_credentials=postgres_credentials, schema=schemaName)

    client.data_mart.get_details()
    ```

## カスタム機械学習エンジンでの作業
{: #cml-cusconfig}

### カスタム機械学習エンジンのバインド
{: #cml-cusbind}

- {{site.data.keyword.pm_full}} 以外のエンジンをカスタム、つまり単なるメタデータとしてバインドします。{{site.data.keyword.pm_full}} 以外のサービスとの直接的な統合はありません。 `client.data_mart.bindings.add` メソッドを使用して、複数の機械学習エンジンを {{site.data.keyword.aios_short}} にバインドできます。

    ```python
    custom_engine_credentials = {
    "url": "***",
    "username": "***",
    "password": "***"
    }

    binding_uid = client.data_mart.bindings.add('My custom engine', CustomMachineLearningInstance(custom_engine_credentials))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  次のコマンドを使用してサービス・バインディングを表示できます。

    ```python
    client.data_mart.bindings.list()
    ```

    ![汎用 ML バインディング](images/ml-generic-bind.png)

### カスタム・サブスクリプションの追加
{: #cml-cussub}

- サブスクリプションを追加します

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

- サブスクリプションでペイロード・ロギングを有効にします

    ```python
    subscription.payload_logging.enable()
    ```

- ロギングの詳細を取得します

    ```python
    subscription.payload_logging.get_details()
    ```

詳しくは、[ペイロード・ロギング]()を参照してください。

### 評価とペイロード・ロギング
{: #cml-cusscore}

- モデルを評価します。 完全なサンプルについては、[IBM {{site.data.keyword.aios_full}} & カスタム ML エンジン・ノートブック](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}を参照してください。

- ペイロード・ロギング・テーブルにリクエストと応答を格納します

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time), PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    subscription.payload_logging.store(records=records_list)
    ```
    **注**: Python 以外の言語の場合、REST API を使用してペイロード・ロギングを直接実行することもできます。

    ```json
    token_endpoint = "https://iam.cloud.ibm.com/identity/token"
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

## Microsoft Azure Machine Learning エンジンでの作業
{: #cml-azconfig}

### Microsoft Azure Machine Learning エンジンのバインド
{: #cml-azbind}

- {{site.data.keyword.pm_full}} 以外のエンジンをカスタム、つまり単なるメタデータとしてバインドします。{{site.data.keyword.pm_full}} 以外のサービスとの直接的な統合はありません。

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
  次のコマンドを使用してサービス・バインディングを表示できます。

    ```python
    client.data_mart.bindings.list()
    ```

    ![Azure ML バインディング](images/ml-azure-bind.png)

### MS Azure ML サブスクリプションの追加
{: #cml-azsub}

- サブスクリプションを追加します

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

- サブスクリプションでペイロード・ロギングを有効にします

    ```python
    subscription.payload_logging.enable()
    ```

- ロギングの詳細を取得します

    ```python
    subscription.payload_logging.get_details()
    ```

### 評価とペイロード・ロギング
{: #cml-azscore}

- モデルを評価します。 完全なサンプルについては、[Azure Machine Learning Studio エンジン・ノートブック](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}を参照してください。

- ペイロード・ロギング・テーブルにリクエストと応答を格納します。

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time),
                    PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    for i in range(1, 10):
    records_list.append(PayloadRecord(request=request_data, response=response_data, response_time=response_time))

    subscription.payload_logging.store(records=records_list)
    ```
    **注**: Python 以外の言語の場合、REST API を使用してペイロード・ロギングを直接実行することもできます。

    ```json
    token_endpoint = "https://iam.cloud.ibm.com/identity/token"
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

## Amazon SageMaker 機械学習エンジンでの作業
{: #cml-smconfig}

### Amazon SageMaker 機械学習エンジンのバインド
{: #cml-smbind}

- {{site.data.keyword.pm_full}} 以外のエンジンをカスタム、つまり単なるメタデータとしてバインドします。{{site.data.keyword.pm_full}} 以外のサービスとの直接的な統合はありません。

    ```python
    SAGEMAKER_ENGINE_CREDENTIALS = {
    "access_key_id": "***",
    "secret_access_key": "***",
    "region": "***"
    }

    binding_uid = client.data_mart.bindings.add('My SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS))

    bindings_details = client.data_mart.bindings.get_details()
    ```
  次のコマンドを使用してサービス・バインディングを表示できます。

    ```python
    client.data_mart.bindings.list()
    ```

    ![SageMaker ML バインディング](images/ml-sagemaker-bind.png)

### Amazon SageMaker ML サブスクリプションの追加
{: #cml-smsub}

- サブスクリプションを追加します

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

- サブスクリプションでペイロード・ロギングを有効にします

    ```python
    subscription.payload_logging.enable()
    ```

- ロギングの詳細を取得します

    ```python
    subscription.payload_logging.get_details()
    ```

### 評価とペイロード・ロギング
{: #cml-smscore}

- モデルを評価します。 完全なサンプルについては、[SageMaker 機械学習エンジン・ノートブック](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: external}を参照してください。


- ペイロード・ロギング・テーブルにリクエストと応答を格納します。

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time),
                    PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    for i in range(1, 10):
    records_list.append(PayloadRecord(request=request_data, response=response_data, response_time=response_time))

    subscription.payload_logging.store(records=records_list)
    ```
    **注**: Python 以外の言語の場合、REST API を使用してペイロード・ロギングを直接実行することもできます。

    ```json
    token_endpoint = "https://iam.cloud.ibm.com/identity/token"
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

- {{site.data.keyword.aios_short}} クライアントの処理を続けるには、[データベースの指定](/docs/services/ai-openscale?topic=ai-openscale-connect-db)を参照してください。

- Python コマンド・ライブラリーを使用して作業を続けるには、[Python クライアント資料](http://ai-openscale-python-client.mybluemix.net/){: external}を参照してください。
